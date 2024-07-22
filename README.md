# 雾凇拼音 + 搜狗词库 + CJK-E郑码 + 双辅自然码

## 雾凇拼音

雾凇拼音提供了一套开箱即用的 Rime 完整配置，包含了输入方案（全拼、双拼）、长期维护的词库及各项扩展功能。

雾凇拼音: https://dvel.me/posts/rime-ice/  github: https://github.com/iDvel/rime-ice/

## 搜狗词库

搜狗标准词库： https://pinyin.sogou.com/dict/detail/index/11640  

搜狗细胞词库的其他词库： https://pinyin.sogou.com/dict/

在雾凇的码表基础上，补充了搜狗词库后，总共约 225 万拼音、双拼共用的字词。

## 单字减少重码的方法

雾凇里已整合了“部件拆字”的功能，输入同音的单字，可减少翻页。

此外，在 custom_phrase_double.txt 里添加了近 7000 常用字（带单辅码）的编码。

输入同音的单字减少，为了翻页，首选做法：单辅。（双拼后多打一键，或许就能看到所要的字）

第二种做法，部件拆字。

第三种做法，切换到自然码，用双辅。（但自然码词库小一些）

## CJK-E 郑码

郑码:（来自Rime作者佛振）https://github.com/lotem/rime-zhengma.git  , 主要提取其中 CJK-E 字，补充到不知郑码中。

不知郑码: https://github.com/GongMu/rime-zhengma.git  使用了 bzzm.*.yaml 等文件。约 18 万字词。


## 双辅自然码

自然码：https://github.com/mutoe/rime ，  使用了 zrm2000.dict.yaml 和 zrm2000.schema.yaml 两个文件，可用双辅码。约96万字词。

## 搜狗词库转 Rime 格式：

https://github.com/lewangdev/scel2txt


# 文件列表

```
不知郑码：

├── bzzm.dict.yaml（修改，增加3行）
├── bzzm.phrases.dict.yaml
├── bzzm.phrases1.dict.yaml
├── bzzm.schema.yaml
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
├── custom_phrase_double.txt（新增，自然码双拼单辅的几千常用单字）
├── default.yaml（修改schema_list、page_size，增加一个swither的hotkey，多启用两组翻页键）
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
│   ├── script
│   │   ├── go.mod
│   │   ├── go.sum
│   │   ├── main.go
│   │   └── rime
│   │       ├── check.go
│   │       ├── cn_en.go
│   │       ├── dir_mac.go
│   │       ├── dir_windows.go
│   │       ├── emoji.go
│   │       ├── others.go
│   │       ├── pinyin.go
│   │       ├── polyphone.go
│   │       ├── rime.go
│   │       ├── sort.go
│   │       ├── 错别字.txt
│   │       ├── 需要注音.txt
│   │       └── 汉字拼音映射.txt
│   └── sponsor.webp
├── pinyin_simp.dict.yam  l（袖珍简化字拼音，源自 Android 拼音。bzzm 依赖它）
├── pinyin_simp.schema.yaml（袖珍简化字拼音，源自 Android 拼音。bzzm 依赖它）
├── radical_pinyin.dict.yaml
├── radical_pinyin.schema.yaml（修改speller的algebra，由全拼改为自然码双拼。删除5行其他双拼）
├── rime.lua
├── rime_ice.dict.yaml（启动41448大字表；增加搜狗标准词库、搜狗网络新词词库、其他常用的搜狗细胞词库）
├── rime_ice.schema.yaml（schema name 由雾凇拼音改为拼音）
├── squirrel.yaml（增加roseo_maple皮肤，作为自用首选皮肤；增加 candidate_list_layout: linear）
├── symbols_caps_v.yaml
├── symbols_v.yaml
├── t9.schema.yaml
├── weasel.yaml

自然码

├── zrm2000.dict.yaml
├── zrm2000.schema.yaml
```


## 提取词库的一些命令行

```
#1.汇总现有词库
#cat base.dict.yaml 8105.dict.yaml 41448.dict.yaml ext.dict.yaml others.dict.yaml tencent.dict.yaml > ice.txt

#2.去掉注释行
#grep -v "^#" ice.txt > ice1.txt

#3.只取有中文的行
#ugrep '[\x{4E00}-\x{9FFF}\x{3400}-\x{4DFF}\x{20000}-\x{2A6DD}\x{9FA6}-\x{9FBB}\x{FA70}-\x{FAD9}\x{9FBC}-\x{9FC3}\x{2A700}-\x{2B734}\x{2B740}-\x{2B81D}\x{2B820}-\x{2CEAF}\x{9FCD}-\x{9FD5}\x{2CEB0}-\x{2EBEF}\x{30000}-\x{3134A}\x{31350}-\x{323AF}\x{2EBF0}-\x{2EE5F}\x{3007}]' ice1.txt > ice2.txt

#4.去掉编码
#sd "   .*$" "" ice2.txt

#5.找出那些在 sogou_network_pop_new_words.txt 但不在 ice2.txt 的行:
#python3 scel2txt.py  ./网络流行新词【官方推荐】.scel  ./sogou_network_pop_new_words.txt
#awk 'NR==FNR {lines[$0]; next} !($0 in lines)' ice2.txt  sogou_network_pop_new_words.txt  > sogou_network_pop_new_words.dict.yaml

#6.人工整理 新的 dict.yaml，在前面加些行。
#...
```

# 感谢 ❤️

感谢上述提到的词库、方案及功能参考。

