# introduction
## ES 是什么？
1、全文搜索引擎
2、一个分布式的实时文档存储，每个字段 可以被索引与搜索
3、一个分布式实时分析搜索引擎
4、能胜任上百个服务节点的扩展，并支持 PB 级别的结构化或者非结构化数据

## 相关资料网址：
lucene:    https://lucene.apache.org/core/
代码库：     https://github.com/elastic/elasticsearch
讨论区：     https://github.com/elastic/elasticsearch/blob/master/CONTRIBUTING.md
错误报告：   https://discuss.elastic.co

## 面向文档：【直接序列化对象/使用json描述对象】
【使用关系型数据库的行和列存储，这相当于是把一个表现力丰富的对象塞到一个非常大的电子表格中：为了适应表结构，
你必须设法将这个对象扁平化—​通常一个字段对应一列—​而且每次查询时又需要将其重新构造为对象。】

Elasticsearch 是 面向文档 的，意味着它存储整个对象或 文档。
Elasticsearch 不仅存储文档，而且 索引 每个文档的内容，使之可以被检索。
在 Elasticsearch 中，我们对文档进行索引、检索、排序和过滤—​而不是对行列数据。
这是一种完全不同的思考数据的方式，也是 Elasticsearch 能支持复杂全文检索的原因。

ES使用 JavaScript Object Notation（或者 JSON）作为文档的序列化格式。
并且已经成为 NoSQL 领域的标准格式。 它简单、简洁、易于阅读。




