

# Unit1:基础配置

## chapter1:用户名及邮箱配置

```bash
git config --global user.name "username"
git config --global user.email "happy@email.com"
```

## chapter2:仅推动当前分支

```shell
git config --global push.default simple
```

注：要求 Git 版本 1.9.5 以上

## chapter3:解决windows下git信息显示乱码的情况

### section1:让git不要管Winsows/Unix换行符转换的事

```shell
git config --global core.autocrlf false
```

### section2:git提示信息中文显示正常

```
git config --global core.quotepath false
```

## chapter4:终端zsh中的特殊配置

zsh 为 Git 提供了一个 Tab 补全库。 想要使用它，只需在你的 `.zshrc` 中执行 `autoload -Uz compinit && compinit` 即可。



# Unit2:git推代码至远端

忽略文件配置一览，可直接用 https://github.com/github/gitignore

## chapter1:生成公钥密钥

```shell
ssh-keygen -t rsa -C "happy@email.com"		          # 查看pub配置github
```

## chapter2:新仓库将代码推至GitHub

```shell
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/zyb-prj/test.git
git push -u origin main
```

## chapter3:已经存在的仓库将代码推至GitHub

```shell
git remote add origin https://github.com/zyb-prj/test.git
git branch -M main
git push -u origin main
```

## chapter4:解决推代码时重复输入账号密码的问题

在推代码至远程分支前，运行以下命令配置Git使用钥匙串访问管理器。

```shell
git config --global credential.helper osxkeychain
```

