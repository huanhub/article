---
title: bash 常用操作快捷键
date: 2017-06-25 22:16:21
tags: linux
---


本文介绍的是 bash 常用操作快捷键
<!-- more -->

### 用来导航命令行的按键
|命令|全称|描述|
|---|---|---|
|Ctrl + F| 向前一个字符|前进一个字符|
|Ctrl + B| 向后一个字符|后退一个字符|
|Alt + F| 向前一个单词|前进一个单词|
|Alt + B| 向后一个单词|后退一个单词|
|Ctrl + A| 命令行开头|转到当期命令行的开头|
|Ctrl + E| 命令行结尾|转到当前命令行的结尾|
|Ctrl + L| 清除屏幕|清除屏幕，并使光标停留在屏幕顶部|

### 用来编辑命令行的按键
|命令|全称|描述|
|---|---|---|
|Ctrl + D| 删除当前字符|删除单词字符|
|Backspace| 删除前一个字符|删除前一个字符|
|Ctrl + T| 调换字符 |交换当前字符和前一个字符的位置|
|Alt + T| 调换单词|交换当前单词和前一个单词的位置|
|Alt + U| 大写单词|将当前单词改为大写|
|Alt + L| 小写单词|将当前单词改为小写|
|Alt + C| 首字母大写单词|把光标当前位置单词的头一个字母变为大写|
|Ctrl + V| 插入特殊字符|添加一个特殊字符。例如，为了添加字符Tab, 单击Ctrl+V+Tab|

### 用来编辑命令行的按键
|命令|全称|描述|
|---|---|---|
|Ctrl + K| 剪切到行末|剪切光标后面的所有字符|
|Ctrl + U| 剪切到行头|剪切光标前面的所有字符|
|Ctrl + W| 剪切前一个单词 |剪切位于当前光标之后的一个单词|
|Alt + D| 剪切后一个单词 |剪切位于当前光标之前的一个单词|
|Ctrl + Y| 粘贴当前文本|粘贴最近剪切的文本|
|Alt + Y| 粘贴早期文本|转回到早期剪切的文本并粘贴|
|Ctrl + C| 删除整行| 删除整个命令行|

### 命令行重复执行

|命令|全称|例子|
|---|---|---|
|!n| 运行命令行编号|$ !128 |
|!!| 运行前一个命令| $ !! (当命令需要sudo 时，忘记加 sudo ，可以直接 sudo !!)|
|!?string?| 运行包含字符串的命令| $ !?dat?  相当于 date |

### 使用命令历史记录的按键

|按键|功能|描述|
|---|---|---|
|箭头键（上和下）|步骤|单击向上和向下箭头键，遍历历史命令列表中的每一个命令行，直到找到所需的命令行（此外，Ctrl + P和 Ctrl + N 也可以分别完成相同的功能 ）|
|Ctrl + R|反向增量搜索|在按下这些键之后，可以输入一个搜索字符串，完成反向搜索。当输入字符串时，会出现可以运行或者编辑的相匹配的命令行|
|Ctrl + S|向前增量搜索|该功能与上一个功能类似，只不过是向前搜索（并不是在所有情况下都可以使用该功能）|
|Alt + P|反向搜索|在按下这些键之后，可以输入一个搜索字符串，完成反向。输入一个字符串并单击Enter键之后，可以看到包括该字符串的最新命令行|
|Alt + N|向前搜索|该功能与上一个功能类似，只不过是向前搜索（并不是在所有情况下都可以使用该功能）|
