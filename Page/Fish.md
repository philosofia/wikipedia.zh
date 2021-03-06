> 本文内容由[Fish](https://zh.wikipedia.org/wiki/Fish)转换而来。


**fish** () 是一个[Unix shell](../Page/Unix_shell.md "wikilink")。fish旨在成为一个比其他shell交互性更强、用户体验更好的shell，并让其丰富的强大功能能够被用户轻松发现、记住并学以致用。fish的语法既不衍生于[Bourne shell也不衍生于](../Page/Bourne_shell.md "wikilink")[C Shell](../Page/C_Shell.md "wikilink")，故被分类为一种“外来”shell。有别于为节约系统资源而默认禁用部分功能的其他shell，fish的全部功能都是默认启用的。

## 特色

fish能根据用户的输入历史与当前所在的目录提供实时的[自动完成](../Page/自动完成.md "wikilink")。与[bash的类似功能](https://zh.wikipedia.org/wiki/bash "wikilink")历史搜索相比，这种不必频繁切换模式还可以用方向键选择建议项的做法使用户能更流畅地进行输入。

fish也拥有功能丰富的Tab补全功能。fish能够自动补全文件路径、变量与不少命令的参数，且支持路径[通配符](../Page/通配符.md "wikilink")与C shell的花括号展开。fish某种意义上会通过分析命令的man文档生成与之相关的补全。

fish倾向于使用命令来代替语法结构。由于命令相比语法结构能更方便地在shell内查到帮助内容，fish的功能很容易在使用过程中被用户自行发现。fish允许[子程序](../Page/子程序.md "wikilink")提供对自己的说明，进一步免去了来回查找帮助的麻烦。fish还允许用户在拥有[图形用户界面](../Page/图形用户界面.md "wikilink")的[浏览器内查看帮助](../Page/网页浏览器.md "wikilink")。

## 语法

fish的语法类似于其他兼容[POSIX的shell](../Page/可移植操作系统接口.md "wikilink")，但由于其开发者认为POSIX shell设计得有问题，fish的语法又与POSIX shell有相当的不同。

``` fish
# 下面演示将"bar"赋给变量foo的过程。
# 由于等号在其他shell中会根据两端是否有空格而表现出不同的行为，
# fish选择了不在赋值中使用这个令人困惑的符号。
# set命令也可以用于数组，并可以轻松设置变量的作用域。
> set foo bar
> echo $foo
bar
```

``` fish
# 下面演示使用命令替换将pwd的输出赋给wd的过程。
# 由于重音符（`）视觉上容易与单引号混淆且左右的符号都相同的话难以嵌套，
# fish改为在命令替换中使用括号。
# 但与ksh不同的是，fish仅在变量展开中使用美元符号。
> set wd (pwd)
> echo $wd
~
```

``` fish
# 将一个有五个元素的数组赋给A。
> set A 3 5 7 9 12
# 将A的第二个和第一个元素赋给B。
# fish的数组索引从1开始。
> set B $A[2 1]
> echo $B
5 3
# 可以用命令替换索引数组中的元素……
> seq 3
1
2
3
> echo $A[(seq 3)]
3 5 7
# ……也可以用其他数组来索引。
# 下面将从A中删除第五个与第三个元素。
> set --erase A[$B]
> echo $A
3 5 9
```

``` fish
# for循环。
> for i in *.jpg
      convert $i (basename $i .jpg).png
  end
# 分号可以代替换行来标记语句的结束：
> for i in *.jpg; convert $i (basename $i .jpg).png; end
# 但由于fish也会在历史记录中分开记录每一行，使用换行一般更加方便。

```

``` fish
# while循环。
# 下面演示输出/etc/passwd中每行的第五个字段。
> cat /etc/passwd | while read line
      set arr (echo $line|tr : \n)
      echo $arr[5]
  end
```

### 没有子shell

其他shell的部分语法结构，例如[管道](../Page/管道_\(Unix\).md "wikilink")、[子程序](../Page/子程序.md "wikilink")与[循环](../Page/迴圈.md "wikilink")，是使用一种称为子shell的方式实现的。所谓子shell即临时执行一个用完即退出的新的子进程。在子shell中执行的修改通常不符合一般人的直觉地，不会反映到真正的shell上（即没有[函数副作用](../Page/函数副作用.md "wikilink")）。fish不依赖于子shell实现其语法结构，故所有内置命令在任何语境下都是会正常运作的。

``` fish
# 相当多的shell会将read在单独的子shell中执行，所以如下语句在他们中无法按预期工作。
# 在常见shell中，bash的管道右边无法产生副作用，故line并不会被赋值；
# ksh中line会被正确赋值，但管道左边的语句无法产生副作用；
# 但是fish和zsh一样，允许管道两边都能有副作用。
> cat *.txt | read line
```

例如，下述bash脚本会因为子shell而导致循环内部给found赋的值在退出循环后即消失

``` bash
found=''
cat /etc/fstab | while read dev mnt rest; do
  if test "$mnt" = "/"; then
    found="$dev"
  fi
done
```

而需要用另一种方式来规避这个问题：

``` bash
found=''
while read dev mnt rest; do
  if test "$mnt" = "/"; then
    found="$dev"
  fi
done < /etc/fstab
```

如下的fish脚本则无需担心子shell会影响副作用。

``` fish
set found ''
cat /etc/fstab | while read dev mnt rest
  if test "$mnt" = "/"
    set found $dev
  end
end
```

## 有用的错误信息

fish会在发生错误时清晰地指出出错的位置并给出修正的方法。

``` fish
> foo=bar
fish: Unknown command “foo=bar”. Did you mean “set VARIABLE VALUE”?
For information on setting variable values, see the help section on
the set command by typing “help set”.
# fish：未知的命令"foo=bar"。你是想输入"set 变量 值"吗？
# 关于如何设置变量的值，请输入"help set"获取set命令的帮助。

> echo ${foo}bar
fish: Did you mean {$VARIABLE}? The '$' character begins a variable
name. A bracket, which directly followed a '$', is not allowed as a
part of a variable name, and variable names may not be zero characters
long. To learn more about variable expansion in fish, type “help
expand-variable”.
# fish：你是想输入{$变量}吗？美元符号"$"仅用于变量名开头，而美元符号后的
# 那个花括号并不能作为变量名称的一部分，且变量也不能没有名称。
# 关于如何展开变量，请输入"help expand-variable"。

> echo $(pwd)
fish: Did you mean (COMMAND)? In fish, the '$' character is only used
for accessing variables. To learn more about command substitution in
fish, type “help expand-command-substitution”.
# fish: 你是想输入(命令)吗？在fish中，美元符号"$"仅用于访问变量。
# 关于如何进行命令替换，请输入"help expand-command-substitution"。
```

## 通用变量

Fish有一个名为通用变量的功能。通过利用通用变量，用户可以在多个同时运行的fish实例之间共享一个变量。即使用户注销或者计算机重启，通用变量的值也不会丢失。

``` fish
# 将emacs设置为默认文本编辑器。
# "--universal"或者"-U"表示设置通用变量。
> set --universal EDITOR emacs

# 如下命令会把fish的提示符中的当前目录变成蓝色。
# 不止执行命令的这个fish，现在所有正在运行的fish的提示符都会发生变化。
> set --universal fish_color_cwd blue
```

## 其它功能

  - 高级tab补全
  - 带完备的错误检查的[语法高亮](../Page/語法突顯.md "wikilink")
  - 支持[X Window系統的](../Page/X_Window系統.md "wikilink")[剪贴板](../Page/剪贴板.md "wikilink")
  - 基于的智能[终端处理](../Page/終端.md "wikilink")
  - 可搜索的

第二版还加入了如下功能：

  - 自动补全
  - 支持256色
  - 基于网页的配置功能
  - 能够提升性能的更多的内置命令

## 參考

## 另请参阅

  - [Unix shell](../Page/Unix_shell.md "wikilink")

  -
## 外部链接

  - [项目主页](http://fishshell.org)

  - [GitHub](../Page/GitHub.md "wikilink")上的[fish](https://github.com/fish-shell/fish-shell)仓库

  - 上的[fish](https://web.archive.org/web/20110726104750/http://gitorious.org/fish-shell/)仓库（不再使用）

  - [SourceForge](../Page/SourceForge.md "wikilink")上的[fish](http://sourceforge.net/projects/fish/)仓库（不再使用）

  - [Fish-users](https://lists.sourceforge.net/lists/listinfo/fish-users) - fish用户的综合讨论列表

  - [bash到fish的命令翻译对照](https://github.com/fish-shell/fish-shell/wiki/Shell-Translation-Dictionary)

[Category:脚本语言](https://zh.wikipedia.org/wiki/Category:脚本语言 "wikilink") [Category:用C編程的自由軟體](https://zh.wikipedia.org/wiki/Category:用C編程的自由軟體 "wikilink")