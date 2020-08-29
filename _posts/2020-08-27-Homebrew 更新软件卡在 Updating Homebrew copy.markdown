---
layout: post
title:  "Homebrew 长时间停在 Updating Homebrew 这个步骤"
date:   2020-08-27 17:00:00 +0800
categories: homebrew
---
<br>

#### Mac下使用 Homebrew 更新软件时卡在 Updating Homebrew 这个步骤解决方法


在国内环境下使用 Homebrew 安装软件的过程中会长时间卡在 Updating Homebrew 这个步骤

例：执行`➜ ~ brew install composer ` 命令后

```
➜ ~ brew install composer
Updating Homebrew...
```

如果碰到长时间卡在这里，参考以下 2 种解决方法

---
<br>

#### 方法1：按住`control + c` 取消本次更新操作	`>>>`	临时、一次性方式

卡顿时按 `control + c` 命令会显示 `^C`，表示取消 `Updating Homebrew` 操作，大概不到 1 秒钟之后就会去执行我们真正需要的安装操作了

```
➜ ~ brew install composer
Updating Homebrew...
^C==> Downloading https://getcomposer.org/download/1.10.1/composer.phar
######################################################################## 100.0%
🍺  /usr/local/Cellar/composer/1.10.1: 3 files, 1.9MB, built in 2 minutes
...
```

---
<br>

#### 方法2：使用 Alibaba 的 Homebrew 镜像源进行加速	`>>>`	永久的

平时我们执行 brew 命令安装软件的时候，跟以下3个仓库有关系

> 1. brew.git
> 2. homebrew-core.git
> 3. homebrew-bottles

通过以下操作将这 3 个仓库地址全部替换为 Alibaba 提供的地址

1. **替换/还原 brew.git 仓库地址**

   `# 替换成阿里巴巴的 brew.git 仓库地址:`

   `cd "$(brew --repo)"`

   `git remote set-url origin https://mirrors.aliyun.com/homebrew/brew.git`

   ##### # ------------------------------------------------------------------------------------------------------------------------

   `# 还原为官方提供的 brew.git 仓库地址:`

   `cd "$(brew --repo)"`

   `git remote set-url origin https://github.com/Homebrew/brew.git`

2. **替换/还原 homebrew-core.git 仓库地址**

   `# 替换成阿里巴巴的 homebrew-core.git 仓库地址:`

   `cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"`

   `git remote set-url origin https://mirrors.aliyun.com/homebrew/homebrew-core.git`

   ###### # ------------------------------------------------------------------------------------------------------------------------

   `# 还原为官方提供的 homebrew-core.git 仓库地址:`

   `cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"`

   `git remote set-url origin https://github.com/Homebrew/homebrew-core.git`

3. **替换/还原 homebrew-bottles 访问地址**

   这个步骤跟你的 macOS 系统使用的 shell 版本有关系

   所以，先来查看当前使用的 shell 版本

   `echo $SHELL`

   ###### 如果你的输出结果是 `/bin/zsh`，参考?的 zsh 终端操作方式

   ######  如果你的输出结果是 `/bin/bash`，参考?的 bash 终端操作方式

   - **zsh** 终端操作方式

     `# 替换成阿里巴巴的 homebrew-bottles 访问地址:`

     ```echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.zshrc```

     `source ~/.zshrc`

     ###### # ------------------------------------------------------------------------------------------------------------------------

     `# 还原为官方提供的 homebrew-bottles 访问地址:`

     `vi ~/.zshrc`

     `# 然后，删除 HOMEBREW_BOTTLE_DOMAIN 这一行配置`

     `source ~/.zshrc`

   - **bash** 终端操作方式

     `# 替换成阿里巴巴的 homebrew-bottles 访问地址:`

     ```echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.aliyun.com/homebrew/homebrew-bottles' >> ~/.bash_profile```

     `source ~/.bash_profile`

     ###### # ------------------------------------------------------------------------------------------------------------------------

     `# 还原为官方提供的 homebrew-bottles 访问地址:`

     `vi ~/.bash_profile`

     `# 然后，删除 HOMEBREW_BOTTLE_DOMAIN 这一行配置`

     `source ~/.bash_profile`


---
<br>

参考

- [https://www.cnblogs.com/tulintao/p/11134877.html](https://www.cnblogs.com/tulintao/p/11134877.html)
