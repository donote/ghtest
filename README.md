# ghtest
Test for github or git cmd

#### github使用

>参考：http://www.runoob.com/w3cnote/git-guide.html

##### 1. 建立shell链接
```
# 生成rsa公钥
ssh-keygen -t rsa -C "github_username@site.com" -f ~/.ssh/id_rsa_github

# copy到粘贴板，下一步粘贴到github上自己账户的SSH-KEY中
pbcopy < ~/.ssh/id_rsa_github.pub

# 如果上面不指定-f 默认文件为id_rsa会被自己加载，如果修改了文件名，需要手动加载
ssh-add ~/.ssh/id_rsa_gpu

# 检验是否加载成功
eval "$(ssh-agent -s)"
ssh-add -l -E md5

# 检验是否可与github连接
ssh -T git@github.com
```

##### 2. 建立新项目
- 在github的主页中「新建项目」ghtest
- 进入项目ghtest，从「Clone or download」复制仓库路径
- 到shell终端下，执行```git clone https://github.com/donote/ghtest.git```  
- 修改README文件，或添加其他文件/文件夹，加入本地仓库，提交到远程仓库

#### 常用git命令

```
# git 命令
# 查看当前所属分支
git branch

# 切换到相应分支liuhui，若没有该分支 则会本地建立
git branch test-br

# 切换到相应的分支test-br
git checkout test-br

# 将本次修改加入待commit
git add filenames

# 撤回上次的修改的
git reset filenames

# 将加入buffer中的文件去掉
git reset HEAD filename

# 增加message信息 commit本次修改，在此之前建议先做git pull
git commit -m "messages ..."

# push到分支，初次会提示增加到origin，之后直接push
# git push --set-upstream origin test-br
git push

# 基本原理：git branch操作只是分支指针的修改，在commit阶段才做内容copy
# pull阶段：从remote branch->origin branch，然后会同步到本地branch
# push阶段：从本地branch同步到remote branch
# fetch阶段：从remote branch->origin branch

# 下载分支代码代码：先clone主干代码，然后checkout到分支，再进行pull
git clone master_code_git
git checkout test-br
git pull

# 删除本地分支
git branch -d test-br

# 暂存之前修改的数据
git stash 

# pull之后再把修改的数据更新回来
git stash pop

# 把主干代码同步到分支，在分支下操作：
git pull origin master

```


#### 其他说明

- bin_py: 存放常用到的一些python用法、函数、小功能封装等
- bin_sh: 存放常用到的一些bash用法、函数、小功能封装等



