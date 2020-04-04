---
title: "一些在Linux上常用的方便指令"
draft: true
date: "2020-04-04"
tags: ["Linux","tools","command"]
categories: ["技術"]
---



### cat
在標準輸出印出檔案內容

- 使用方式
    > $ cat [Option]... [File]...

- 常用選項

    - -n,-b
        顯示輸出行數，方便快速找出問題行數

### echo
顯示一行文字，常配合其他指令組合使用

### date 日期
根據設定格式顯示現在時間或設定系統時間

- 使用方式
    > date [Option]... [+format]

- 常用 format
    - %Y：西元年
    - %m：月
    - %d：日
    - %H：幾點，24小時制
    - %M：分鐘
    - %S：秒
    - %Z：時區縮寫

- 範例
```bash=
date -u '+%Y-%m-%d_%H:%M:%S_%Z'
# 2020-04-04_03:16:08_UTC
```

### find
層層目錄中搜尋檔案，內建許多搜索選項方便使用

- -name：指定檔名搜索
- -type：指定檔案類型搜索
    - -type c 檔案
    - -type d 目錄
- -perm：指定檔案權限搜索
- -user：指定檔案擁有者搜索
- -size：指定檔案大小搜索


### basename
印出移除目錄的檔案名稱(只保留最後的檔案名)，也可移除副檔名




### export 輸出
用來設定or顯示環境變數。在shell執行時，shell會提供一組環境變數。export 可新增、修改或刪除環境變數，供後續執行的程式使用。該效果只存在當次登錄操作。
    
```bash=
export [-fnp][變數名稱]=[變數設定值]
```
    
- -f 代表[變數名稱]中的函數名稱
- -n 刪除指定的變量。變量實際上未刪除，只是不會輸出到後續執行的環境中。
- -p 列出所有shell賦予程式的環境變數

### rsync
複製本機or遠端的檔案
```bash=
rsync -vrah <來源檔案> <目標檔案>
```
- -v：verbose模式，輸出比較詳細的訊息
- -r：遞迴(recursive)，備份所有子目錄下的目錄&檔案
- -a：封裝備份模式，相當於 -rlptgoD，遞迴備份所有子目錄下的目錄與檔案，保留連結檔、檔案的擁有者、群組、權限以及時間戳記。
- -z：啟用壓縮。
- -h：將數字以比較容易閱讀的格式輸出。

### dd
* ddimg.sh
    ```bash
    dd if=$2 conv=sync,noerror bs=128K count=262144 sutatus=progress | gzip -3c | dd of=$1

    if=$2 --> 讀入第2個值的資料
    conv=sync,noerror --> 把每個輸入的大小都調到ibs的大小(用NUL填充)，遇到錯誤持續處理不暫停
    bs=128K --> 指定block size，一次讀取&寫入BYTES位元組的資料(default=512)，會覆蓋ibs(指定輸入區塊大小)&obs(指定輸出區塊大小)
    count=262144 --> 只複製N個輸入區塊
    status=progress --> 顯示複製進度
    of=$1 --> 寫到第1個值的位置
    ```

* imgdd.sh
    ```bash
    zcat $1 | dd of=$2 conv=sync,noerror status=progress
    parted $2 -s 'resizepart 3 512.11GB'

    zcat -->解壓縮