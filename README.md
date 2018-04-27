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

```


#### 其他说明

- bin_py: 存放常用到的一些python用法、函数、小功能封装等
- bin_sh: 存放常用到的一些bash用法、函数、小功能封装等



