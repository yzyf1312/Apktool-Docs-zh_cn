# 框架安装

框架可以通过`if`或`install-framework`命令进行安装，并可以附加两个参数。

- `-p, --frame-path <directory>`：将框架文件存储在指定的`<dir>`目录中。
- `-t, --tag <tag>`：使用`<dir>`作为标签来标记框架。

这允许您更精细地控制文件的存储和命名方式。

```bash
$ apktool if framework-res.apk
I: Framework installed to: 1.apk
# framework-res.apk的pkgId决定了编号。(即0x01)

$ apktool if com.htc.resources.apk
I: Framework installed to: 2.apk
# com.htc.resources.apk的pkgId是0x02

$ apktool if com.htc.resources.apk -t htc
I: Framework installed to: 2-htc.apk
# pkgId-tag.apk

$ apktool if framework-res.apk -p foo/bar
I: Framework installed to: foo/bar/1.apk

$ apktool if framework-res.apk -t baz -p foo/bar
I: Framework installed to: foo/bar/1-baz.apk
```