# resources.arsc文件

在Android应用程序中，`resources.arsc`是一个二进制文件，它包含了应用程序的资源。文件扩展名`.arsc`暗示了它是Android Resource Storage Container（Android 资源存储容器），这是一个包含大量chunk的集合。

如果我们查看文件的第一行，会看到以下内容：

```text
00000000: 0200 0c00 f00b 0000 0100 0000 0100 1c00  ................
```

`.arsc`文件使用`ResChunk_header`来描述文件中的各个chunk。这个头部位于文件的开始处，其结构如下：

### ResChunk_header

| 名称       | 大小 | 描述                 |
| ---------- | ---- | -------------------- |
| Type       | 2字节 | chunk的类型           |
| Header Size | 2字节 | 头部的大小           |
| Size       | 4字节 | chunk的大小           |

由于我们知道文件采用的是小端格式，我们可以解析出这个头部。我们得到：

- Type - `0x0002`
- Header Size - `0x000c`
- Size - `0x00000bf0`

因此，我们可以利用[ResourceTypes.h](https://github.com/iBotPeaches/platform_frameworks_base/blob/master/libs/androidfw/include/androidfw/ResourceTypes.h)文件来理解这个chunk是什么。

```cpp
enum {
    RES_NULL_TYPE                     = 0x0000,
    RES_STRING_POOL_TYPE              = 0x0001,
    RES_TABLE_TYPE                    = 0x0002,
    RES_XML_TYPE                      = 0x0003,
};
```

我们从文件的`RES_TABLE_TYPE`（`0x0002`）开始。这个chunk的描述如下：

| 名称          | 大小 | 描述                 |
| ------------- | ---- | -------------------- |
| Header        | 8字节 | chunk的类型           |
| Package Count | 4字节 | 包的数量             |

这是一个简单的chunk，它帮助我们理解文件中有多少个`ResTable_package` chunks。现在我们知道每个chunk都以`ResChunk_header`开始，我们可以安全地读取下一个chunk来查看它是什么。

再次查看该行并标记我们已经阅读的部分：

```text
00000000: [0200 0c00 f00b 0000] 0100 0000 0100 1c00  ................
```

我们可以看到，接下来的chunk是`RES_STRING_POOL_TYPE`（`0x0001`）。这个字符串池chunk的描述如下：

| 名称          | 大小 | 描述                                            |
| ------------- | ---- | ------------------------------------------------ |
| String Count  | 4字节 | 池中字符串的数量                              |
| Style Count   | 4字节 | 池中span数组样式的数量                      |
| Flags         | 4字节 | 字符串是UTF-8还是UTF-16编码，是否排序         |
| String Offset | 4字节 | 从头部到字符串数据的偏移量                    |
| Style Offset  | 4字节 | 从头部到样式数据的偏移量                      |

这个chunk比前一个更复杂，但它仍然可以被我们解析。我们可以了解到字符串和样式的数量，以及它们在文件中的起始位置。因此，Apktool在这种情况下通过读取这些数据池并将它们存储在内存中，从而允许我们稍后通过索引引用它们。

字符串池本身有许多奇怪和奇特的地方，我们在本文中将不涵盖它们。如果你想深入了解字符串池是如何工作的，可以查阅相关的文档。目前，假设你可以通过字符串池的索引获得字符串。

字符串池很重要，因为它包含了整个资源表的所有字符串值。然而，除了条目名称或类型标识符外，其他内容都不包含在该池中。

因此，假设我们正确地读取了池，或者从`ResChunk_header`中省略了它，我们最终到达了另一个新的chunk。以下是字符串池之后的相关部分。

```text
00000340: 0000 0000] 0002 2001 ac08 0000 7f00 0000  ...... .........
00000350: 6300 6f00 6d00 2e00 6900 6200 6f00 7400  c.o.m...i.b.o.t.
00000360: 7000 6500 6100 6300 6800 6500 7300 2e00  p.e.a.c.h.e.s...
00000370: 6100 7200 7300 6300 7400 6500 7300 7400  a.r.s.c.t.e.s.t.
```

- `]` -字符串池的结束。

如果我们读取另一个`ResChunk_header`，我们会得到一个新的类型的chunk。这个chunk是`RES_TABLE_TYPE`（`0x0200`），它的描述如下：

| 名称                           | 大小     | 描述                                                  |
| ------------------------------ | -------- | ---------------------------------------------------- |
| Package Id                     | 4字节   | 包ID                                                 |
| Package Name                   | 可变     | 包名称，以null结尾                                 |
| Type String Offset             | 4字节   | 类型符号表的偏移量，如果继承自另一个包，则可能为零 |
| Last Public Type String Offset | 4字节   | 上述表中公共类型的最后索引                            |
| Key Symbol Offset              | 4字节   | 键符号表的偏移量，如果继承自另一个包，则可能为零 |
| Last Public Key Symbol Offset  | 4字节   | 上述表中公钥符号的最后索引                            |
| Type Id Offset                 | 4字节   | 分割apk的特定类型ID的偏移量                            |

这个chunk属性和解释表明，它将启动child chunks：`ResTable_type`和`ResTable_typeSpec`。