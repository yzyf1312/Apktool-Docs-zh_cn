# 安装指南

> **信息**
>
> 运行Apktool至少需要[Java 8](https://www.java.com/en/download/)。请确保您的系统中已经安装了Java 8或更高版本。
>

### Windows系统安装步骤

> **信息**
>
> 由于 Windows 不区分大小写，请[设置区分大小写](https://learn.microsoft.com/en-us/windows/wsl/case-sensitivity)以正确操作。

1. 下载Windows平台的[wrapper脚本](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/windows/apktool.bat)。（右键点击，选择“另存为”，保存为`apktool.bat`）
2. 下载Apktool的[最新版本](https://bitbucket.org/iBotPeaches/apktool/downloads)。
3. 将下载的jar文件重命名为`apktool.jar`。
4. 将`apktool.jar`和`apktool.bat`文件移动到Windows系统的`C:\Windows`。如果您没有权限访问`C:\Windows`，也可以将这两个文件放置在任意位置，并将该目录添加到系统环境变量`PATH`中。
5. 尝试通过命令提示符运行Apktool。

### Linux系统安装步骤

1. 下载Linux平台的[wrapper脚本](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/linux/apktool). (右键点击，选择“另存为”，保存为`apktool`)
2. 下载Apktool的[最新版本](https://bitbucket.org/iBotPeaches/apktool/downloads)。
3. 将下载的jar文件重命名为`apktool.jar`。
4. 将`apktool.jar`和`apktool`脚本移动到`/usr/local/bin`目录。（需要root权限）
5. 确保两个文件都具有执行权限。（使用`chmod +x`命令）
6. 尝试通过命令行界面（CLI）运行Apktool。

### Mac系统安装步骤

1. 下载Mac平台的[wrapper脚本](https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/osx/apktool). (右键点击，选择“另存为”，保存为`apktool`)
2. 下载Apktool的[最新版本](https://bitbucket.org/iBotPeaches/apktool/downloads)。
3. 将下载的jar文件重命名为`apktool.jar`。
4. 将`apktool.jar`和`apktool`脚本移动到`/usr/local/bin`目录。（需要root权限）
5. 确保两个文件都具有执行权限。（使用`chmod +x`命令）
6. 尝试通过命令行界面（CLI）运行Apktool。

### 使用Homebrew安装（Mac系统）

1. 按照[官方网站](https://brew.sh/)上的指示安装Homebrew。
2. 在终端中执行`brew install apktool`命令来安装Apktool。
3. 尝试通过命令行界面（CLI）运行Apktool。

> **TIP**
>
> 虽然wrapper脚本不是必需的，但它们可以使您无需重复输入`java -jar apktool.jar`命令。
