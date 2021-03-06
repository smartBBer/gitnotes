# .gitignore文件说明

###### 一、简绍

我们做的每个Git项目中都需要一个“.gitignore”文件，这个文件的作用就是告诉Git哪些文件不需要添加到版本管理中。比如我们项目中的npm包(node\_modules)，它在我们项目中是很重要的，但是它占的内存也是很大的，所以一般我们用Git管理的时候是不需要添加npm包的。

###### 二、常用的规则

```swift
/mtk/ 过滤整个文件夹
*.zip 过滤所有.zip文件
/mtk/do.c 过滤某个具体文件
```

以上规则意思是：被过滤掉的文件就不会出现在你的GitHub库中了，当然本地库中还有，只是push的时候不会上传。  
除了以上规则，它还可以指定要将哪些文件添加到版本管理中。

```swift
!src/   不过滤该文件夹
!*.zip   不过滤所有.zip文件
!/mtk/do.c 不过滤该文件
```

**1、配置语法：**  
以斜杠`/`开头表示目录；  
以星号`*`通配多个字符；  
以问号`?`通配单个字符  
以方括号`[]`包含单个字符的匹配列表；  
以叹号`!`表示不忽略(跟踪)匹配到的文件或目录；

此外，git 对于 .ignore 配置文件是按行从上到下进行规则匹配的，意味着如果前面的规则匹配的范围更大，则后面的规则将不会生效；

**2、示例说明**  
**a、规则：fd1/**\*  
说明：忽略目录 fd1 下的全部内容；注意，不管是根目录下的 /fd1/ 目录，还是某个子目录 /child/fd1/ 目录，都会被忽略；  
**b、规则：/fd1/**\*  
说明：忽略根目录下的 /fd1/ 目录的全部内容；  
**c、规则：**  
/\*  
!.gitignore  
!/fw/bin/  
!/fw/sf/  
说明：忽略全部内容，但是不忽略 .gitignore 文件、根目录下的 /fw/bin/ 和 /fw/sf/ 目录；

###### 3、创建.gitignore文件

**1) 常规的windows操作**

- 根目录下创建gitignore.txt；
- 编辑gitignore.txt，写下你的规则，例如加上node\_modules/；
- 打开命令行窗口，切换到根目录（可以直接在文件夹上面的地址栏输入cmd回车）；
- 执行命令ren gitignore.txt .gitignore。

**2) 用Git Bash**

- 根目录下右键选择“Git Bash Here”进入bash命令窗口；
- 输入`vim .gitignore`或`touch .gitignore`命令，打开文件（没有文件会自动创建）；
- 按i键切换到编辑状态，输入规则，例如node\_modules/，然后按Esc键退出编辑，输入:wq保存退出。

如图：

```cpp
# dependencies  npm包文件
/node_modules

# production  打包文件
/build

# misc 
.DS_Store

npm-debug.log*
```

**.DS\_Store：**这个文件是Mac OS X用来存储文件夹的一些诸如自定义图标，ICON位置尺寸，窗口位置，显示列表种类以及一些像窗体自定义背景样式，颜色这样的元信息。默认情况下，Mac OS X下的每个文件夹下应该都会生成一个，包括网络介质存储盘和U盘这样的外部设备。  

![](https://gitee.com/tooyi/picbox/raw/master/img/4434233-0157f5244c8cb047.png)



**npm-debug.log：**项目主目录下总是会出现这个文件，而且不止一个，原因是npm i 的时候，如果报错，就会增加一个此文件来显示报错信息，npm install的时候则不会出现。

最后需要强调的一点是，如果你不慎在创建.gitignore文件之前就push了项目，那么即使你在.gitignore文件中写入新的过滤规则，这些规则也不会起作用，Git仍然会对所有文件进行版本管理。  
简单来说，出现这种问题的原因就是Git已经开始管理这些文件了，所以你无法再通过过滤规则过滤它们。因此一定要养成在项目开始就创建.gitignore文件的习惯，否则一旦push，处理起来会非常麻烦。



## 若已提交的内容需要处理

1. 暂存区移除已提交的内容

`git rm --cached 文件名` 会把文件从暂存区删除，工作区仍存在

2. .gitignore文件中添加忽略项

`git commit -m 'delete remote somefile'`

3. 提交远程

`git push`

### git rm与git rm --cached

#### 当我们需要删除暂存区或分支上的文件, 同时工作区也不需要这个文件了, 可以使用

1. git rm file_path
2. git commit -m 'delete somefile'
3. git push

#### 当我们需要删除暂存区或分支上的文件, 但本地又需要使用, 只是不希望这个文件被版本控制, 可以使用

1. git rm --cached file_path
2. git commit -m 'delete remote somefile'
3. git push
