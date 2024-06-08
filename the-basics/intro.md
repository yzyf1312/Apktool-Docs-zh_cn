# 引言

首先，让我们来了解一下APK文件。APK文件其实就是一个包含资源和组装好的Java代码的ZIP文件。如果你像这样简单地解压一个APK文件，你会得到诸如`classes.dex`和`resources.arsc`这样的文件。

```shell
$ unzip testapp.apk
Archive: testapp.apk
inflating: AndroidManifest.xml
inflating: classes.dex
extracting: res/drawable-hdpi/ic_launcher.png
inflating: res/xml/literals.xml
inflating: res/xml/references.xml
extracting: resources.arsc
```

然而，在这个阶段，你只是解压缩了编译后的源代码。如果你试图查看`AndroidManifest.xml`，你会看到这样的内容。

```shell
�����������P��������������4���F���������������������0��\��f��n���v�e�r�s�i�o�n�C�o�d�e����v�e�r�s�i�o�n�N�a�m�e����a�n�d�r�o�i�d���*�h�t�t�p�:�/�/�s�c�h�e�m�a�s�.�a�n�d�r�o�i�d�.�c�o�m�/�a�p�k�/�r�e�s�/
```

显然，编辑或查看编译后的文件几乎是不可能的。这时，Apktool就派上了用场。

```shell
$ apktool d testapp.apk
I: Using Apktool 2.0.0 on testapp.apk
I: Loading resource table...
I: Decoding AndroidManifest.xml with resources...
I: Loading resource table from file: 1.apk
I: Regular manifest package...
I: Decoding file-resources...
I: Decoding values */* XMLs...
I: Baksmaling classes.dex...
I: Copying assets and libs..
```

再次查看`AndroidManifest.xml`，你会看到更加易于理解的内容。

```xml
<?xml version="1.0" encoding="utf-8" standalone="no"?>
<manifest xmlns:android="https://schemas.android.com/apk/res/android" package="brut.apktool.testapp"
          platformBuildVersionCode="21" platformBuildVersionName="APKTOOL" />
```

除了XML文件，还有9patch图片、布局、字符串等资源，它们都被正确解码为原始形式。