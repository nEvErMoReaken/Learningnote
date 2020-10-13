# 10.13

遇到问题，想把以前毕设做的文本摘要项目上传到Github上就当练习git使用了，在上传文件中有一个模型大小约为120MB左右，导致了上传失败。

一番搜索后才知道github上传文件大小的最大为100MB，可是所有的文件已经add后commit到电脑的暂存区了，这该怎么办？

```shell
$ git ls-files
//查看暂存区的文件
$ git rm --cache 文件名
//从暂存区删除该文件
$ git reset HEAD -- file；
//清空add命令向暂存区提交的关于file文件的修改（Ustage）；这个命令仅改变暂存区，并不改变工作区，这意味着在无任何其他操作的情况下，工作区中的实际文件同该命令运行之前无任何改变
```

以上三行命令解决此问题。

另外将几个常用命令贴在这里：

```shell
$ git remote add origin git@xxx
//连接远程仓库
$ git clone git@xxx
//克隆
```

### 同步删除文件：

```shell
$ git rm --f test.md
$ git commit test.md -m '描述内容随便写'
$ git pull
$ git push
$ git status -s //精简版
```

### 同步删除文件夹：

删除前目录状态

![1](E:\Github\Learningnote\img\1.jpg)



![2](E:\Github\Learningnote\img\2.png)

```shell
$ rm -rf img project test text 
$ git commit -m '删除了文件夹 img project test text'
$ git pull
$ git push
$ git status -s
```

