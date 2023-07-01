# py3_innodb_page_info

## 来源
forked from https://github.com/happieme/py_innodb_page_info

the old code can only supported by python2;

current code supported python 3.10

python tool for innodb page info   

原来仓库代码 (https://github.com/happieme/py_innodb_page_info) 很久没更新了，只支持python2。

本代码基于现在主流的python3（我环境是python 3.10)修改而成。

如果有其它语法不支持，也是少数，简单修改即可。

针对MySQL 8.0代码改造，

代码参考:

mysql 8.0: storage/innobase/include/fil0fil.h:1184

新增了不支持的类型:

'45be':u'R-tree Node',

'45bd':u'Tablespace SDI Index page'


## 用法
首先 要安装python

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
