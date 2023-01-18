---
title: Merge UT Dictionaries
date: 2023-01-15
---

## Overview

Merge UT Dictionaries merges multiple Mozc UT dictionaries into one and modify the costs.

Mozc UT dictionaries contain the following dictionaries:

- [mozcdic-ut-alt-cannadic](https://github.com/utuhiro78/mozcdic-ut-alt-cannadic)

- [mozcdic-ut-edict2](https://github.com/utuhiro78/mozcdic-ut-edict2)

- [mozcdic-ut-jawiki](https://github.com/utuhiro78/mozcdic-ut-jawiki)

- [mozcdic-ut-neologd](https://github.com/utuhiro78/mozcdic-ut-neologd)

- [mozcdic-ut-personal-names](https://github.com/utuhiro78/mozcdic-ut-personal-names)

- [mozcdic-ut-place-names](https://github.com/utuhiro78/mozcdic-ut-place-names)

- [mozcdic-ut-skk-jisyo](https://github.com/utuhiro78/mozcdic-ut-skk-jisyo)

- [mozcdic-ut-sudachidict](https://github.com/utuhiro78/mozcdic-ut-sudachidict)

Please give them a [GitHub Star](https://docs.github.com/ja/get-started/exploring-projects-on-github/saving-repositories-with-stars):

Mozc: [1678 Stars](https://github.com/google/mozc)
Fcitx5: [895 Stars](https://github.com/fcitx/fcitx5)
Fcitx5-mozc: [33 Stars](https://github.com/fcitx/mozc)

> リポジトリに Star を付けるということは、リポジトリメンテナに対してその作業についての感謝を示すことでもあります。

## License

mozcdic-ut.txt (generated by this tool): Combined

jawiki-latest-all-titles: [CC BY-SA 3.0](https://ja.wikipedia.org/wiki/Wikipedia:ウィキペディアを二次利用する)

- This tool updates the costs for words using jawiki-latest-all-titles.

[id.def](https://github.com/google/mozc/blob/master/src/data/dictionary_oss/id.def) from Mozc: [BSD-3-Clause](https://github.com/google/mozc)

- This tool updates the ID for words using id.def.

Source code: Apache License, Version 2.0

## Usage

Clone the Mozc UT dictionaries and extract them.

```
git clone https://github.com/utuhiro78/merge-ut-dictionaries.git

cd merge-ut-dictionaries/src/

git clone https://github.com/utuhiro78/mozcdic-ut-alt-cannadic.git
git clone https://github.com/utuhiro78/mozcdic-ut-edict2.git
git clone https://github.com/utuhiro78/mozcdic-ut-jawiki.git
git clone https://github.com/utuhiro78/mozcdic-ut-neologd.git
git clone https://github.com/utuhiro78/mozcdic-ut-personal-names.git
git clone https://github.com/utuhiro78/mozcdic-ut-place-names.git
git clone https://github.com/utuhiro78/mozcdic-ut-skk-jisyo.git
git clone https://github.com/utuhiro78/mozcdic-ut-sudachidict.git

cp mozcdic-ut-*/mozcdic-ut-*.txt.tar.bz2 .

for f in mozcdic-ut-*.txt.tar.bz2; do tar xf "$f"; done
```

Comment out unnecessary UT dictionaries in make.sh.

```
mousepad make.sh
```

Default settings:

```
#alt_cannadic="true"
#edict="true"
jawiki="true"
neologd="true"
personal_names="true"
place_names="true"
#skk_jisyo="true"
#sudachidict="true"
```

Run make.sh.

```
sh make.sh
```

It generates a merged dictionary "mozcdic-ut.txt". The costs are modified by jawiki-latest-all-titles.

```
ls mozcdic-ut.txt
```

## Building Mozc

### Arch Linux

```
ruby get_latest_mozc.rb 

rm -rf tmp_mozc
mkdir tmp_mozc
cp {fcitx5-mozc-ut.PKGBUILD,mozc-2.*.tar.bz2,mozcdic-ut.txt} tmp_mozc/

cd tmp_mozc/
makepkg -is -p fcitx5-mozc-ut.PKGBUILD
```

### Other distributions

Add mozcdic-ut.txt to dictionary00.txt.

```
cd src/
ruby get_latest_mozc.rb 

rm -rf tmp_mozc
mkdir tmp_mozc
cp {mozc-2.*.tar.bz2,mozcdic-ut.txt} tmp_mozc/

cd tmp_mozc/
tar xf mozc-2.*.tar.bz2

cat mozc-2.*/src/data/dictionary_oss/dictionary00.txt mozcdic-ut.txt > dictionary00.txt.new
mv dictionary00.txt.new mozc-2.*/src/data/dictionary_oss/dictionary00.txt
```

Build Mozc as usual.

[HOME](http://linuxplayers.g1.xrea.com/mozc-ut.html)
