title: Elasticsearch的文本字段解析
date: 2020-01-08 13:15:00
tags:
---

年前读了一本书叫Elastic Search Definitive Guide，由于书的内容太老了，看完才发现很多内容都在新版本里已经不支持了，于是捧着文档又重新看了一下。 在老版本里，文本字段类型只有一种，叫做string。对于设置是否要分词，需要设置"analyzed"属性，在新版本里以及改成了两种不同的文本字段，一种是string, 一种是keyword。对于自动生成的mapping，文本类型的字段会默认映射成 "text"，同时也会生成一个subfield, xxx.keyword，他的类型会是keyword。 这样做的好处是各种use cases都支持了。
