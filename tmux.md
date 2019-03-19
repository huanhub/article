---
title: tmux 使用与配置
date: 2017-06-25 22:02:55
tags: tmux
---



tmux 是一个优秀的终端复用软件, 它能通过一个终端登录远程主机并运行后，在其中可以开启多个控制台的终端复用软件。

<!-- more -->

> 本文在操作环境是在mac上

### 安装
```bash
brew install tmux
```

### 安装插件管理器

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```
然后在 ~/.tmux.conf 文件底部加上

```bash
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com/user/plugin'
# set -g @plugin 'git@bitbucket.com/user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```
如果你已经打开tmux, 需要在重新加载一下配置文件

```bash
tmux source ~/.tmux.conf
```

* 插件管理器的常用命令
```bash
prefix shift-i      # install
prefix shift-u      # update
prefix alt-u        # uninstall plugins not on the plugin list
```

* 安装 tmux-resurrect 插件
```bash
 vim ~/.tmux.conf

# List of plugins
...
set -g @plugin 'tmux-plugins/tmux-resurrect'
...
# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'

```
保存后在执行 `prefix shift-i ` 安装, 在tmux 出现 Done, press ESCAPE to continue. 则代表安装成功

配置 tmux-resurrect

```bash
...
set -g @plugin 'tmux-plugins/tmux-resurrect'

# tmux-resurrect
set -g @resurrect-save-bash-history 'on'
set -g @resurrect-capture-pane-contents 'on'
set -g @resurrect-strategy-vim 'session'
# set -g @resurrect-save 'S'
# set -g @resurrect-restore 'R'
...

```
这样，只要定期 prefix Ctrl-s 就会保存键入的命令历史、Tmux 的面板布局还有 Vim 的状态了。
还原只要 prefix Ctrl-r 即可

* 安装 [tmux-continuum](https://github.com/tmux-plugins/tmux-continuum/blob/master/docs/faq.md) 插件

```bash
 vim ~/.tmux.conf

# List of plugins
...
set -g @plugin 'tmux-plugins/tmux-continuum'
...
# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'

```
配置 tmux-continuum

```bash
# 时间间隔单位分钟, 默认时间为 15 分钟，如果需要可以用以下方式改为 60 分钟，如果想改停止自动保存 则设置为 0 就可以
set -g @continuum-save-interval '60'
```


### session 常用操作

* 创建一个新的session
```bash
tmux new -s <session name>
```

* 进入一个已存在的session
```bash
tmux a -t <session name>
```

* 重命名会话名称
```bash
tmux rename-session -t targetname newname
```

### pane 和 window 常用操作
> 以下命令都需要按一下 tmux 默认设置的prefix 键 `<C-b>`

* pane 操作

|命令|描述|
|---|---|
|`"`| 水平分割窗口|
|`%`| 垂直分割窗口|
|`o`| 跳到下一个分隔窗口|
|`%`| 确认后退出窗口|

* window 操作

|命令|描述|
|---|---|
|`c`| 创建一个新的window|
|`n`|下一个窗口|
|`p`|上一个窗口|



### 配置
> tmux 配置文件是在用户目录下 `~/.tmux.conf`

```bash
vim ~/.tmux.conf
```
