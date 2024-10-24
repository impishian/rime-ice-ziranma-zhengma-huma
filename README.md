### 输入法组合图示

<img width="818" alt="image" src="https://github.com/user-attachments/assets/bb207e7c-b1e5-4d1a-946a-6034c7410eef">

<img width="1155" alt="image" src="https://github.com/user-attachments/assets/1e6f7934-2d8f-4cc9-a670-378e4770ae1f">

----

### 0. TL;DR

(1) **雾凇拼音、搜狗细胞词库、自定义短语辅码方案、多种对候选字词二次筛选的方案 + 双辅自然码 + CJK-E郑码 + CJK-I虎码**

将自己常用的输入法组合，配置到一套 rime 配置里。记述定制过程。后面的树形 “文件列表” 部分，列出了在雾凇基础上增删改的文件。

在 MacOS 安装好鼠须管，备份并清空 ~/Library/Rime，将本仓库内容复制到该路径下，重新部署即可。其他平台，未实测，应该基本类似。

(2) **自然/虎形输入法组合**
  
- **音码：双拼 (自然码方案)**，打词打句

- **音形结合**：[**自然虎形**](https://github.com/impishian/rime-ice-ziranma-zhengma-huma/) - 虎码首末作为双拼辅码，打单字

  比鹤形辅码、自然辅码重码率更低。对于已记住虎码字根者，不需再记一套仅专用于音形码的字根和键位。

  边打边想，分词断句。该打词句时，打词句。该打字时，打字。
  
- **形码：虎码**，适合盲打和大字集的古籍等
  
  8105字集内：近乎单字唯一化，重码本不多，若有重，大都可用 ;' 选二三字。 重码>3的只有三组编码: kor 旭沓汩汨旮 / gwfr 彀觳榖縠 / fdvi 嬴羸赢蠃

  若追求更极致，想不重码打这少量的字，可参看[虎码官网给一些用户自定优化的建议](https://tiger-code.com/docs/customDefinition)，用 无理容错码 、回头码 、音补、顺取变为先取中间 等方式取码，当然这些都是可选的方式。

- 记忆量：双拼键位、虎码字根（规则几乎0记忆量）。

----
### 1. 雾凇拼音

[雾凇拼音](https://dvel.me/posts/rime-ice/) 提供了一套开箱即用的 Rime 完整配置，包含了输入方案（全拼、双拼）、长期维护的词库及各项扩展功能。

[雾凇拼音github](https://github.com/iDvel/rime-ice/)


|  功能   | 用法 | 说明 |
|-------|----------|--------|
| **拆字二次筛选** | 输完拼音，` + 汉字部件的音<br>进行二次筛选，以减少重码 | **注意：与自然码辅码 不同** <br><br> 它是通过[汉字部件拆字](https://github.com/mirtlecn/rime-radical-pinyin)实现的 |
| **拆字组字** | uU 开头 + 各部件的音 | 常用于输多个常见字作为部件所组成的难字。<br><br>因为反查时前缀会消失，影响打英文，<br>所以设定为两个字母，或可改成一个非字母符号|
| **以词定字** | 打词组，用两个中括号 [ ] 分别取首字、尾字| |
| 符号 | 双拼大写 V 开头，全拼 v 开头 | symbols_caps_v.yaml 和 <br>symbols_v.yaml 里的各种符号。 |
| 数字和金额大写 |大写 R 开头 | 如 R1234 得到：<br>「一千二百三十四、壹仟贰佰叁拾肆元整」 |
| 日期时间 | 双拼为 date time week datetime <br>timestamp，全拼为 rq sj xq dt ts | |
| 农历指定日期 | 大写 N 开头 |如 N20240210 得到：<br>「二〇二四年正月初一」 |
| 农历 | 双拼 lunar，全拼 nl。 | |
| Unicode | 大写 U 开头 | 如 U62fc 得到「拼」|
| 在拼音中前后移动 | Tab 或 Shift + Tab | |
| 删词/降频| 鼠须管 Fn + ⇧ + ⌫，<br>小狼毫 Ctrl/Shift + Del <br>删除自造词，<br>或降低词库中已有词语的权重<br>（回到原始权重，不是降到最低） |想永久删除一个词库中<br>存在的词汇，<br>只能编辑词库，重新部署 |
| 中英混输 | 带了2万多常用单词 | 如果需纯英文单词输入的方案，可以换用 [rime-easy-en](https://github.com/BlindingDark/rime-easy-en)，支持语句流；或者直接换个输入法，例如这个很好用的[哈利路亚输入法](https://github.com/dongyuwei/hallelujahIM) |

### 2. 搜狗细胞词库

[搜狗标准词库](https://pinyin.sogou.com/dict/detail/index/11640) （只是名字叫这个，可能不是搜狗官方词库？）

[搜狗细胞词库的其他词库](https://pinyin.sogou.com/dict/) （选了些诗词、名句、地名、明星、网络热词）

在雾凇的词库基础上，补充了一些诗词、地名等搜狗词库后，去重，总共约 220 万拼音、双拼共用的字词。

### 3. 打单字减少重码和打难字的几种方法

雾凇里本已整合了“部件拆字”、“以词定字”等功能，以减少同音字的重码和翻页，以及能打出难字。

还可通过复制 custom_phrase_double_zrm.txt 为 custom_phrase_double.txt，再重新部署，自定义短语。这是 6000 多带有自然码的单或双辅码的常用字。

打同音单字减少重码翻页和打难字，有以下几种方法，都可以使用。

**3.1 第一种：单字辅码**

声韵双拼后多打一或两键（自然码辅码），或许就能看到所要的字。

这是依赖 custom_phrase_double.txt 自定义短语来做到的，只有 6000 多常用字。

BTW, 若将 custom_phrase_double_zrm_hu.txt 复制为 custom_phrase_double.txt，则是 **自然虎形** (自然双拼 + 虎码首末 的双辅码)，涵盖规范字 8000-9000 字，适合双拼+虎码都熟悉者使用。

|  字   | 双拼 | 辅码 | 说明 |
|-------|----------|--------|--------|
| 沐 | mu | d | d = 氵 |
| 幕 | mu | j | j = 巾 |
| 牡 | mu | n | n = 牛 |

这样，4键以内，若有对应的字，则候选的第1位置优先显示单字。4键以后，第1位置逐渐显示为词。

**3.2 第二种：以词定字**、**拆字二次筛选**、**拆字组字**

都是雾凇里整合好的功能。

举例：

|  功能   | 用法 | 举例 | 说明 |
|-------|----------|--------|--------|
| 以词定字 | 打词后,<br> [选词首的字, <br>]选词尾的字 | mzgv = 玫瑰，<br>mzgv[ = 玫<br>mzgv] = 瑰| mzgv是 mei gui 的双拼  |
| 拆字二次筛选 | 为了打难字，在双拼后,<br> \`+部件的音 | mu\`uv = 沐<br> mu\`mojn = 幕<br>mu\`nqtu = 牡 | uv = 三点水的双拼<br>mo = 莫，jn = 巾，jn 不必输，就看到该字<br>nq = 牛，tu = 土，nqtu 也不必全输，就看到该字 |
| 拆字组字 | 打难字时，uU+各部件双拼 |uUmojn 幕<br>uUnqtu 牡 | mo = 莫，jn = 巾<br>nq = 牛，tu = 土 |

【注】

如果觉得雾凇整合的拆字部件作为筛选条件，输入码太长，不够顺手，还可由 "双拼" 切换到 “**双拼2**”。

双拼2，是 copy & paste 双拼而得到的一个新schema，只是 **将二次筛选方式，由汉字拆字部件，改为自然码辅码**。

|  功能   | 用法 | 举例 | 说明 |
|-------|----------|--------|--------|
| 自然码辅码 | 在双拼后,<br> \`+部件的音 |mu\`dm = 沐<br><br>mu\`cj = 幕<br>或<br>mu\`jm = 幕<br><br>mu\`nt = 牡 |  |

对比 double_pinyin.schema.yaml 和 double_pinyin2.schema.yaml，可看到 “双拼”和 “双拼2” 这二者的细微区别。
```
  schema_id: double_pinyin               |         schema_id: double_pinyin2
  name: 双拼                              |         name: 双拼2
    - lua_filter@search@radical_pinyin   |           #- lua_filter@search@radical_pinyin  # 部件拆字二次筛选
                                         >           - lua_filter@*aux_code@ZRM_Aux-code_4.3  # 几种筛选方案：ZRM_Aux-code_4.3, flypy_full, wubi86-code, tiger
                                         >         aux_code_trigger: "`"
```

双拼2，是通过[辅助码的音形分离插件](https://github.com/HowcanoeWang/rime-lua-aux-code) 来实现的（btw, 触发码由;改为`），配置使用都很简单。

这个插件的**二次筛选码表，与现有的拼音码表，是独立的、分离的文件**。 附带了自然码辅码、鹤形辅码、五笔86、郑码、虎码等几种。想用哪个都可以。

如果想用小鹤音形的形码、86五笔、郑码或虎码来二次筛选，可以修改 double_pinyin2.schema.yaml 里的这行配置，@ 后面改为具体的方案。

打难字或重码太多的词组时，往往加一两码筛选，就能减少很多翻页。

```
- lua_filter@*aux_code@ZRM_Aux-code_4.3
# rime-lua-aux-code。几种选择：
# (1) 自然码辅码作为二次筛选：ZRM_Aux-code_4.3；
# (2) 鹤形辅码作为二次筛选：flypy_full；
# (3) 86五笔作为二次筛选：wubi86-code；
# (4) 郑码作为二次筛选：zhengma；
# (5) 虎码作为二次筛选：tiger
```

文件格式也很简单，如果有自己的定制其他方案的码表，也可自行替换。**双拼方案 + 二次筛选方案，可以自由组合**。

**"自然鹤形" （自然码的双拼 + 小鹤的形辅）**，这样的搭配是不是也挺有意思呢。

它适用于这样的使用者：已习惯多年的自然码双拼布局，但因自然码的辅码在官方手册描述不多，想找一个其他的详细描述规则的辅码方案。

若使用手心输入法，可参考：[手心输入法中使用自然鹤形打单](https://github.com/impishian/input_method/blob/main/%E9%B9%A4%E5%BD%A2%E8%BE%85%E7%A0%81/README.md) 的 2.3 小节。

小鹤音形，应该也是受自然码启发而作，只是双拼键位稍微换了些位置，并且二者的辅码字根也有些是相同的。

[鹤形辅码](https://github.com/impishian/input_method/blob/main/%E9%B9%A4%E5%BD%A2%E8%BE%85%E7%A0%81/%E9%B9%A4%E5%BD%A2.md) 的字根和规则，似乎梳理得有规律些，字根也多些。

可是鹤形主要是8105个规范汉字。（按一些专家观点，这也已经[覆盖日常打字99.999%以上的字](https://flypy.cc/#/zf)了） 

自然码辅码码表，大概覆盖 CJK 约两万的字（但也不一定全有 8105 规范汉字的全部）。

多年前也有人做过 “自然鹤形” 的码表，若对此有兴趣，也可参考 [ziranma_flyx_for_Rime](https://github.com/daya-prac/ziranma_flyx_for_Rime)

**3.3 第三种：切换到自然码，用双辅**

详见下面的”双辅自然码“。

但是，自然码词库小一些，且官方已隐退江湖多年，没有维护新词库，词库里难免有些过时的词。

**3.4 第四种：用纯形码**

若面对的不是常用单字，或者需要输入大量的不知读音的单字，只能用形码。

比如：郑码、仓颉、五笔，或受它们影响而诞生的各种像虎码、徐码、宇浩、......等等这样的方案。

### 4. 双辅自然码

1. [自然码2000官网](http://ziranma.com.cn/uiysuomy.htm)

2. [自然码双拼和辅码参考pdf](https://github.com/impishian/input_method/blob/main/%E5%8F%8C%E6%8B%BC_%E8%87%AA%E7%84%B6%E7%A0%81%E6%96%B9%E6%A1%88/zrm.pdf) 

   pdf说明：
```
(1) 自然码辅码，均为声母。只要会念，就会了。

(2) 括号里的蓝色字：形近归并的项。

(3) 红色字：难念的项，特别标出了拼音，以便理解记忆。
```

3. 再次提醒注意：**自然码辅码**，与雾凇整合的 **拆字二次筛选**，是不同的。二者均是减少重码的好手段。

4. 采用 [mutoe](https://github.com/mutoe/rime) 或 [henices](https://github.com/henices/rime) 的码表
  
   用了 zrm2000.dict.yaml 和 zrm2000.schema.yaml 这两个文件。若去掉编码，只留字词，再去重，统计结果约 18 万字词。

5. 自然码辅码

  - 举例

    |  字   | 双拼 | 辅码 | 说明 |
    |-------|----------|--------|--------|
    | 沐 | mu | d<br>或<br>dm | d = 氵<br><br>d = 氵，m = 木 |
    | 幕 | mu | j<br>或<br>cj | j = 巾<br><br>c = 艹，j = 巾 |
    | 牡 | mu | n<br>或<br>nt | n = 牛<br><br>n = 牛，t = 土 |

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

6. 与双拼2有何不同

奥林匹克：用双拼2，每字声韵，共8键。用自然码，只需 alpk 4键

自然码，这里设置6键码长，自动上屏。双拼2则可以输入很长的句子，智能组长词。

自然码，词库相对小一些。双拼2，词库很大。

通用规范汉字表 8105 个覆盖情况：这词库里只有 CJK 的字 7829 个（少3个），扩展A-E 的 273 个字没有（似乎一般人倒是也用不上）

### 5. CJK-E 郑码

采用了 [不知郑码](https://github.com/GongMu/rime-zhengma.git)  的 bzzm.*.yaml 等文件。

提取 [郑码（来自Rime作者佛振）](https://github.com/lotem/rime-zhengma.git) 的 CJK-E 字，补充到不知郑码中。通用规范汉字表 8105 个字全覆盖。

约 18 万字词。自从用虎码后，郑码目前少用了。以前很喜欢用，因此，留一份在这儿。

### 6. CJK-I 虎码单字

[虎码资源下载](http://huma.ysepan.com)

采用了[虎码](https://tiger-code.com) 官方单字 tiger.dict.yaml, tiger.schema.yaml ，适当简化配置，仅用于打单。

tiger.dict.yaml.orig 是官方原始单字码表，tiger.dict.yaml 移除一些部首和笔画等影响正常选字的编码。

完全支持 CJK to CJK-I 所有单字，近 10 万。适合录入古籍。

支持拼音滤镜、拆字滤镜（Ctrl + Shift + 0， <- 和 ->， Enter，启用/禁用），在输入的同时，可看到某个字的读音 或者 拆法。

BTW，如果只需打《通用规范汉字表》的8105单字，可切换到 "虎码8105单字"。(实现方式很简单：将 tiger.dict.yaml 过滤 8105字集 的字，得到 tiger3.dict.yaml)

### 7. CJK-I 虎码字词

为了简化配置，虎码官方的三个 tigress*.dict.yaml 合为 tiger2.dict.yaml。

除了所有的近 10 万单字外，还支持 16 万词。

### 8. 文件列表

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
├── custom_phrase_double_zrm.txt   （新增，自然码双拼，单字辅码，6000 多常用单字。需复制到 custom_phrase_double.txt，重新部署）
├── custom_phrase_double_zrm_hu.txt（新增，自然码双拼，虎码首末作为辅码，8000多常用单字。需复制到 custom_phrase_double.txt，重新部署）
├── default.yaml（修改schema_list、page_size，增加一个switcher的hotkey，启用，.翻页）
├── double_pinyin.schema.yaml（修改 schema name ，由“自然码双拼”改为“双拼”。删除其他双拼方案的schema.yaml文件）
├── double_pinyin2.schema.yaml（添加“双拼2”。 部件拆字的二次筛选查询，由汉字部件改为自然码辅码 或 鹤形辅码、五笔86、虎码。）
├── en_dicts
│   ├── cn_en.txt
│   ├── cn_en_double_pinyin.txt（只留下自然码双拼，删除其他双拼方案的txt文件）
│   ├── en.dict.yaml
│   └── en_ext.dict.yaml
├── lua
│   ├── ZRM_Aux-code_4.3.txt （添加：二次筛选插件的 自然码辅码表）
│   ├── autocap_filter.lua
│   ├── aux_code.lua   （添加：独立处理二次筛选的插件）
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
│   ├── flypy_full.txt（添加：二次筛选插件的 鹤形表）
│   ├── is_in_user_dict.lua
│   ├── long_word_filter.lua
│   ├── lunar.lua
│   ├── number_translator.lua
│   ├── pin_cand_filter.lua
│   ├── reduce_english_filter.lua
│   ├── search.lua
│   ├── select_character.lua
│   ├── t9_preedit.lua
│   ├── tiger.txt      （添加：二次筛选插件的 虎码表）
│   ├── unicode.lua
│   ├── v_filter.lua
│   ├── wubi86-code.txt（添加：二次筛选插件的 五笔86表）
│   └── zhengma.txt    （添加：二次筛选插件的 郑码表）
├── melt_eng.dict.yaml
├── melt_eng.schema.yaml（修改speller的algebra，由全拼改为自然码双拼。删除5行其他双拼）
├── opencc
│   ├── pinyin.json       (虎码，拼音滤镜)
│   ├── PYCharacters.txt
│   ├── PYPhrases.txt
│   ├── hu_cf.json        (虎码，拆分滤镜)
│   ├── hu_cf.tx
│   ├── emoji.json
│   ├── emoji.txt
│   └── others.txt
├── pinyin_simp.dict.yam  l（袖珍简化字拼音，源自 Android 拼音。bzzm 依赖它）
├── pinyin_simp.schema.yaml（袖珍简化字拼音，源自 Android 拼音。bzzm 依赖它）
├── radical_pinyin.dict.yaml
├── radical_pinyin.schema.yaml（修改speller的algebra，由全拼改为自然码双拼。删除5行其他双拼）
├── rime.lua
├── rime_ice.dict.yaml（启用41448大字表？日常打字还是不建议启用，实在用不着。增加搜狗标准词库、搜狗网络新词词库、其他常用的搜狗细胞词库）
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

├── tiger.dict.yaml  (增加虎码单字：CJK-I 内约10万单字。以官方单字码表为基础，移除一些部首、笔画等)
├── tiger.dict.yaml.orig (原始官方单字码表)
├── tiger.schema.yaml (官方 schema 适当简化，减少依赖等)

├── tiger2.dict.yaml  (增加虎码字词)
├── tiger2.schema.yaml

├── tiger3.dict.yaml  (增加虎码单字：《通用规范汉字表》的8105字)
├── tiger3.schema.yaml
```

### 9. 工具

#### 9.1 搜狗词库转 Rime 格式工具

[scel2txt](https://github.com/lewangdev/scel2txt)

#### 9.2 提取词库的一些命令行

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

#7.提取 CJK-E 字  （MacOS: ugrep, Linux: grep -P。 因为 MacOS 的 grep/sed 是 BSD 的版本，不是 GNU 的版本，支持的特性弱一些）
ugrep '[\x{2B820}-\x{2CEAF}]' zhengma.dict.yaml |wc -l
5815
#可以导入5815个字到bzzm
```

### 10. CJK 和 Unicode

[支持大字集的字体](https://zh.wikipedia.org/wiki/Wikipedia:Unicode%E6%89%A9%E5%B1%95%E6%B1%89%E5%AD%97)

[CJK](https://zh.wikipedia.org/wiki/%E4%B8%AD%E6%97%A5%E9%9F%93%E7%B5%B1%E4%B8%80%E8%A1%A8%E6%84%8F%E6%96%87%E5%AD%97)

[通用规范汉字表](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E8%A7%84%E8%8C%83%E6%B1%89%E5%AD%97%E8%A1%A8)

[通用规范汉字表 8105 字的 Unicode 编码和拼音](https://zh.wiktionary.org/wiki/Appendix:%E9%80%9A%E7%94%A8%E8%A7%84%E8%8C%83%E6%B1%89%E5%AD%97%E8%A1%A8)

通用规范汉字表的 8105 个字，直到 CJK-E 才全覆盖。其中，在 CJK 区有 7832 字，在 CJK-A/B/C/D/E 区分别有 77/36/44/8/108 字。

为覆盖《通用规范汉字表》的所有字：

1.字体至少应支持到 CJK-E。

2.输入法码表，也不应只是 CJK 字。

（雾凇里单列了 8105 字的码表。实际上，还补充了：〇 U+3007 、冇 U+7121 ......等35 个字，并注释掉里1个字(呣)，再加上一字多音，码表总行数比 8105 还多几百行。BTW，“〇”这个字，属于[中日韩符号和标点](https://zh.wikipedia.org/wiki/%E4%B8%AD%E6%97%A5%E9%9F%A9%E7%AC%A6%E5%8F%B7%E5%92%8C%E6%A0%87%E7%82%B9)区)。

```
# 8105.txt：8105行，每行一字（第$1列为字）。
# 8105.dict.yaml：码表
# 为了找出码表里属于 8105.txt 的字，先用 awk 在两个文件间做 pattern match，再去重，得到 8104.txt。经比较，码表里未启用“呣”这1字。
$ awk 'NR==FNR{a[$1];next} { if ($1 in a) {print $0}}' 8105.txt  cn_dicts/8105.dict.yaml| awk '{print $1}' | awk '!a[$0]++'  > 8104.txt

# 用相反的条件，可找出补充的35个字：
$ awk 'NR==FNR{a[$1];next} { if (!($1 in a)) {print $0}}' 8105.txt  cn_dicts/8105.dict.yaml |grep .|grep -v -E "#|name|version|sort|\.|-"|wc -l
35
```

### 11. 从 CJK, CJK-A 到 CJK-I

1 根据 CJK wikipedia 词条正文的表格，整理的情况如下：

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

2.而根据 CJK wikipedia 词条最后的表格里的“编码范围”，整理的情况如下：

（1）已统一：

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
grep -P '[\x{4E00}-\x{9FFF}]'
grep -P '[\x{3400}-\x{4DBF}]'
grep -P '[\x{20000}-\x{2A6DF}]'
grep -P '[\x{2A700}-\x{2B73F}]'
grep -P '[\x{2B740}-\x{2B81F}]'
grep -P '[\x{2B820}-\x{2CEAF}]'
grep -P '[\x{2CEB0}-\x{2EBEF}]'
grep -P '[\x{30000}-\x{3134F}]'
grep -P '[\x{31350}-\x{323AF}]'
grep -P '[\x{2EBF0}-\x{2EE5F}]'

#### grep -P '[\x{4E00}-\x{9FFF}\x{3400}-\x{4DBF}\x{20000}-\x{2A6DF}\x{2A700}-\x{2B73F}\x{2B740}-\x{2B81F}\x{2B820}-\x{2CEAF}\x{2CEB0}-\x{2EBEF}\x{30000}-\x{3134F}\x{31350}-\x{323AF}\x{2EBF0}-\x{2EE5F}]' ... 似乎不支持多个范围？？
```

（2）未统一：

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
grep -P '[\x{2E80}-\x{2EFF}]' 
grep -P '[\x{2F00}-\x{2FDF}]' 
grep -P '[\x{2FF0}-\x{2FFF}]' 
grep -P '[\x{3000}-\x{303F}]' 
grep -P '[\x{31C0}-\x{31EF}]' 
grep -P '[\x{3200}-\x{32FF}]' 
grep -P '[\x{3300}-\x{33FF}]' 
grep -P '[\x{F900}-\x{FAFF}]' 
grep -P '[\x{FE30}-\x{FE4F}]' 
grep -P '[\x{1F200}-\x{1F2FF}]' 
grep -P '[\x{2F800}-\x{2FA1F}]' 

#### ugrep '[\x{2E80}-\x{2EFF}\x{2F00}-\x{2FDF}\x{2FF0}-\x{2FFF}\x{3000}-\x{303F}\x{31C0}-\x{31EF}\x{3200}-\x{32FF}\x{3300}-\x{33FF}\x{F900}-\x{FAFF}\x{FE30}-\x{FE4F}\x{1F200}-\x{1F2FF}\x{2F800}-\x{2FA1F}]' ... 似乎不支持多个范围？？
```

### 12. 其他

在此提一下一位打字冠军。某音号：`打字快的州州`，她主要用：搜狗输入法 + 自然码双拼 + 独家词库 + 独家辅码。尽量整句输入。独家辅码，尽量 **让单字唯一化**。

不少 Rime 的用户，是担心大厂输入法上传隐私，才使用 Rime。 

既然 Rime 不能用云计算的整句智能输入，那就弄好自己的词库吧，尽量用长词来输入。

几百万的词库里，好多是几个词连在一起的长词。

用了[辅助码的音形分离插件](https://github.com/HowcanoeWang/rime-lua-aux-code) 的“双拼2”，可以整句输入。对于一整句，只需按一次`，便可对每字词分别用辅码和空格选字。不妨试试打“施氏食狮史”。

----

不同场景，不同的人，输入法的选择和打字习惯，都不一样。比如：

打《小学语文》生字表等常用字打单的场景，可用带辅助码的自然码，减少翻页选字，或者用五笔、郑码、虎码打单。

打古文或古籍录入，可用大字集的五笔、郑码或虎码打单，并且需要安装大字符集的字体（比如：[天珩字体](http://cheonhyeong.com/Simplified/download.html) ）。

打繁体字，则可用[注音](https://github.com/rime/rime-bopomofo)（Rime自带，在default.yaml里启用就行。若要更符合港台习惯，则最好另找更好的注音词库）。

用广东话打字，则可用[粤拼](https://github.com/rime/rime-cantonese) （Rime不自带）。

----

本人的日常习惯：

**自然虎形**

(1) 绝大部分时候用双拼2（自然码方案），打词打句为主，因为有数百万级别词条的词库。

(2) **断句很重要。断句很重要。断句很重要**。

边输入边思考，还能连续打词吗？能连续打词的，就继续打词，不急于空格推上去（能连续打，都是4键以上的）。需及时断句的，要及时把前面内容推上去，用**自然虎形（虎码首末两码为辅码）打个别单字（3键或4键）**，... ，接着再继续思考，再接着尽量打词。 

[单字重码对比](https://github.com/impishian/input_method/tree/main/%E5%8D%95%E5%AD%97%E9%87%8D%E7%A0%81%E5%AF%B9%E6%AF%94)

```
虎码 (0.01%) < 五笔86 (0.14%) <

自然虎形 或 小鹤虎形 (0.38%~0.54%) < 自然表形 (0.79%~1.02%) <

小鹤音形 (1.01%~1.38%) < 自然码 (2%~2.95%) < 

纯双拼 (45%~52%)
```

(3) **打词不带辅**，带辅会影响打字节奏（两码一字），尽量打连着的多个字词（即4键以上，以避免首选字为单字）。 

以上配置，正好没使用更复杂的打词带辅的方案哈。

对于 shi shi 这样的重码较多的词，在继续输入其他词后，结合上下文也没能自动调整为正确的词的话，则可用下面的二次筛选（或提早断句修正，或按ESC取消重输）。

(4) **[] 以词定字。uU 组字输入。` 以虎码作为二次筛选**（因为它是比自然码辅码、鹤形辅码更全能和精准的形码)。 【注】反单撇 后面，目前用的是正常虎码取码法的表，而不是 custom_phrase_double_zrm_hu.txt 里的只取虎码首末两码的表。这是二者的小区别，也比较容易适应。

(5) 实在不会念的、uU 模式又打不了的个别字，才切到虎码。

未经太多练习，日常现代文，每分钟也能打 60-100 字。

若使用手心或搜狗输入法，可参考：[手心或搜狗输入法中使用自然虎形打单](https://github.com/impishian/input_method/tree/main/%E8%99%8E%E5%BD%A2%E8%BE%85%E7%A0%81) , 对 8105 规范字，用虎码首末根作为辅码。

----

btw, 虎码比五笔拆字更直观简单，比郑码打字打词规则一致。不要背字根，需按官网练习程序，字根练习超过3万分，则字根过关，可开始打字。

若以打字为业，或日常需大量打字，则应好好练练虎码，形成肌肉记忆，逐步提速。形码，码长短，重码低，提速上限高，但是需大量练习才能达到高境界。

在B站上搜索：[虎码](https://search.bilibili.com/all?keyword=虎码&from_source=webtop_search&spm_id_from=333.1007&search_source=5)，可看到不少人每分钟能打 100-250 字。

----

[一些输入法的简介](https://github.com/impishian/input_method)

### 13. 感谢 ❤️

感谢上述提到的词库、方案及功能参考。

