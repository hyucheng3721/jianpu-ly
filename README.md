# jianpu-ly

- [English](README_en.md)

## 简介

jianpu-ly（来自 [Silas S. Brown](http://ssb22.user.srcf.net/mwrhome/jianpu-ly.html) ）是一个 Python 程序（兼容 Python 2 和 Python 3 ），用于在 Lilypond 中打印简谱。当然，你也可以通过 jianpu-ly 同时打印简谱和线谱。

使用 jianpu-ly 需要一些技术知识。如果你不知道什么是命令行，什么是文本编辑器，什么是目录，或者什么是Python，那么请在尝试使用 jianpu-ly 之前了解这些内容。它不是像 Frescobaldi 那样的 Lilypond 前端扩展；它是一个预处理器，需要你有命令行经验。

如果你有问题，可以尝试不同的 Lilypond 版本。jianpu-ly 适用于 Lilypond 2.20、2.22 和 2.24。

## 使用

在命令提示符窗口中运行以下命令，可将文本文件（.txt ）输出为Lilypond文件（.ly ）

`python jianpu-ly.py < 文件名.txt > 文件名.ly` 或 `python jianpu-ly.py 文件名.txt > 文件名.ly`

通过以下命令可以导入 MusicXML，但这是实验性质的，并不适合所有乐曲。

`python jianpu-ly.py piece.xml` 或 `python jianpu-ly.py piece.xml > 文件名.ly`

## 语法

请在文本文件（.txt ）中进行编辑。通常，音符中字符的顺序并不重要，因此 #1 与 1# 相同，'1 与 1' 相同，s1 与 1s 相同。

### 页头指令
标题：`title=标题`

副标题：`subtitle=副标题`

三级标题：`subsubtitle=三级标题`

乐器：`instrument=乐器`

作词人：`poet=作词人`

作曲家：`composer=作曲家`

节拍：`meter=节拍`

编曲家：`arranger=编曲家`

作品：`piece=作品`

作品编号：`opus=作品编号`

<img src="https://github.com/hyucheng3721/jianpu-ly/blob/e891bfc04937f9fb432dc214494593cd47d5820b/%E7%A4%BA%E4%BE%8B/%E7%A4%BA%E4%BE%8B.png" alt="Capture" width="960">

### 常用指令
调号（大调）：`1=Bb`

调号（小调）：`6=Bb`

拍号：`3/4`		`4/4`		`3/4,8`    `6/8,4`（拍号后的数字表示以几分音符的时值弱起）

速度记号：`4=76`

&nbsp;

倍低音：`1,, 2,, 3,, 4,,`

低音：`1, 2, 3, 4,`

中音：`1 2 3 4`

高音：`1' 2' 3' 4'`（高音1、高音2可用按键`8`、按键`9`代替）

倍高音：`1'' 2'' 3'' 4''`

&nbsp;

四分音符：`1 2 3 4` （或`c1 c2 c3 c4`）

八分音符：`q1 q2 q3 q4`（或`1\ 2\ 3\ 4\`）

十六分音符：`s1 s2 s3 s4`（或`1\\ 2\\ 3\\ 4\\`）

三十二分音符：`d1 d2 d3 d4`（或`1\\\ 2\\\ 3\\\ 4\\\`）

六十四分音符：`h1 h2 h3 h4`（或`1\\\\ 2\\\\ 3\\\\ 4\\\\`）

&nbsp;

大附点：`1. q2 3. q4`（或`1. 2\ 3. 4\`）

小附点：`q1. s2 q3. s4`（或`1\. 2\\ 3\. 4\\`）

二分音符：`1 -`

附点二分音符：`1 - -`

全音符：`1 - - -`

&nbsp;

休止符：`0` `q0` `s0` `d0`

&nbsp;

变音记号：`#1` `#2` `b3` `b4`（还原号会根据小节内的音符变化自动添加）

圆滑线：`1 ( 2 ) 3 4`		`5 ( 6 7 1'  )`

延音线：`1 ~ 1 1 1`		`1 - ~ 1 1`

连音：`3[ q1 q2 q3 ] 4 5 6`		`5[ q1 q2 q3 q4 q5 ] 6 7`

延音记号：`1 2 3 4 \fermata`

&nbsp;

段落反复记号：`R{ 1 2 3 4 5 6 7 1' }`

D.C.记号：`1 2 Fine 3 4 5 6 7 1' DC`

D.S.记号：未知****

反复跳跃记号：`R{ 1 2 3 4 } A{ 5 6 7 1' | 7 6 5 4 }`

&nbsp;

力度记号：`1 2 \p 3 4 5 \f 6 7 1'`		`1 \< 2 \! 3 4 1' \> 7 6 5 4 3 2 1 \!`

双小节线（双竖线）：
`1 2 3 4 
LP: \bar "||" 
:LP 
5 6 7 1'`（LP:和:LP必须位于行首）

其它常用小节线符号：`"|."` `".|:"` `":|."` `":|.|:"`（用这些符号代替双小节线中的符号）

&nbsp;

中文歌词：`H: 这是歌词`（有无空格都可）

中文歌词（第1节）：`H: 1. 这是第一节`

中文歌词（第2节）：`H: 2. 这是第二节`

歌词：`L: here are the syl- la- bles`（全部写在一行内，或者:之后换行输入）

歌词（第1节）：`L: 1. Here is verse one`

歌词（第2节）：`L: 2. Here is verse two`

### 其它指令

旧式拍号： `SeparateTimesig 1=C 4/4`

保持不变的时值 （4个十六分音符+1个四分音符）： `KeepLength s1 1 1 1 c1`

间奏：`1 [( 2 3 4 5 6 7 )] 5`

前倚音： `g[#45] 1`

后倚音： `1 ['1]g`

带时值的倚音： `g[d4d5s6] 1`

震音： `1/// - 1///5 -`

简易和弦： `,135' 1 1b3 1`

吉他和弦符号： `chords=c2. g:7 c` （单独一行，或在=之后换行输入）

吉他和弦转为级数和弦：`ChordsRoman`

高低八度记号： `< >`

小节反复： `R4{ 1 2 }`

多小节休止： `R*8`

排练记号： `letterA letterB`

打击乐节拍： `x`

和弦指板图： `frets=guitar` （单独一行）

主音符上的泛音符号： `Harm: (音乐) :Harm` （主音乐）

当前分谱使用的乐器： `instrument=Flute` （单独一行）

二胡指法符号（适用于前一个音符）： `Fr=0 Fr=4`

二胡其它符号（适用于前一个音符）： `souyin harmonic up down bend tilde`

印尼 not angka 风格： `angka`

交替使用印尼风格的二分音符、附点二分音符和全音符： `1 . 1 . . 1 . . .` （点被视为破折号）

&nbsp;

忽略： `% 这是注释`

文本： `^"音符上方" _"音符下方"`

多声部： `NextPart`

多个乐章： `NextScore`

增加五线谱来显示双谱： `WithStaff`

在乐章结束前禁止换页： `OnePage`

禁止为小节编号： `NoBarNums`

禁止首行缩进： `NoIndent`

最后一行不规则对齐： `RaggedLast`

其它 Lilypond 代码： `LP: (代码块) :LP` （每个分隔符必须位于各行行首）

用 Unicode 近似值代替 Lilypond 代码： `Unicode`

按声部导出MIDI文件： `PartMidi`

版权和商标
------------------------

(c) Silas S. Brown，经 Apache 2.0 许可。

Apache 是 Apache 软件基金会的注册商标。Python 是 Python 软件基金会的商标。我无意中提到的任何其他商标均为其各自持有人的商标。
