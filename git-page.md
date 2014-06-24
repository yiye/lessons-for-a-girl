#git page

 这篇主要总结一些git的常用命令
 
----------------------------------------------------------
###开始
 在这之前默认自己的电脑是安装好了git。
 首先是一些在使用git之前基本的设置。基本上命令的单词都可以用`TAB`键来进行联想输入。
* 用户名和邮箱

 注意： 这里的邮箱得使用公司公司邮箱。
 
```
 git config --global user.name "HeDao"
 git config --global user.gmail "123@123"
```
* 在github上添加自己电脑的SHH Key

  这样做的好处就是以后提交代码的时候就可以不用每次都输入用户名和密码。
  
  一般来说刚领到的电脑是没有ssh密钥的。如果不放心可以用下边的命令进行检测。
```
 cd ~/.sh
```
 如果没有密钥，则不存在这个文件夹。
 
* 生成密钥的代码

```
 ssh-keygen -t rsa -C "123@123"

```
 其中要求输入的地方都按回车键略过。
 完成后会在目录`~/`生成两个文件`id_rsa`和`id_rsa.pub`。
* 添加公钥

在浏览器中输入gitlib的地址。(如果你没有权限找你的师兄帮你开一下。）进入后点击右上角的Profile settings图标（一个小黑人图标）。在导航栏中找到My SSH keys这个Tab，进入点击 Add SSH Key 。在key 的输入框中将`id_rsa.pub` 内容全部复制到里边，然后点击Add Key。这样就添加好ssh key了
 

完成这些后可以用
```
ssh git@gitlab.alibaba-inc.com

``` 
来进行测试，如果出现欢迎，则说明成功了。

###建立本地仓库
默认情况下远程仓库是已经建立好了的。并且一个团队中有人来管理这些远程仓库。你需要做的就是让管理
把你加入这个仓库。然后克隆这个仓库。
```
git clone git@gitlab.alibaba-inc.com:**/**.git ./your folder name

``` 
git地址可以在gitlab上项目主页的右上角找到。后边文件位置可以不输入

###开发
通过上边的步棸获取到的分支是master。这边规则是不能在master上进行开发。所以在编写代码前得
建议一个新的分支。如果只是你一个人开发话，可以直接在daily上建立分支，如果是和别人一起开发的话
最好先问问分支建立的规则。
```
git branch daily/1.0.0
```
注意：想要发布到daily（也就是测试环境）上，分支名称必须是 daily/1.0.0 这种的格式。

版本号可以用`git branch`和`git tag`来查看哪些版本号已经备用了。

切换到当前分支:
```
git checkout daily/1.0.0
```
建立分支和切换分支可以合成一条命令：
```
git chechout -b daily/1.0.0
```
然后就可以按照需求修改代码....

提交发布代码：

```
git status 
git add -A
git commit -m"123"
git push origin daily/1.0.0

```
这里有条比较重要的规则：只有再build目录下的文件才会被发布到日常环境和正式环境中。所以
最好是将压缩后的js和css，以及必要文件放在build目录。

在日常环境可以通过`http://g.assets.daily.taobao.net /组名/库名/1.0.0/文件名` 文件名是build下文件。

###发布到线上
```
git tag publish/1.0.0
git push origin publish/1.0.0:pushlish/1.0.0
```
线上环境里通过`http://g.tbcdn.cn//组名/库名/1.0.0/文件名`。
这里的daily环境和线上环境里url不同以及版本号的变化，最好是叫开发来进行管理。
###多人开发常用的命令
获取所有人的分支
```
git fetch
```
合并别人的分支（dev-hedao）到自己的分支
```
git merge origin/dev-hedao
```
解决冲突
```
git mergetool
```
一些好用mergertool是需要进行安置和配置。你可以 试试`P4Merge`和`beyond compare`。 

 
 
