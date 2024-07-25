# 雾凇拼音加搜狗词库 + 双辅自然码 + CJK-E郑码 + CJK-I虎码

【TLDR】

将自己常用的输入法放到一套 rime 配置里。

在 MacOS 安装好鼠须管，备份并清空 ~/Library/Rime，将本仓库内容复制到该路径下，重新部署即可。其他平台，基本类似。

## 雾凇拼音

[雾凇拼音](https://dvel.me/posts/rime-ice/) 提供了一套开箱即用的 Rime 完整配置，包含了输入方案（全拼、双拼）、长期维护的词库及各项扩展功能。

[雾凇拼音github](https://github.com/iDvel/rime-ice/)

- **拆字辅码**：输完拼音，` ，接着是汉字部件的音作为拆字辅码（**注意：与自然码辅码 不同**），减少重码。（注：通过[汉字部件拆字](https://github.com/mirtlecn/rime-radical-pinyin)实现）

- **拆字组字**：uU 开头，接各部件的音，常用于输多个常见字作为部件所组成的难字。(反查时前缀会消失，影响打英文，所以设定为两个字母，或可改成一个非字母符号)

- **以词定字**：两个中括号 [ ]，取首字、尾字。

- 符号：双拼大写 V 开头，全拼 v 开头。symbols_caps_v.yaml 和 symbols_v.yaml 里的各种符号。

- 数字和金额大写：大写 R 开头，如 R1234 得到「一千二百三十四、壹仟贰佰叁拾肆元整」。

- 日期时间：双拼为 date time week datetime timestamp，全拼为 rq sj xq dt ts。

- 农历指定日期：大写 N 开头，如 N20240210 得到「二〇二四年正月初一」。

- 农历：双拼 lunar，全拼 nl。

- Unicode：大写 U 开头，如 U62fc 得到「拼」。

- 在拼音中前后移动：Tab 或 Shift + Tab

- 删除自造词，或降低词库中已有词语的权重（回到原始权重，不是降到最低）：鼠须管 Fn + ⇧ + ⌫，小狼毫 Ctrl/Shift + Del。想永久删除一个词库中存在的词汇，只能编辑词库，重新部署。

## 搜狗细胞词库

[搜狗标准词库](https://pinyin.sogou.com/dict/detail/index/11640) （只是名字叫这个，可能不是搜狗官方词库？）

[搜狗细胞词库的其他词库](https://pinyin.sogou.com/dict/) （选了些诗词、名句、地名、明星、网络热词）

在雾凇的词库基础上，补充了一些诗词、地名等搜狗词库后，去重，总共约 220 万拼音、双拼共用的字词。

## 单字减少重码的方法

雾凇里整合了“部件拆字”、“以词定字”的功能，以减少同音字的重码和翻页。

此外，在 custom_phrase_double.txt 里添加了近 7000 常用字（带自然码的单辅码）的编码。

输入同音的单字减少重码减少翻页的方法：

第一种：自然单辅（声韵双拼后多打一键，或许就能看到所要的字）。这是依赖自定义短语，只有常用字。

举例：

```
mu的同音字很多，

mud = 沐（d为氵），

muj = 幕（j为巾），

mun = 牡（n为牛）。
```

第二种：以词定字（打词后用左右中括号[或]定字）、拆字辅码（打难字，在双拼后，加`，部件的辅码）、拆字组字（打难字时，uU+各部件双拼）等。

举例：

```
(1) 以词定字: 双拼 mzgv 是玫瑰，mzgv[ 则是玫，mzgv] 则是瑰。

(2) 拆字辅码：

mu`uv = 沐（uv = 三点水的双拼），

mu`mojn = 幕（mo = 莫，jn = 巾，通常 jn 不用输，就看到所需的字了），

mu`nqtu = 牡（nq = 牛，tu = 土，通常 nqtu 也不必全输完，就看到所需的字了）。

(3) 拆字组字：

uUmojn 幕（mo = 莫，jn = 巾）

uUnqtu 牡（nq = 牛，tu = 土）
```

【注】

拆字部件作为辅码，如果感觉不顺手，可由 "双拼" 切换到 “双拼2”，后者是将拆字辅码方案，改为自然码辅码方案。

通过这个[辅助码的音形分离插件](https://github.com/HowcanoeWang/rime-lua-aux-code) 来实现的

第三种：切换到自然码，用双辅（但自然码词库小一些）。

详见下面的”双辅自然码“。

第四种：若面对的不是常用单字，或者大量不知读音的单字，只能用形码（比如：郑码、仓颉、五笔，或受它们影响而诞生的各种像虎码、徐码、宇浩、......等等这样的方案）。


## 双辅自然码

1. [自然码2000官网](http://ziranma.com.cn/uiysuomy.htm)

2. [自然码双拼和辅码参考pdf](https://github.com/impishian/input_method/blob/main/%E5%8F%8C%E6%8B%BC_%E8%87%AA%E7%84%B6%E7%A0%81%E6%96%B9%E6%A1%88/zrm.pdf) 

   pdf说明：
```
(1) 自然码辅码，均为声母。只要会念，就会了。

(2) 括号里的蓝色字：形近归并的项。

(3) 红色字：难念的项，特别标出了拼音，以便理解记忆。
```

3. 再次提醒注意：**自然码辅码**，与雾凇整合的 **拆字辅码**，是不同的。二者均是减少重码的好手段。

4. [mutoe](https://github.com/mutoe/rime) 或 [henices](https://github.com/henices/rime) 的码表
  
   采用 zrm2000.dict.yaml 和 zrm2000.schema.yaml 两个文件。统计码表，去掉编码，只留字词，再去重，最后约 18 万字词。

5. 自然码辅码

  - 举例

```
mud = 沐 (d = 氵)
或
mudm = 沐 (d = 氵, m = 木)

mucj = 幕 (c = 艹, j = 巾) 
或
muj = 幕 ( j = 巾)

mun = 牡（n = 牛）
或
munt = 牡（n = 牛，t = 土）
```

  - 用 ,, 查询辅码
  
```
声+韵+,,+形1+形2

比如：查询"栋"的辅码，只需在声韵双拼之后加两个逗号，即：ds,,
即可看到多个 dong 字的辅码。下次直接输入 dsmd 即得到"栋"。
```

  - 用 .. 切形输入

```
形1声+形1韵+..+形2声+形2韵。

类似前面提到的 “拆字组字”，用于输入多个常用字组成的难字。

比如：查询"岶"的编码，只需分别输入"山"和"白"的双拼编码、中间用 ".." 连接，
即输入：uj..bl (shan..bai)，便可查到该字的编码 poub。
```

## CJK-E 郑码

采用了 [不知郑码](https://github.com/GongMu/rime-zhengma.git)  的 bzzm.*.yaml 等文件。

提取 [郑码（来自Rime作者佛振）](https://github.com/lotem/rime-zhengma.git) 的 CJK-E 字，补充到不知郑码中。

约 18 万字词。

## CJK-I 虎码

[虎码资源下载](http://huma.ysepan.com)

采用了[虎码](https://tiger-code.com) 官方单字 tiger.dict.yaml, tiger.schema.yaml ，适当简化配置，仅用于打单。

tiger.dict.yaml.orig 是官方原始单字码表，tiger.dict.yaml 移除一些部首和笔画等影响正常选字的编码。

完全支持 CJK to CJK-I 所有单字，近10万。

## 搜狗词库转 Rime 格式工具

[scel2txt](https://github.com/lewangdev/scel2txt)

# 文件列表

```
不知郑码：

├── bzzm.dict.yaml（修改，增加3行）
├── bzzm.phrases.dict.yaml
├── bzzm.phrases1.dict.yaml
├── bzzm.schema.yaml (schema name 改为 郑码)
├── bzzm.symbols.dict.yaml
├── bzzm.words.dict.yaml
├── bzzm.words1.dict.yaml（新增）

雾凇拼音：

├── cn_dicts
│   ├── 41448.dict.yaml
│   ├── 8105.dict.yaml
│   ├── base.dict.yaml
│   ├── ext.dict.yaml
│   ├── others.dict.yaml
│   ├── sogou_biaozhun.dict.yaml （新增）
│   ├── sogou_chengyu_poem_people_shenzhen.dict.yaml (新增)
│   ├── sogou_network_pop_new_words.dict.yaml（新增）
│   └── tencent.dict.yaml
├── custom_phrase.txt
├── custom_phrase_double.txt（新增，自然码双拼单辅的近7000常用单字）
├── default.yaml（修改schema_list、page_size，增加一个switcher的hotkey，启用，.翻页）
├── double_pinyin.schema.yaml（修改 schema name ，由“自然码双拼”改为“双拼”。删除其他双拼方案的schema.yaml文件）
├── en_dicts
│   ├── cn_en.txt
│   ├── cn_en_double_pinyin.txt（只留下自然码双拼，删除其他双拼方案的txt文件）
│   ├── en.dict.yaml
│   └── en_ext.dict.yaml
├── lua
│   ├── autocap_filter.lua
│   ├── cn_en_spacer.lua
│   ├── cold_word_drop
│   │   ├── drop_words.lua
│   │   ├── filter.lua
│   │   ├── hide_words.lua
│   │   ├── logger.lua
│   │   ├── metatable.lua
│   │   ├── processor.lua
│   │   ├── reduce_freq_words.lua
│   │   └── string.lua
│   ├── corrector.lua
│   ├── date_translator.lua
│   ├── en_spacer.lua
│   ├── is_in_user_dict.lua
│   ├── long_word_filter.lua
│   ├── lunar.lua
│   ├── number_translator.lua
│   ├── pin_cand_filter.lua
│   ├── reduce_english_filter.lua
│   ├── search.lua
│   ├── select_character.lua
│   ├── t9_preedit.lua
│   ├── unicode.lua
│   └── v_filter.lua
├── melt_eng.dict.yaml
├── melt_eng.schema.yaml（修改speller的algebra，由全拼改为自然码双拼。删除5行其他双拼）
├── opencc
│   ├── emoji.json
│   ├── emoji.txt
│   └── others.txt
├── others
│   ├── CHANGELOG.md
│   ├── Hamster
│   │   ├── README.md
│   │   └── melt_eng.custom.yaml
│   ├── cn_en.txt
│   ├── demo.webp
│   ├── emoji-map.txt
│   ├── iRime
│   │   ├── README.md
│   │   ├── iRime 九宫格
│   │   │   ├── melt_eng.custom.yaml
│   │   │   └── rime_ice.custom.yaml
│   │   └── iRime 全键盘
│   │       ├── rime_ice.custom.yaml
│   │       └── theme
│   │           └── iPhone_custom
│   │               ├── info.yaml
│   │               └── port
│   │                   └── theme.yaml
│   ├── recipes
│   │   ├── all_dicts.recipe.yaml
│   │   ├── cn_dicts.recipe.yaml
│   │   ├── config.recipe.yaml
│   │   ├── en_dicts.recipe.yaml
│   │   ├── full.recipe.yaml（删除其他双拼方案的5行）
│   │   └── opencc.recipe.yaml
│   └── sponsor.webp
├── pinyin_simp.dict.yam  l（袖珍简化字拼音，源自 Android 拼音。bzzm 依赖它）
├── pinyin_simp.schema.yaml（袖珍简化字拼音，源自 Android 拼音。bzzm 依赖它）
├── radical_pinyin.dict.yaml
├── radical_pinyin.schema.yaml（修改speller的algebra，由全拼改为自然码双拼。删除5行其他双拼）
├── rime.lua
├── rime_ice.dict.yaml（启用41448大字表；增加搜狗标准词库、搜狗网络新词词库、其他常用的搜狗细胞词库）
├── rime_ice.schema.yaml（schema name 由雾凇拼音改为拼音）
├── squirrel.yaml（增加roseo_maple皮肤，作为自用首选皮肤；增加 candidate_list_layout: linear）
├── symbols_caps_v.yaml
├── symbols_v.yaml
├── t9.schema.yaml
├── weasel.yaml

自然码

├── zrm2000.dict.yaml
├── zrm2000.schema.yaml

虎码

├── tiger.dict.yaml  (官方单字码表，移除一些部首、笔画等)
├── tiger.dict.yaml.orig (官方单字码表)
├── tiger.schema.yaml (官方 schema 适当简化，减少依赖等)
```

## 提取词库的一些命令行

```
#1.汇总现有词库
#cat base.dict.yaml 8105.dict.yaml 41448.dict.yaml ext.dict.yaml others.dict.yaml tencent.dict.yaml > ice.txt

#2.去掉注释行
#ugrep -v "^#" ice.txt > ice1.txt

#3.只取有中文的行
#ugrep '[\x{4E00}-\x{9FFF}\x{3400}-\x{4DFF}\x{20000}-\x{2A6DD}\x{9FA6}-\x{9FBB}\x{FA70}-\x{FAD9}\x{9FBC}-\x{9FC3}\x{2A700}-\x{2B734}\x{2B740}-\x{2B81D}\x{2B820}-\x{2CEAF}\x{9FCD}-\x{9FD5}\x{2CEB0}-\x{2EBEF}\x{30000}-\x{3134A}\x{31350}-\x{323AF}\x{2EBF0}-\x{2EE5F}\x{3007}]' ice1.txt > ice2.txt

#4.去掉编码
#sd "\t.*$" "" ice2.txt

#5.找出那些在 sogou_network_pop_new_words.txt 但不在 ice2.txt 的行:
#python3 scel2txt.py  ./网络流行新词【官方推荐】.scel  ./sogou_network_pop_new_words.txt
#awk 'NR==FNR {lines[$0]; next} !($0 in lines)' ice2.txt  sogou_network_pop_new_words.txt  > sogou_network_pop_new_words.dict.yaml

#6.人工整理 新的 dict.yaml，在前面加些行。
#...

#7.提取 CJK-E 字
ugrep '[\x{2B820}-\x{2CEAF}]' zhengma.dict.yaml |wc -l
5815
#可以导入5815个字到bzzm
```

## CJK 和 Unicode

[支持大字集的字体](https://zh.wikipedia.org/wiki/Wikipedia:Unicode%E6%89%A9%E5%B1%95%E6%B1%89%E5%AD%97)

[CJK](https://zh.wikipedia.org/wiki/%E4%B8%AD%E6%97%A5%E9%9F%93%E7%B5%B1%E4%B8%80%E8%A1%A8%E6%84%8F%E6%96%87%E5%AD%97)

[通用规范汉字表](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E8%A7%84%E8%8C%83%E6%B1%89%E5%AD%97%E8%A1%A8)

为覆盖到《通用规范汉字表》的字，字体和输入法至少应支持到 CJK-E

## 从 CJK, CJK-A 到 CJK-I

1.根据 CJK wikipedia 词条正文的表格，整理如下：

| CJK  | 对应的 Unicode 版本   | 时间   |  备注  |
|------------|------------|------------|------------|
| CJK | 1.0, 1.1 | 1993-1998 | 20915字 |
| CJK-A | 3.0 | 1999 |  6582字 |
| CJK-B | 3.1 | 2001 | 42711字 （4.1: 22字，5.1: 8字）|
| CJK-C | 5.2 | 2009 | 4149字 + 8字 |
| CJK-D | 6.0 | 2010 | 222字 + 1字 |
| CJK-E | 8.0 | 2015-06-17 |  5762字+9字 |
| CJK-F | 10.0 | 2017-06-20 | 7473字+21  (11.0: 5字) |
| CJK-G | 13.0 | 2020-03 | 4939字 +23字+7字  （14.0: 3+2+4字）|
| CJK-H | 15.0 | 2022-09 | 4192字 + 1字 |
| CJK-I | 15.1 | 2023-09 | 622字。|

截至 CJK-E，共有 `8万余` CJK 字。

截至 CJK-I，共有 `97681` CJK 字，加上非 CJK 的，共有约 `15万`

2.根据 CJK wikipedia 词条最后的表格里的“编码范围”，整理如下：

已统一：

|       | 编码范围 | 已使用 |
|-------|----------|--------|
| CJK   | 4E00-9FFF   | 20992 | 
| CJK-A | 3400-4DBF   | 6592  |
| CJK-B | 20000-2A6DF | 42720 |
| CJK-C | 2A700-2B73F | 4154  |
| CJK-D | 2B740-2B81F | 222   |
| CJK-E | 2B820-2CEAF | 5762  |
| CJK-F | 2CEB0-2EBEF | 7473  |
| CJK-G | 30000-3134F | 4939  |
| CJK-H | 31350-323AF | 4192  |
| CJK-I | 2EBF0-2EE5F | 622   |
| 总计  |                               | 97668 |

```
ugrep '[\x{4E00}-\x{9FFF}]'
ugrep '[\x{3400}-\x{4DBF}]'
ugrep '[\x{20000}-\x{2A6DF}]'
ugrep '[\x{2A700}-\x{2B73F}]'
ugrep '[\x{2B740}-\x{2B81F}]'
ugrep '[\x{2B820}-\x{2CEAF}]'
ugrep '[\x{2CEB0}-\x{2EBEF}]'
ugrep '[\x{30000}-\x{3134F}]'
ugrep '[\x{31350}-\x{323AF}]'
ugrep '[\x{2EBF0}-\x{2EE5F}]'

ugrep '[\x{4E00}-\x{9FFF}\x{3400}-\x{4DBF}\x{20000}-\x{2A6DF}\x{2A700}-\x{2B73F}\x{2B740}-\x{2B81F}\x{2B820}-\x{2CEAF}\x{2CEB0}-\x{2EBEF}\x{30000}-\x{3134F}\x{31350}-\x{323AF}\x{2EBF0}-\x{2EE5F}]' ...
```

未统一：

|       | 编码范围 | 已使用 |
|-------|----------|--------|
| 汉字部首补充       | 2E80-2EFF | 115 | 
| 康熙部首           | 2F00-2FDF | 214  |
| 表意文字描述字符   | 2FF0-2FFF | 12 |
| 符号和标点         | 3000-303F | 64  |
| 笔画               | 31C0-31EF | 36   |
| 带圈字符及月份     | 3200-32FF | 255  |
| 兼容字符           | 3300-33FF | 256  |
| 兼容表意文字       | F900-FAFF | 472  |
| 兼容形式           | FE30-FE4F | 32  |
| 带圈表意文字补充   | 1F200-1F2FF | 64   |
| 兼容表意文字补充   | 2F800-2FA1F | 542 |
| 总计  |        | 2062 |

```
ugrep '[\x{2E80}-\x{2EFF}]' 
ugrep '[\x{2F00}-\x{2FDF}]' 
ugrep '[\x{2FF0}-\x{2FFF}]' 
ugrep '[\x{3000}-\x{303F}]' 
ugrep '[\x{31C0}-\x{31EF}]' 
ugrep '[\x{3200}-\x{32FF}]' 
ugrep '[\x{3300}-\x{33FF}]' 
ugrep '[\x{F900}-\x{FAFF}]' 
ugrep '[\x{FE30}-\x{FE4F}]' 
ugrep '[\x{1F200}-\x{1F2FF}]' 
ugrep '[\x{2F800}-\x{2FA1F}]' 

ugrep '[\x{2E80}-\x{2EFF}\x{2F00}-\x{2FDF}\x{2FF0}-\x{2FFF}\x{3000}-\x{303F}\x{31C0}-\x{31EF}\x{3200}-\x{32FF}\x{3300}-\x{33FF}\x{F900}-\x{FAFF}\x{FE30}-\x{FE4F}\x{1F200}-\x{1F2FF}\x{2F800}-\x{2FA1F}]' ...
```

## 其他

在此提一下一位打字冠军。某音号：`打字快的州州`，她主要用：搜狗输入法 + 自然码双拼 + 独家词库 + 独家辅码。尽量整句输入。独家辅码让单字尽量唯一化。

不少 Rime 的用户，是担心大厂输入法上传隐私，才使用 Rime。 既然 Rime 不能云计算的整句输入，那就弄好自己的词库吧，尽量用长词来输入。几百万的词库里，好多是几个词连在一起的长词。

本人的日常习惯，绝大部分时候用双拼（自然码方案），打词为主，因为有数百万级别词条的词库。

打《小学语文》生字表等常用字打单的场景，可用带辅助码的自然码，减少翻页选字，或者用郑码、虎码打单。

打古文或古籍录入，可用大字集的郑码或虎码打单，并且需要安装大字符集的字体（比如：[天珩字体](http://cheonhyeong.com/Simplified/download.html) ）。

打繁体字，偶尔用[注音](https://github.com/rime/rime-bopomofo)（Rime自带，在default.yaml里启用就行。若要更符合港台习惯，则最好另找更好的注音词库）。

用广东话打字，偶尔用[粤拼](https://github.com/rime/rime-cantonese) （Rime不自带）。

# 感谢 ❤️

感谢上述提到的词库、方案及功能参考。

