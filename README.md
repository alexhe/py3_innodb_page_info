# py3_innodb_page_info

## 背景

原来仓库代码 (https://github.com/happieme/py_innodb_page_info) 很久没更新了，只支持python2。

本代码基于现在主流的python3（我环境是python 3.10)修改而成。

后续如果遇到Python新语法，不支持，也是少数，简单修改即可。

## 代码实现原理
对idb数据文件按page(16K)进行逐页读取，取每个page中的type、offset等偏移，进行统计。

## 主要改动
* python3语法支持
* MySQL 8.0 新的类型支持
* 改为单文件脚本，方便直接 curl 下载

针对MySQL 8.0代码做了异常改造（非全测）。

代码参考:

mysql 8.0: storage/innobase/include/fil0fil.h:1184

新增了不支持的类型:

'45be':u'R-tree Node',

'45bd':u'Tablespace SDI Index page'


## 用法
仓库地址: https://github.com/alexhe/py3_innodb_page_info
直接下载: curl https://github.com/alexhe/py3_innodb_page_info/blob/main/py3_innodb_page_info.py

首先 要安装python3，(MacOS 默认改为了python3了)

用法:

python py3_innodb_page_info.py xxx.ibd -v

- v 表示详细信息

```
$ python py3_innodb_page_info.py xxx.ibd -v
page_type =  0008
page offset 00000000, page type <File Space Header>
page_type =  0005
page offset 00000001, page type <Insert Buffer Bitmap>
page_type =  0003
page offset 00000002, page type <File Segment inode>
page_type =  45bd
page offset 00000003, page type <Tablespace SDI Index page>
page_type =  45bf
page offset 00000004, page type <B-tree Node>, page level <0000>
page_type =  45bf
page offset 00000005, page type <B-tree Node>, page level <0000>
page_type =  0000
page offset 00000000, page type <Freshly Allocated Page>
page_type =  0000
page offset 00000000, page type <Freshly Allocated Page>
Total number of page: 8:
File Space Header: 1
Insert Buffer Bitmap: 1
File Segment inode: 1
Tablespace SDI Index page: 1
B-tree Node: 2
Freshly Allocated Page: 2
```
