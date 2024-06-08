# CLI参数

### 实用选项

*适用于实用命令（`apktool {options}`）*

```text
-advance, --advanced
```

- 输出高级使用输出。

```text
-version, --version
```

- 输出当前软件版本。（例如：1.5.2）

### 解码选项

*用于解码的命令（`apktool d file.apk {options}`）*

```text
-api, --api-level <API>
```

- 设置生成的smali文件中使用的API级别。
 - 默认为`targetSdkVersion`

```text
-b, --no-debug-info
```

- 阻止baksmali写入调试信息（`.local`, `.param`, `.line`等）。

```text
-f, --force
```

- 强制删除目标目录。

```text
--force-manifest
```

- 无论使用了什么解码选项，都强制Apktool解码`AndroidManifest.xml`。

```text
--keep-broken-res
```

- 如果抛出错误并且丢弃了一些资源，您仍然想要解码它们。
 - 例如：“检出无效配置标志。丢弃资源”。
 - 您将不得不在构建之前手动修复它们。

```text
-m, --match-original
```

- 使生成的文件尽可能接近原始文件。
 - 代价是这可能妨碍重新构建。

```text
--no-assets
```

- 防止解码/复制未知资产文件。

```text
--only-main-classes
```

- 只反汇编位于应用程序根目录中的dex类。

```text
-p, --frame-path <DIR>
```

- 设置框架文件存储/读取的文件夹。

```text
-r, --no-res
```

- 防止反编译资源。
 - 保留`resources.arsc`完好无损，即不对其作任何处理。

```text
-resm, --resource-mode <mode>
```

- 设置解析资源时使用的模式。
 - `remove`（默认） - 移除无法解析的资源。
 - `dummy` - 为无法解析的资源添加一个占位资源。
 - `keep` - 使用`APKTOOL_MISSING_{resId}`命名法保留未解析的资源。

```text
-s, --no-src
```

- 防止反汇编dex文件。
 - 留下dex文件不变，并在构建时移动它们。

```text
-t, --frame-tag <TAG>
```

- 使用由`TAG`标记的框架文件。

### 构建选项

*适用于构建命令（`apktool b folder {options}`）*

```text
-a, --aapt <FILE>
```

- 从指定位置加载aapt/aapt2二进制文件。
 - 这些用于代替内部版本。

```text
-api, --api-level <API>
```

- 设置用于构建的smali文件的API级别。
 - 默认为`minSdkVersion`。

```text
-c, --copy-original
```

- 复制原始的`AndroidManifest.xml`和`META-INF`。

```text
-d, --debug
```

- 在`AndroidManifest.xml`中添加`debuggable="true"`，即允许调试。

```text
-f, --force-all
```

- 在构建过程中覆盖现有文件。
 - 包括资源和源代码。

```text
-n, --net-sec-conf
```

-在apk中添加通用网络安全配置文件。

```text
-nc, --no-crunch
```

-禁止在构建过程中压缩资源文件。

 - 防止aapt/aapt2自动优化位图。

```text
-o, --output <FILE>
```

-设置输出apk的名称。
 - 默认是`dist/{apkname}.apk`。

```text
-p, --frame-path <DIR>
```

-设置存储/读取框架文件的文件夹。

```text
--use-aapt1
```

-使用`aapt`而不是`aapt2`。

 - Apktool在v2.9.0及以上版本中默认使用`aapt2`。

```text
--use-aapt2
```

-使用`aapt2`而不是`aapt`。

 - Apktool在v2.8.2及以上版本中默认使用`aapt`。

### 空框架目录选项

*适用于空框架目录命令（`apktool empty-framework-dir {options}`）*

```text
-f, --force
```

- 强制删除目标目录。

```text
-p, --frame-path <DIR>
```

- 设置存储/读取框架文件的文件夹。

### 列出框架目录选项

*适用于列出框架命令（`apktool list-frameworks {options}`）*

```text
-p, --frame-path <DIR>
```

- 设置存储/读取框架文件的文件夹。

### 通用选项

*可以与任何命令一起使用的选项*

```text
-v, --verbose
```

-详细输出。
 - 包括任何标有`FINE`的日志消息。

```text
-q, --quiet
```

-安静输出。