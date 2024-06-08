# 解码选项

`Apktool` 的解码选项可以通过`d`或`decode`命令来调用，具体用法如下：

```bash
$ apktool d foo.jar
# 将foo.jar解码到foo.jar.out文件夹

$ apktool decode foo.jar
# 将foo.jar解码到foo.jar.out文件夹

$ apktool d bar.apk
# 将bar.apk解码到bar文件夹

$ apktool decode bar.apk
# 将bar.apk解码到bar文件夹

$ apktool d bar.apk -o baz
# 将bar.apk解码到baz文件夹
```
