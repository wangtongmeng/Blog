# git 三剑客

## 01 | 课程综述

##  02 | 安装 Git

Git 官网： https://git-scm.com

GitHub： https://github.com

GitLab：https://about.gitlab.com

SVN：https://subversion.apache.org

安装 Git： https://git-scm.com/book/zh/v2/起步-安装-Git

确定安装成功：git --version

## 03 | 使用Git之前需要做的最小配置

配置 user 信息

配置 user.name 和 user.email

```shell
git config --global user.name 'your_name'
git config --global user.email 'your_email@domain.com'
```

config 的三个作用域

缺省等同于 local

```shell
git config --local // local 只对某个仓库有效
git config --global //global 对当前用户所有仓库有效
git config --system // system 对系统所有登录的用户有效
```

显示 config  的配置， 加 --list

```shell
git config --list --local
git config --lsit --global
git config --list --system
```
清除设置
```shell
$ git config --unset --local user.name
$ git config --unset --global user.name
$ git config --unset --system user.name
```
## 04 | 创建第一个仓库并配置local用户信息

建 Git 仓库

两种场景：

1.把已有的项目代码纳入 Git 管理

```shell
cd 项目代码所在文件夹
git init
```

2.新建的项目直接用 Git 管理

```shell
cd 某个文件夹
git init your_project #会在当前路径下创建和项目名同名的文件夹
cd your_project
```


