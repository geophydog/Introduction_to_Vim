:hotel: [Return to Home Page](https://github.com/geophydog/geophydog.github.io/blob/master/README.md#welcome-to-geophydogs-self-pages)
# Vim 使用笔记
---
## 目录
* **[Command Mode](#command-mode)**
  * [Cursor Motions](#cursor-motions)
  * [Edit Command](#edit-command)
  * [Window Motion](#window-motion)
* **[Insert Mode](#insert-mode)**
* **[Visual Mode](#visual-mode)**
* **[Search and Replace](#search-and-replace)**
  * [Basic usage](#basic-usage)
  * [Replace](#replace)
  * [Regular Expression](#regular-expression)
  * [Vim 中常用的替换表达式](#vim-中常用的替换表达式)
* **[Ctags and Taglist](#ctags-and-taglist)**
  * [Ctags Configure](#ctags-configure)
  * [为Python标准库添加标签](#pythontag)
  * [为C/C++系统函数添加标签](#systag)
  * [Taglist Configure](#taglist-configure)
  
---
## Command Mode
### Cursor Motions
- `^`: 回到行首
-  `$`: 回到行尾
-  `l`: 向前移动一个单词
-  `w`: 向后移动一个单词
> Note: `w`通常表示一个单词，如`dw`删除一个单词， `yw`复制一个单词，`cw`替换一个单词。

### Edit Command
#### Deletion
- `x`: 删除一个字符
-  `dd`: 删除一行
-  `ndd`: 删除n行
- `dw`: 删除一个单词
-  `D`: 删除至行尾
>  Note: 这里的删除类似于剪切，可以粘贴。

#### Copy and Paste
- `yy`: 复制一行
- `yw`: 复制一个单词
- `p`: 在光标后复制
-  `P`: 在 光标前复制

#### Undo and Redo
- `u`: 撤销
-  `<ctrl>r`: 恢复

### Window Motion
- `<ctrl>f` or `<Page Down>`: 向下翻页
-  `<ctrl>b` or `<Page Up>`: 向上翻页
-  `<ctrl>d`: 下滚（向下翻半页）
-  `<ctrl>u`: 上滚（向上翻半页）
-  `G`: 定位文件最后一行
-  `:n`: 定位到第n行

## Insert Mode
- `a`: 光标后插入
-  `i`: 光标前插入
-  `:r file`: 在当前行之后插入文件内容

## Visual Mode
- `v`: 进入可视模式
-  `V`: 进入可视行模式
-  `<ctrl>v`: 进入可视块模式

## Search and Replace
### Basic usage
1. 在Command Mode 下输入`/xxxx` 后按`<Enter>`可在光标后搜索内容为xxxx的字段。
2. `n`: 跳转下一个字段，`N`: 跳转上一个字段。

### Replace
```
Syntax:[addr]s/源字符串/目的字符串/[option]
```
- `addr`: 表示搜索范围

|  选项  |  功能   |
|-------|:------:|
|`.`| 当前行
|`n`| 第n行
|`$`| 最后一行
|`%`| 全文
|[addr1],[addr2]|: 指定一个范围
> 我们常用的范围有`%`（全文），`n1,n2`（从第n1行到n2行）。

- `option`

|  选项 | 功能  |
|-------|:-----:|
|`g`| 全局替换
|`c`| 替换时进行确认
|`i`| 忽略大小写

### Regular Expression
正则表达式是一种**按一定规则匹配一系列文本**的字符串表达式。
>"正则表达式是烦琐的，但它是强大的，学会之后的应用会让你除了提高效率外，会给你带来绝对的成就感。"

这里推荐一个网站来学习正则表达式：<http://www.runoob.com/regexp/regexp-tutorial.html>
Vim中的搜索和替换同样支持正则表达式。大部分语法与其他正则表达式语法相同，但有一小部分略有区别。这里列出一些规则供参考。

- 元字符

| 模式          | 功能		|	
| ------------- |:-------------:|
|`.`            |匹配任意字符    |
|`[abc]`| 匹配方括号中的任意一个字符，可用-表示字符范围。如`[a-z0-9]`匹配小写字母和数字|
|`[^abc]`| 匹配除方括号中字符之外的任意字符|
|`\d `| 匹配阿拉伯数字，等同于`[0-9]`
|`\D `| 匹配阿拉伯数字之外的任意字符，等同于`[^0-9]`
|`\x` | 匹配十六进制数字，等同于`[0-9A-Fa-f]`
|`\X`| 匹配十六进制数字之外的任意字符，等同于`[^0-9A-Fa-f]`
|`\l`| 匹配`[a-z]`
|`\L`| 匹配`[^a-z]`
|`\u`| 匹配`[A-Z]`
|`\U`| 匹配`[^A-Z]`
|`\w`| 匹配单词字母，等同于`[0-9A-Za-z_]`
|`\W`| 匹配单词字母之外的任意字符，等同于`[^0-9A-Za-z_]`
| `\t`| 匹配`<tab>`字符
|`\s`| 匹配空白字符，等同于`[\t]`
|`\S`| 匹配非空白字符，等同于`[^\t]`

- 普通字符需转意

| 模式          | 功能		|	
| ------------- |:-------------:|
|`\*`| 匹配`*`字符
|`\.`| 匹配`.` 字符
|`\/`| 匹配 `/` 字符
|`\\`|  匹配 `\` 字符
|`\[`| 匹配 `[` 字符
|`\]`| 匹配 `]` 字符

- 表示数量的元字符

| 模式          | 功能		|	
| ------------- |:-------------:|
|`*`| 匹配0-任意个
|`\+`| 匹配1-任意个
|`\?`| 匹配0-1个
|`\{n,m}`| 匹配n-m个
|`\{n}`|   匹配n个
|`\{n,}`|  匹配n-任意个
|`\{,m}`| 匹配0-m个

- 表示位置的元字符

| 模式          | 功能		|	
| ------------- |:-------------:|
|`$`| 匹配行尾
|`^`|  匹配行首
|`\< `| 匹配单词词首
|`\>`| 匹配单词词尾

### Vim 中常用的替换表达式
#### 简单替换表达式
- 替换命令可以在全文中用一个单词替换另一个单词：
```
:%s/four/4/g
```
- 如果你有一个象 "thirtyfour" 这样的单词，上面的命令会出错。这种情况下，这个单词会被替换成"thirty4"。要解决这个问题，用 "\<" 来指定匹配单词开头：
```
:%s/\<four/4/g
```
- 显然，这样在处理 "fourty" 的时候还是会出错。用 "\>" 来解决这个问题：
```
:%s/\<four\>/4/g
```
- 如果你在编码，你可能只想替换注释中的 "four"，而保留代码中的。由于这很难指定，可以在替换命令中加一个 "c" 标记，这样，Vim 会在每次替换前提示你：
```
:%s/\<four\>/4/gc
```

#### 删除多余的空格
- 要删除这些每行后面多余的空格，可以执行如下命令：
`:%s/\s\+$//`
  匹配模式为`\s\+$`，这表示行末（`$`）前的一个或者多个（`\+`）空格（`\s`）。替换命令的部分是空的：`//`。

#### 匹配重复性
- 星号项 `*` 规定在它前面的项可以重复任意次。因此:
```
/a*
```
匹配 "a"，"aa"，"aaa"，等等。但也匹配 "" (空字串)，因为零次也包含在内。星号 `*` 仅仅应用于那个紧邻在它前面的项。因此 `ab*` 匹配 "a"，"ab"，"abb","abbb"，等等。如要多次重复整个字符串，那么该字符串必须被组成一个项。组成一项的方法就是在它前面加 `\(`，后面加 `\)`。因此这个命令:
```
/\(ab\)*
```
匹配: "ab"，"abab"，"ababab"，等等。而且也匹配 ""。
要避免匹配空字串，使用 `\+`。这表示前面一项可以被匹配一次或多次。
```
/ab\+
```
匹配 "ab"，"abb"，"abbb"，等等。它不匹配 后面没有跟随 "b" 的 "a"。

#### 指定重复次数
- 要匹配某一项的特定次数重复，使用 `\{n,m}` 这样的形式。其中 "n" 和 "m" 都是数字。在它前面的那个项将被重复 "n" 到 "m" 次 (包含 "n" 和 "m")。例如:
```
/ab\{3,5}
```
匹配 "abbb"，"abbbb" 以及 "abbbbb"。
当 "n" 省略时，被默认为零。当 "m" 省略时，被默认为无限大。当 ",m" 省略时，就表示重复正好 "n" 次。例如:

| 模式          | 匹配次数		|	
| ------------- |:-------------:|
| `\{,4}`      |  0，1，2，3 或 4 | 
| `\{3,}`       | 3，4，5，等等   |  
|   `\{0,1}`      |   0 或 1      |
|  `\{0,}`     |    0 或 更多，同 *
|`\{1,}`      |    1 或 更多，同 \+
|    `\{3}`       |    3


#### 多选一匹配
- 在一个查找模式中，"或" 运算符是 `\\|`。例如:
```
/foo\|bar
```
这个命令匹配了 `foo` 或 `bar`。更多的抉择可以连在后面:
```
/one\|two\|three
```
匹配 `one`，`two` 或 `three`。
如要匹配其多次重复，那么整个抉择结构须置于 `\(` 和 `\)` 之间:
```
/\(foo\|bar\)\+
```
这个命令匹配 `foo`，`foobar`，`foofoo`，`barfoobar`，等等。

#### 变量替换
- 置于 `\(` 和 `\)` 之间的字符串可以作为变量在替换是引用，例如`xxxx this is that xxxx`，我们想将这段文本中的`this`和`that`进行换位变成`xxxx that is this xxxx`，Vim的替换命令应该这样写：
```
:.s/\(this\) is \(that\)/\2 is \1/
```
其中`\1`表示`this`，`\2`表示`that`。


## Ctags and Taglist
Ctags可以定义项目目录下的文件所包含的结构体、函数类型、变量类型、函数名所在位置，并可以他们之间跳转。
### Ctags Configure
1. 在项目目录下生成tags文件，文件记录了函数、变量等的位置和类型。
```
cd /path/to/project
ctags -R *
```
2. 在`~/.vimrc`中设置
```
set tags=tags
```
3. 打开项目中的文件
- `<ctrl>]`: 进入光标所指的标识符的定义
- `<ctrl>t`: 回到前一个标签处

<h1 id="pythontag"></h1>

### 为Python标准库添加标签
1. 假设Python标准库的位置是`/usr/lib/python3.6`
```
ctags -R -f ~/.python.tags /usr/lib/python3.6
```
2. 在`~/.vimrc`中添加设置
```
set tags+=~/.python.tags
```

<h2 id="systag"></h2>

### 为C/C++系统函数添加标签
1. 设置系统头文件标签
```
ctags -R -f ~/.sys.tags /usr/include /usr/local/include
```
2. 在`~/.vimrc`中添加设置
```
set tags+=~/.sys.tags
```

### Taglist Configure
1. 安装Taglist，在[Taglist](http://vim-taglist.sourceforge.net/)官网下载插件，并解压到`~/.vim/`目录中，保证该目录下存在：
```
plugin/taglist.vim
doc/taglist.txt
```
2. 打开项目中的文件，在Command Mode下输入
```
:Tilst
```
3. Taglist中常用快捷键

|   命令    |   功能   |
|----------|:---------:|
|   `<ctrl>ww` |在文本窗口和Taglist窗口间切换
| `o` |在一个新打开的窗口中显示光标下tag
| `s` |更改排序方式，在按名字排序和按出现顺序排序间切换
| `+` |打开一个折叠，同zo
| `-` |将tag折叠起来，同zc
| `*` |打开所有的折叠，同zR
|`=`  |将所有tag折叠起来，同zM
|`[[` | 跳到前一个文件
|`]]` | 跳到后一个文件
|`q`  |关闭taglist窗口
