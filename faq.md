# 常见问题解答

### 关于原始YouTube视频中的`-j`开关

在原始的YouTube视频中提到的`-j`开关实际上并不存在。请参考[Issue 199](https://github.com/iBotPeaches/Apktool/issues/199)以获取详细信息。

### 关于在Android设备上运行Apktool的可能性

目前官方不支持在Android设备上运行Apktool，因为存在一些兼容性问题，特别是在Android早期版本中，使用`aapt`二进制文件可能会遇到困难，并且旧版Android系统在使用`java.nio`库时也会遇到问题。非官方的包只能通过交叉编译二进制文件来实现运行。

### Apktool源代码在哪下载？

Apktool的源代码可以从[GitHub](https://github.com/iBotPeaches/Apktool)或[Bitbucket](https://bitbucket.org/iBotPeaches/apktool/overview)的仓库中下载。

### 反编译后的APK文件大小异常减小

反编译后的APK文件比原始文件小可能有几个原因：

- Apktool构建的是未签名的APK，这意味着某些目录和文件，如`META-INF`，可能缺失。
- 更新的构建过程 - Apktool使用现代版本的`aapt`/`aapt2`，这可能减少了文件大小。

### 反编译后的APK文件中缺少`META-INF`目录

`META-INF`目录包含APK的签名。一旦APK被修改，它就不再被签名。您可以使用`-c / --copy-original`选项来保留这些签名。然而，`-c`选项将使用原始的`AndroidManifest.xml`，并且只能与原始APK签名v1方案一起工作。

### 什么是“Magic APKs”？

有些APK是使用专为特定OEM设计的修改过的构建工具构建的。这些APK不是使用常规的AOSP工具构建的，因此与Apktool不兼容。Apktool无法解码或构建这些APK。

### 能否将Apktool集成到自己的项目中？能否修改它？是否需要提及原开发者？

Apktool使用的[Apache](https://github.com/iBotPeaches/Apktool/blob/master/LICENSE.md)许可证可以回答这些问题：

- 您可以在未经许可的情况下重新分发和/或修改Apktool。
- 然而，如果可以的话，最好添加贡献者（`brut.all`，`iBotPeaches`，`JesusFreke`）到您的致谢名单中。

### Apktool存储框架文件的位置在哪？

- Windows：`$HOME/AppData/Local/apktool`
- Mac：`$HOME/Library/apktool`
- Linux：`$HOME/.local/share/apktool`