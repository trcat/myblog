---
title: '使用git让本地项目和远程空项目关联'
date: 2020-02-29 11:59:47
copyright: false
header_image: /intro/git_header.png
abstract: 本地文件已经存在，现在要将本地代码存放到远程代码库中。
categories:
- [计算机技术]
tags:
- Git
- 搬运
---

>本文为搬运文章
>
>作者：没有名字愿做一尘埃
>链接：https://www.jianshu.com/p/dc730295e356
>来源：简书
>著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。



1、（先进入项目文件夹）通过命令 git init 把这个目录变成git可以管理的仓库



```kotlin
git init
```

2、把文件添加到版本库中，使用命令 git add .添加到暂存区里面去，不要忘记后面的小数点“.”，意为添加文件夹下的所有文件



```csharp
git add .
```

3、用命令 git commit告诉Git，把文件提交到仓库。引号内为提交说明（linux为单引号；window为双引号）



```ruby
git commit -m 'first commit' || git commit -m "first commit"
```

4、关联到远程库git remote add origin 你的远程库地址，如：



```csharp
git remote add origin https://github.com/cade8800/ionic-demo.git
```

5、获取远程库与本地同步合并（如果远程库不为空必须做这一步，否则后面的提交会失败）



```undefined
git pull --rebase origin master
```

6、把本地库的内容推送到远程，使用 git push命令，实际上是把当前分支master推送到远程。执行此命令后会要求输入用户名、密码，验证通过后即开始上传。



```undefined
git push -u origin master
```


