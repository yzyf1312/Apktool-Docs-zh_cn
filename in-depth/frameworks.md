# 应用框架资源

Android应用程序在开发过程中会使用到操作系统自带的代码和资源，这些被称为框架资源。Apktool是一个工具，它依赖这些框架资源来正确解码和解构APK文件。

每当Apktool发布新版本时，它都会包含当时最新的AOSP（Android Open Source Project）框架。这使得大多数APK文件可以在不遇到问题的情况下被解码和构建。然而，制造商通常会在标准的AOSP框架之外添加自己的框架文件。如果你想使用Apktool处理这些制造商的APK文件，你必须首先安装相应的制造商框架文件。

**例如**：如果你想解码HTC设备上的`HtcContacts.apk`文件，你可能会遇到错误。

```text
$ apktool d HtcContacts.apk
I: Loading resource table...
I: Decoding resources...
I: Loading resource table from file: 1.apk
W: Could not decode attr value, using undecoded value instead: ns=android, name=drawable
W: Could not decode attr value, using undecoded value instead: ns=android, name=icon
Can't find framework resources for package of id: 2. You must install proper framework files, see project website for more info.
```

这是因为Apktool无法找到用于该应用程序的框架资源。在这种情况下，你需要从设备中提取HTC的框架资源文件`com.htc.resources.apk`并安装它。

```text
$ apktool if com.htc.resources.apk
I: Framework installed to: 2.apk
```

安装后，你可以再次尝试解码APK文件。

```text
$ apktool d HtcContacts.apk
I: Loading resource table...
I: Decoding resources...
I: Loading resource table from file: /home/brutall/apktool/framework/1.apk
I: Loading resource table from file: /home/brutall/apktool/framework/2.apk
I: Copying assets and libs...
```

现在Apktool能够正确地使用`1.apk`和`2.apk`两个框架文件来解码应用程序。

### 寻找框架文件

在大多数设备上，框架文件位于`/system/framework`目录。在一些设备上，它们可能位于`/data/system-framework`，甚至可能巧妙地隐藏在`/system/app`或`/system/priv-app`目录中。这些文件通常命名为"resources"、"res"或"framework"。

> **信息**
>
> HTC有一个名为`com.htc.resources.apk`的框架文件，而LG有一个名为`lge-res.apk`的框架文件。

找到框架文件后，你可以通过`adb pull /path/to/file`或使用文件管理器应用程序来提取它。在获取文件后，请注意Apktool的安装方式。框架在安装过程中被命名的数字与应用程序的pkgId相对应。这些数值范围应在1至30之间。任何安装为`127`的 APK 都是`0x7F`，这是一个内部pkgId。

### 内部框架

Apktool 自带一个内部框架。在执行过程中，该文件会被复制到本地计算机上。

> **警告**
>
> Apktool 不知道内部框架的版本。它总会认为这是最新版本，因此请在Apktool升级时删除该文件。

### 管理框架文件

框架文件的存储位置取决于操作系统。

- 在Linux系统中，它们位于`$HOME/.local/share/apktool`。
- 在Windows系统中，它们位于`%UserProfile%\AppData\Local\apktool`。
- 在Mac系统中，它们位于`$HOME/Library/apktool`。

如果这些目录不可用，Apktool将默认使用`java.io.tmpdir`，通常是`/tmp`。这是一个临时目录，因此使用`--frame-path`参数选择框架文件的替代文件夹是有意义的。

由于这些位置有时是隐藏的目录，管理这些框架文件可能会变得困难。Apktool v2.2.1版本增加了一个帮助函数，允许你运行`apktool empty-framework-dir`来清空框架文件。

> **信息**
>
> Apktool不会控制安装后的框架，但你可以自行管理这些文件。

### 标签框架文件

框架文件可以根据pkgId和可选的自定义标签进行命名，格式为`<id>-<tag>.apk`。通常，给框架文件打标签不是必需的，但如果你处理来自多个不同设备的应用程序，并且它们的框架不兼容，你将需要一种简便的方式来在它们之间切换。

你可以通过以下命令给框架文件打标签：

```shell
$ apktool if com.htc.resources.apk -t hero
I: Framework installed to: /home/brutall/apktool/framework/2-hero.apk
$ apktool if com.htc.resources.apk -t desire
I: Framework installed to: /home/brutall/apktool/framework/2-desire.apk
```

然后你可以使用这些标签来解码APK文件：

```shell
$ apktool d HtcContacts.apk -t hero
I: Loading resource table...
I: Decoding resources...
I: Loading resource table from file: /home/brutall/apktool/framework/1.apk
I: Loading resource table from file: /home/brutall/apktool/framework/2-hero.apk
I: Copying assets and libs...
$ apktool d HtcContacts.apk -t desire
I: Loading resource table...
I: Decoding resources...
I: Loading resource table from file: /home/brutall/apktool/framework/1.apk
I: Loading resource table from file: /home/brutall/apktool/framework/2-desire.apk
I: Copying assets and libs...
```

当构建APK时，你不必选择标签，因为Apktool会自动使用与解码时相同的标签。