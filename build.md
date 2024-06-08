# 构建Apktool

Apktool是一个包含多个子项目和依赖的项目集合。

- **brut.apktool.lib** - 主库
- **brut.apktool.cli** - CLI接口
- **brut.j.dir** - 工具
- **brut.j.util** - 工具
- **brut.j.common** - 工具

### 要求

- [JDK](https://www.oracle.com/java/technologies/downloads/) > 11
- [git](https://git-scm.com/downloads)
- [Gradle](https://gradle.org/)

### 构建步骤

首先使用以下任一方法克隆仓库：[SSH](ssh://git@github.com:iBotPeaches/Apktool.git) 或 [HTTPS](https://github.com/iBotPeaches/Apktool.git)。

1. 导航至Apktool文件夹，并使用`./gradlew`（Unix系统）或`gradlew.bat`（Windows系统）继续后续步骤。
2. 您可以通过以下两种方式构建项目：

> **信息**
>
> v2.10从Proguard迁移到R8，但暂时保持Proguard的命名。未来会更新。

##### 不使用R8（JDK > 8）

```bash
[./gradlew][gradlew.bat] build shadowJar
```

- 创建jar文件：`brut.apktool/apktool-cli/build/libs/apktool-cli-all.jar`。

##### 使用R8（JDK > 11）

```bash
[./gradlew][gradlew.bat] build shadowJar proguard
```

- 创建jar文件：`brut.apktool/apktool-cli/build/libs/apktool-vXXX.jar`。

##### Windows要求

> **警告**
>
>请注意Windows的目录路径长度限制。

Windows对最大文件路径有一些限制。在Apktool的某个位置，我们有一个218字符的目录路径，这意味着由于Windows的最大255字符限制，我们需要实施一些要求。

这留给我们在Windows上克隆项目的总字符数为37。例如，我可以将该项目克隆到以下位置：

```text
C:/Users/Connor/Desktop/Apktool
```

这是31个字符，可以正确克隆Apktool。而将项目克隆到一个超过37个字符的目录将会出现错误。