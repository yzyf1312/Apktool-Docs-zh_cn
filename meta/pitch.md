# 推销与反推销

很多时候，人们会问--这与xxx工具有什么不同？这是一个合理的问题，也是一个应该问的问题。然而，这也是一个经常被恶意提出的问题。这里可以大致解答这两个问题。

因此，本文将给你一个 “推销”（为什么你应该使用Apktool）和一个 “反推销”（为什么你不应该使用Apktool）。

### 为什么你应该使用Apktool

- Apktool已经存在超过13年，拥有大量的用户群体，因此你几乎可以在任何地方找到支持。
- Apktool是开源软件，你可以查看其工作原理，甚至贡献代码。
- Apktool是免费的，它遵循Apache 2.0许可证，使用起来非常灵活。
  - Apktool建立在其他人的研究和工作之上，许多工具都是基于Apktool构建的，你也可以这样做。

- Apktool支持跨平台，可以在Windows、Linux和macOS上运行。
- Apktool是一个单一的jar文件，不需要额外安装任何东西就可以使用。
- Apktool提供了一个简单的命令来进行反编译和重新组装。

### 为什么你不应该使用Apktool

- Apktool在Android设备上的表现并不理想，因为它使用与Android Studio相同的原生工具进行应用编译
  - 这意味着为了在设备上构建应用程序，你需要为相应的架构交叉编译aapt/aapt2。
  - 虽然这并非不可能，但并不容易，也不是Apktool官方想要投入时间的方向。
  - 为了取代设备上的aapt/aapt2，已经发明了如[ARSCLib](https://github.com/REAndroid/ARSCLib)这样的库。

- Apktool在修复问题和添加功能方面工作缓慢。
  - Apktool是唯一当前维护者的侧项目，他有全职工作和其他责任。
  - 付费替代品如[JEB from PNF Software](https://www.pnfsoftware.com/jeb/android)提供了可能超越Apktool的昂贵选项。
  - 免费官方替代品如[apkanalyzer](https://developer.android.com/tools/apkanalyzer)可能更新更快，但在第三方混淆的最低级别上也会失败。

- Apktool返回smali格式而不是重构的Java代码，这对于新用户来说往往是一个障碍。
  - [JADX](https://github.com/skylot/jadx)是一个很好的替代方案，它会返回Java代码而不是smali，并且有一个增长的健壮资源解析器。

