# 构建选项

`Apktool` 的构建选项可以通过 `b` 或 `build` 命令来调用，具体用法如下：

```bash
$ apktool b foo.jar.out
# 将 foo.jar.out 文件夹构建成 foo.jar.out/dist/foo.jar。

$ apktool build foo.jar.out
# 同样将 foo.jar.out 文件夹构建成 foo.jar.out/dist/foo.jar。

$ apktool b bar
# 将 bar 文件夹构建成 bar/dist/bar.apk。

$ apktool b .
# 将当前目录构建成 ./dist。

$ apktool b bar -o new_bar.apk
# 将 bar 文件夹构建成 new_bar.apk。

$ apktool b bar.apk
# 用法错误。必须使用文件夹，而不是 .apk 或 .jar 文件。
```

> **信息**
>
> 为了运行重新构建的应用程序，你必须对其进行重新签名。Android 官方文档 [Sign your app](https://developer.android.com/studio/publish/app-signing#signing-manually) 提供了手动签名应用程序的指导。