# 资源模式

Apktool可以提取和解析APK中的资源文件和AndroidManifest.xml文件。在Apktool v2.9.0中，引入了一项新配置，用于决定在反编译过程中如何处理未解析的资源。

### 背景

在处理应用程序时，可以使用`aapt`工具（`aapt d resources app.apk`）来查看资源文件。例如，对于一个名为`bugged.apk`的应用程序，使用`aapt`工具可以列出其中的资源包和资源条目。

```text
➜ aapt d resources bugged.apk
Package Groups (1)
Package Group 0 id=0x7f packageCount=1 name=com.ibotpeaches.arsctest
  Package 0 id=0x7f name=com.ibotpeaches.arsctest
    type 0 configCount=1 entryCount=10
      spec resource 0x7f010000 com.ibotpeaches.arsctest:color/black: flags=0x00000000
      spec resource 0x7f010001 com.ibotpeaches.arsctest:color/purple_200: flags=0x00000000
      spec resource 0x7f010002 com.ibotpeaches.arsctest:color/purple_500: flags=0x00000000
      spec resource 0x7f010003 com.ibotpeaches.arsctest:color/purple_700: flags=0x00000000
      spec resource 0x7f010004 com.ibotpeaches.arsctest:color/teal_200: flags=0x00000000
      spec resource 0x7f010005 com.ibotpeaches.arsctest:color/teal_700: flags=0x00000000
      spec resource 0x7f010006 com.ibotpeaches.arsctest:color/white: flags=0x00000000
      INVALID TYPE CONFIG FOR RESOURCE 0x7f010007
      INVALID TYPE CONFIG FOR RESOURCE 0x7f010008
      spec resource 0x7f010009 com.ibotpeaches.arsctest:color/bugged: flags=0x00000000
```

在上述例子中，资源`0x7f010007`和`0x7f010008`无法被解析。然而，用户收到的错误消息仅仅是一个包裹了底层问题的外壳，可能的问题包括：

- 未找到资源包。
- 未找到资源类型。
- 资源名称的标识符无效。
- 在字符串解包过程中UTF-8索引无效。
- 在字符串解包过程中UTF-16索引无效。
- 未找到资源条目。

因此，理解到底存在什么问题是相当困难的。

### 历史

在Apktool能够保持资源ID静态之前，它会故意为这些问题创建占位符资源。这些占位符资源可能看起来像这样：

```xml
<item type="color" name="APKTOOL_DUMMY_7f010007" />
<item type="color" name="APKTOOL_DUMMY_7f010008" />
```

当构建资源表时，ID不会因为占位符资源而移位，因为占位符资源填满了所有资源未能正确分解的位置。然而，这种做法随着时间的推移变得不再必要，因为保持资源ID静态的代价是使它们成为公共资源，这与Android提升安全性的趋势背道而驰。

此外，在2019年Apktool被注意到无意中使用占位符资源导致了对应用程序进行标识，因为当时一家大型公司使用Apktool重新命名其应用程序并重新发布到商店。这篇帖子可以在[这里](https://connortumbleson.com/2019/06/02/apktool-in-the-wild/)找到。

随着稀疏资源支持的引入，Apktool中的占位符资源意外地破坏了一些功能，但大多数人并未注意到这一点。这实际上是一个积极的变化，因为它解决了以前处理的一些奇怪问题。

例如，Apktool v2.8.x中错误地将未知资源拆分成如下形式：

```xml
<attr name="actionBarSize" format="dimension">
    <enum name="@null" value="0" />
</attr>
```

这种做法是不恰当的，因为未解析的资源名不能为`@null`。

替换成占位符资源是否更好呢？

```xml
<attr name="actionBarSize" formats="dimension">
    <enum name="APKTOOL_DUMMY_0x7f090459" value="0" />
</attr>
```

虽然有人可能认为这样做更好，但如果你正在拆解一个没有引用此属性的资源，那么发明一个占位符资源来满足它似乎就显得不合理了。

因此，另一个选择是简单地移除未解析的资源。

```xml
<attr name="actionBarSize" formats="dimension"/>
```

这里的挑战在于，每个单独的使用案例可能都倾向于选择不同的选项。

### 资源模式

在反编译过程中，可以通过运行`-resm <mode>`来设置Apktool处理未解析资源的模式。

##### 移除模式（默认）

- `remove` | `delete`

Apktool将移除任何未解析的资源。这是默认行为。

```xml
<attr name="actionBarSize" formats="dimension"/>
```

##### 占位符模式

- `dummy` | `dummies`

Apktool将使用占位符值填充未解析的资源。

```xml
<attr name="actionBarSize" formats="dimension">
    <enum name="APKTOOL_DUMMY_0x7f090459" value="0" />
</attr>
```

##### 保留模式

- `keep` | `preserve`

Apktool将保留资源，但如果名称被剥离，它将适当制作有效的资源名称。

```xml
<attr name="actionBarSize" format="dimension">
    <enum name="resUnk0x7f090459" value="0" />
</attr>
```
