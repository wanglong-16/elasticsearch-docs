# curl
## 一、使用curl命令和es 交互模版：
curl -X<VERB> '<PROTOCOL>://<HOST>:<PORT>/<PATH>?<QUERY_STRING>' -d '<BODY>'

## 二、使用curl命令和es交互命令举例：


#### 1、添加索引数据
curl -XPUT 'http://39.106.228.247:9200/twitter/user/kimchy?pretty' -H 'Content-Type: application/json' -d '{ "name" : "Shay Banon" }'

curl -XPUT 'http://39.106.228.247:9200/twitter/tweet/1?pretty' -H 'Content-Type: application/json' -d '
{
    "user": "kimchy",
    "post_date": "2009-11-15T13:12:00",
    "message": "Trying out Elasticsearch, so far so good?"
}'

curl -XPUT 'http://39.106.228.247:9200/twitter/tweet/2?pretty' -H 'Content-Type: application/json' -d '
{
    "user": "kimchy",
    "post_date": "2009-11-15T14:12:12",
    "message": "Another tweet, will it be indexed?"
}'

#### 2、查看数据
curl -XGET 'http://39.106.228.247:9200/twitter/user/kimchy?pretty=true'
curl -XGET 'http://39.106.228.247:9200/twitter/tweet/1?pretty=true'
curl -XGET 'http://39.106.228.247:9200/twitter/tweet/2?pretty=true'

#### 3、搜索数据

curl -XGET 'http://39.106.228.247:9200/twitter/tweet/_search?q=user:kimchy&pretty=true'

curl -XGET 'http://39.106.228.247:9200/twitter/tweet/_search?pretty=true' -H 'Content-Type: application/json' -d '
{
    "query" : {
        "match" : { "user": "kimchy" }
    }
}'

curl -XGET 'http://39.106.228.247:9200/twitter/_search?pretty=true' -H 'Content-Type: application/json' -d '
{
    "query" : {
        "match_all" : {}
    }
}'

curl -XGET 'http://39.106.228.247:9200/twitter/_search?pretty=true' -H 'Content-Type: application/json' -d '
{
    "query" : {
        "range" : {
            "post_date" : { "from" : "2009-11-15T13:00:00", "to" : "2009-11-15T14:00:00" }
        }
    }
}'

#### 4、修改索引setting配置

curl -XPUT 'http://39.106.228.247:9200/another_user?pretty' -H 'Content-Type: application/json' -d '
{
    "index" : {
        "number_of_shards" : 1,
        "number_of_replicas" : 1
    }
}'


#### 5、修改索引mapping配置, 添加动态列 【指定索引/类型】

curl -XPOST 'http://192.168.2.13:29200/dmp-customer-portrait-20210708.2/data_filter/_mapping?pretty' -H 'Content-Type:application/json' -d '
{"data_filter":{"properties":{"must_not_loss":{"type":"integer","doc_values" : false}}}}'

#### 6、通过文档ID更新文档字段 【局部更新】

curl -XPOST 'http://192.168.2.13:29200/dmp-customer-portrait-20210708.2/data_filter/731891/_update' -H 'Content-Type:application/json' -d '{"doc":{"must_not_loss": 1}}'

#### 7、删除索引

curl -XDELETE 'http://39.106.228.247:9200/twitter'


#### 8、查看集群信息

6.1 查看节点
curl -X GET "http://39.106.228.247:9200/_cat/nodes?v&pretty"

6.2 查看分片
curl -X GET "http://39.106.228.247:9200/_cat/shards?pretty"

6.3 查看索引
curl -X GET "http://39.106.228.247:9200/_cat/indices?pretty"



