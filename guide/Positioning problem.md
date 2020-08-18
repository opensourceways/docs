如何获取时间段内的日志信息：

1.安装npm
参考[安装文档](https://itsfoss.com/install-nodejs-ubuntu/)

```
sudo apt install nodejs
sudo apt install npm
npm -v
```


2.安装elasticdump

```
  npm install elasticdump -g
```

2.执行命令获取elasticsearch数据表（logstash-2020.07.01）时间段内指定参数日志到本地（/root/zj/test.json）文件

参数含义：

 * --input  表示elasticsearch数据库的链接，如果有用户名按照user:password@格式加在中间
 * --input-index 表示elasticsearch数据库的表名称，通常为logstash-加时间，比如logstash-2020.07.01
 * --output  为导出的日志存放的本地绝对路径，文件名可自己定义
 * --searchBody 为导出数据库数据的过滤条件

  ** time_zone 表示时区，北京时间为+08:00
  ** gte，lte   选择时间范围为   gte> your_want_time > lte.
  ** term  为过滤条件，key，value的形式，此处为"kubernetes.labels.app.keyword": "openeuler-hk-ingress"

```
  NODE_TLS_REJECT_UNAUTHORIZED=0 elasticdump --input=https://user:password@127.0.0.1:9200 --input-index=logstash-2020.07.01 --output=/root/zj/test.json  --searchBody '{"query": {"bool": {"must": [{"range": {"@timestamp": {"time_zone":"+00:00","gte":"2020-07-01T14:20:46","lte": "2020-07-01T14:21:46"}}},{"term":{"kubernetes.labels.app.keyword": "openeuler-hk-ingress"}}]}}}' --type=data
```
