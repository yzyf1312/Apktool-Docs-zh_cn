# 贡献

### 报告bug

随着混淆工具和Android版本的快速更新，bug堆积如山。当您认为自己遇到了一个bug时，请按照以下步骤操作：

1. 首先搜索是否已存在相同的issue。如果找到了，请留下任何额外的信息评论，或者投上一个+1反应。
2. 如果没有找到相关的issue，请创建一个新的issue，但请务必遵循issue模板。

遵循issue模板非常关键。维护者的时间有限，如果issue格式不当，可能会被关闭。

### 改进文档

任何大型项目都需要良好的文档，Apktool也不例外。文档保持在同一个仓库的[docs](https://github.com/iBotPeaches/Apktool/tree/docs)分支上。因此，欢迎通过pull request来增加这份文档。

在更新文档时，请与其余文档保持风格一致。文档上会运行lint检查，以确保格式正确。

要设置代码库以运行lint检查，请确保安装了node包依赖。为此，请运行以下命令：

```
npm install
```

要运行lint检查，请运行以下命令：

```
npm run lint
```

要修复lint检查发现的大部分问题，请运行以下命令：

```
npm run lint:fix
```

### 响应issue

帮助Apktool的另一种伟大方式是对issue进行分类/回应。这是开始参与项目和帮助其他用户的好方法。

### 修复bug

正如前面提到的，Apktool是开源的，接受pull请求。如果您有bug的修复方案，请提交一个[pull request](https://github.com/iBotPeaches/Apktool/pulls)。

### 建议特性

虽然Apktool的主要焦点一直是修复bug，但总有新特性可以添加。如果您有建议，请在[Ideas](https://github.com/iBotPeaches/Apktool/discussions/categories/ideas)板块创建讨论。