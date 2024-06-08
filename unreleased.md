# 即将发布的更新

Apktool是一个用于处理Android应用程序APK文件的工具，它允许开发者逆向工程和解编译APK文件，以便进行修改和重新打包。以下是Apktool即将发布的更新内容：

- [[#3476](https://github.com/iBotPeaches/Apktool/pull/3476)]：新增了对`build`命令的并行处理功能，提高了构建速度。
- [[#3559](https://github.com/iBotPeaches/Apktool/pull/3559)]：移除了Proguard，改用R8进行代码混淆，使得构建过程更加稳定和可重复。
- [[#3602](https://github.com/iBotPeaches/Apktool/issues/3602)]：针对xmlpull组件，修复了在处理过程中剥离`META-INF`文件的问题。
- [[#3512](https://github.com/iBotPeaches/Apktool/issues/3512)]：改进了对Facebook应用的反汇编处理，解决了相关问题。
- [[#3536](https://github.com/iBotPeaches/Apktool/issues/3536)]：修正了将`stamp-cert-sha256`视为未知文件的问题。
- [[#3578](https://github.com/iBotPeaches/Apktool/issues/3578)]：修复了将非主类DEX文件错误识别为压缩文件的问题。
- [[#3583](https://github.com/iBotPeaches/Apktool/issues/3583)]：修正了序列化器在处理命名空间限制时的对齐问题。
- [[#3519](https://github.com/iBotPeaches/Apktool/pull/3519), [#3601](https://github.com/iBotPeaches/Apktool/pull/3601)]：将baksmali/smali库升级至版本`3.0.7`。
- [[#3459](https://github.com/iBotPeaches/Apktool/pull/3459), [#3595](https://github.com/iBotPeaches/Apktool/pull/3595)]：将Gradle升级至版本`8.7`。
- [[#3509](https://github.com/iBotPeaches/Apktool/pull/3509)]：将`proguard-gradle`升级至版本`7.4.2`。
- [[#3577](https://github.com/iBotPeaches/Apktool/pull/3577), [#3607](https://github.com/iBotPeaches/Apktool/pull/3607)]：将`commons-cli`库升级至版本`1.8.0`。
- [[#3560](https://github.com/iBotPeaches/Apktool/pull/3560), [#3570](https://github.com/iBotPeaches/Apktool/pull/3570)]：将`commons-io`库升级至版本`2.16.1`。
- [[#3576](https://github.com/iBotPeaches/Apktool/pull/3576)]：将`commons-text`库升级至版本`1.12.0`。
- [[#3585](https://github.com/iBotPeaches/Apktool/pull/3585)]：将`xmlunit-legacy`库升级至版本`2.10.0`。
- [[#3510](https://github.com/iBotPeaches/Apktool/pull/3510), [#3515](https://github.com/iBotPeaches/Apktool/pull/3515), [#3550](https://github.com/iBotPeaches/Apktool/pull/3550), [#3572](https://github.com/iBotPeaches/Apktool/pull/3572)]：将`wrapper-validation-action`升级至版本`3.3.0`。
- [[#3470](https://github.com/iBotPeaches/Apktool/pull/3470), [#3479](https://github.com/iBotPeaches/Apktool/pull/3479), [#3500](https://github.com/iBotPeaches/Apktool/pull/3500), [#3511](https://github.com/iBotPeaches/Apktool/pull/3511), [#3522](https://github.com/iBotPeaches/Apktool/pull/3522), [#3566](https://github.com/iBotPeaches/Apktool/pull/3566), [#3571](https://github.com/iBotPeaches/Apktool/pull/3571), [#3575](https://github.com/iBotPeaches/Apktool/pull/3575), [#3586](https://github.com/iBotPeaches/Apktool/pull/3586)]：将`gradle/actions`升级至版本`3.3.2`。
- [[#3471](https://github.com/iBotPeaches/Apktool/pull/3471)]：将`github/codeql-action`升级至版本`3`。
- [[#3528](https://github.com/iBotPeaches/Apktool/pull/3528)]：将`actions/upload-artifact`升级至版本`4`。

以上更新内容均处于待最终确定状态，可能会有所变动。