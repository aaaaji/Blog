---
title: "隨手亂筆記區"
draft: true
date: "2020-04-03"
tags: [""]
categories: ["技術"]
---

## 參考資料



## bash相關

* 定義使用的shell
**```#!/bin/sh```** --> Bourne Shell (sh)，sh是所有Unix系統中都會有的shell

* 變數
```shell=
//定義變數，印出變數，被引用要加$
color=red
echo $color
--> red

//指令輸出成變數，用``包起來代表執行該指令
now=`date`
echo $now
--> Tue Jul 2 19:54:17 CST 2019

//變數後面有其他字串
A=dark
echo ${A}blue
--> darkblue

echo "$A"blue
--> darkblue

//注意
//雙引號""中的特殊字元不會被忽略
//單引號''中的特殊字元會被忽略
//反斜線\後的一個字元會被視為普通字串
animal=fox
echo $animal
--> fox

echo "$animal"
--> fox

echo '$animal'
--> animal

echo \$animal
--> animal
```

* if判斷
```shell=
if [判斷A] || [判斷B] && [判斷C]; then
    做事情1
elif [判斷D]; then
    做事情2
else
    做事情3
fi
```
