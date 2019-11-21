---
title: Git多SSH Key配置
date: 2019-10-11 23:48:00
tags: Git
---
在开发过程中我们可能需要配置多个git账户，比如将项目A上传至Github，项目B上传至GitLab，或者是需要配置两个Github账号，不同项目上传至不同的账号下。
# 上传至不同平台
这种情况，无需多个ssh key，只需要在不同的代码托管平台上配置ssh key即可。
# 上传至同一平台的不同账号
由于是同一平台，需要区分账号，且同一平台会出现ssh key冲突的情况，我们需要两个不同的ssh key。那么如何配置呢？
首先，创建两个ssh key, 分别保存在两个不同的文件中，默认文件名为 id_rsa 和 id_rsa.pub 。

``` shell
ssh-keygen -t rsa -C +邮箱地址
```

**场景：假设现在创建了两个 ssh key ,私钥分别保存为 id_rsa 和 test_rsa 文件中。项目A配置的 ssh key为 id_rsa.pub, 项目B配置的ssh key为 test_rsa.pub。**
测试 git 提交代码，执行时发现只有项目A能够提交，而项目B提交失败，提示

```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

这是项目B的ssh key校验失败，因为默认使用的是id_rsa私钥。针对这种情况，我们需要针对不同平台或者项目配置ssh key的验证文件。
这就是第二步，在 ~/.ssh/ 目录下创建config文件，config文件具体配置内容如下：

```
Host myhost（这里是自定义的host简称，相当于下面配置的HostName的别名，用以区分）
    User 登录用户名(如：git)或账号邮箱     (可以不配)
    HostName 主机名可用ip也可以是域名(如:github.com或者bitbucket.org)
    Port 服务器open-ssh端口（默认：22,默认时一般不写此行）
    IdentityFile 私钥文件路径
```

那么针对上面的场景，我们的config文件应该配置如下：

```
Host github1
    HostName github.com
    IdentityFile ~/.ssh/id_rsa

Host github2
    HostName github.com
    IdentityFile ~/.ssh/test_rsa
```

修改对应项目文件夹中.git/config 的相关配置，修改对应的url由原来的`git@github.com:xxx/xxx.git` 修改为 `git@github1:xxx/xxx.git`（这里xxx替换为实际的项目路径），另一项目配置修改类似。
测试执行 git pull , 成功！
