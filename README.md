# elasticsearch

```js
  elasticsearch: 
  1.基于lucene全文搜索引擎.
  2词汇：term:  analysis： index： type： document：{_index, _type, _id, _source}一条数据记录， mapping. 
  3.索引操作 ： curl -x  put/delete ‘lcoalhost:9200/weather(索引名，相当于表)’ 
  4.操作记录: curl -x put ‘lcoalhost:9200/weather/person（type）/1（id） -d’ 查看/删除/更新（put） 
  5.搜索： term content(搜索词也进行分词)
  6.

```
