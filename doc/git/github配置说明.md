# `github`配置说明

##  `git`相关配置

- 如果没有**ssh**密钥, 先生成**ssh**密钥

```
ssh-keygen -t rsa -C "你的gitlab账号对应的邮箱"
```

- 如果已有**ssh**密钥, 则直接使用**ssh**密钥

  

##  github相关配置

- 找到 **.ssh** 文件夹里面的 **.pub** 密钥, 将内容粘贴到 *github* 的 *ssh* 中

  

## 多个邮箱对应密钥相关配置

​	对不同的资源库使用不同的邮箱密钥进行访问

- 继续生成**ssh**密钥, 注意新的密钥文件需要加后缀与之前默认生成的进行区分

```
ssh-keygen -t rsa -C "你的github账号对应的邮箱" -f ~/.ssh/id_rsa_github
```

- 将密钥添加到`SSH agent` 中，为了让**SSH**识别其他私钥

```
ssh-agent bash
ssh-add ~/.ssh/id_rsa_github
```

- 配置*config*文件, 进入`.ssh`目录下，新建一个没有后缀的文件"config"，编辑以下内容进去


```
Host github.com  
    HostName github.com  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/id_rsa_github  

Host gitlab  
    HostName 你的gitlab项目域名 
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/id_rsa
```

  

## 验证配置是否成功

### 1. 从*github*拉取*repository*

完成以上配置后, 以*GitHub*的一个 *repository* 进行`clone`, 验证是否成功

这里以自己的一个*github*库为例进行演示, 打开`git bash`, 输入以下代码

```
git clone git@github.com:chawuNG/learingGit.git
```

若对应的文件被创建, 则证明关联成功

#### 注意:

若进行上述操作时, 命令窗口提示以下内容

```
The authenticity of host 'github.com (192.30.255.112)' can't be established.
Are you sure you want to continue connecting (yes/no)? 
```

输入**yes**，回车即可, 以后不再出现该**waring**



### 2. 将本地存在的代码关联到github的repository

- 获取远程仓库的**ssh**地址

- 输入以下命令, 建立连接桥梁

  ```
  git remote add "桥梁名称"(一般为origin) "ssh地址"
  ```

- 将本地代码推送

  ```
  git push 
  ```

  



