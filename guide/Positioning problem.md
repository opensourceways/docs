如何获取时间段内的日志信息：

1.安装elasticdump

```
  npm install elasticdump -g
```

2.执行命令获取elasticsearch数据表（logstash-2020.07.01）时间段内指定参数日志到本地（/root/zj/test.json）文件

```
  NODE_TLS_REJECT_UNAUTHORIZED=0 elasticdump --input=https://user:password@127.0.0.1:9200 --input-index=logstash-2020.07.01 --output=/root/zj/test.json  --searchBody '{"query": {"bool": {"must": [{"range": {"@timestamp": {"time_zone":"+00:00","gte":"2020-07-01T14:20:46","lte": "2020-07-01T14:21:46"}}},{"term":{"kubernetes.labels.app.keyword": "openeuler-hk-ingress"}}]}}}' --type=data
```
