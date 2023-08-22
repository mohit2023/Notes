### Steps setup elastic search locally using docker:

```
docker network create elastic
```

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.17.12
```

```
docker run -d --name es-quick-learn --net elastic -p 127.0.0.1:9200:9200 -p 127.0.0.1:9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.17.12
```

Port 9200 is used for http communication with elasticsearch's REST api, port 9300 is used for internal communication between nodes of a cluster.  

To stop or start the docker conianer run :

```
docker stop es-quick-learn
```

```
docker start es-quick-learn
```

### Steps to setup kibana using docker: 

```
docker pull docker.elastic.co/kibana/kibana:7.17.12
```

```
docker run -d --name kibana-quick-learn --net elastic -p 127.0.0.1:5601:5601 -e "ELASTICSEARCH_HOSTS=http://es-quick-learn:9200" docker.elastic.co/kibana/kibana:7.17.12
```

Note: The env in above docker run command requires to use the correct name of running elastic search container running.  


### Cleanup docker setup:

```
docker stop es-quick-learn 
```  

```
docker stop kibana-quick-learn  
```

```
docker network rm elastic  
```

```
docker rm es-quick-learn  
```

```
docker rm kibana-quick-learn  
```


## Elastic Search Queries:

- **To get all indexes**

```
GET _cat/indices?v
```

The "v" parameter is used to include column headers in returned data to make it more readable.

- **To get all documents of an index**

```
GET /.geoip_databases/_search
{
  "query": {
    "match_all": {}
  }
}
```

or in short:

```
GET /.geoip_databases/_search
```

- **To get all index templates**

```
GET /_index_template
```

- **To get index template with given name (accepts wild card expressions)**

```
Get /_index_template/template-name
```

- **To insert document**

```
POST index-name/_doc
{
    "key1": "value1",
    "key2": {"ob_key2_1": "ob_value2_1"}
}
```

```
POST logs-my_app-default/_doc
{
  "@timestamp": "2099-05-06T16:21:15.000Z",
  "event": {
    "original": "192.0.2.42 - - [06/May/2099:16:21:15 +0000] \"GET /images/bg.jpg HTTP/1.0\" 200 24736"
  }
}
```

Because in elasticseaarch there is a default index mappings with pattern logs-*-*, and that mapping defines the index to be a data_stream, hence above will form a data_stream instead of a regular index.

- **Bulk write**

```
PUT logs-my_app-default/_bulk
{ "create": { } }
{ "@timestamp": "2099-05-07T16:24:32.000Z", "event": { "original": "192.0.2.242 - - [07/May/2020:16:24:32 -0500] \"GET /images/hm_nbg.jpg HTTP/1.0\" 304 0" } }
{ "create": { } }
{ "@timestamp": "2099-05-08T16:25:42.000Z", "event": { "original": "192.0.2.255 - - [08/May/2099:16:25:42 +0000] \"GET /favicon.ico HTTP/1.0\" 200 3638" } }
```

All bulk data must be newline-delimited JSON

- **Search data**

```
GET logs-my_app-default/_search
{
  "query": {
    "match_all": { }
  },
  "sort": [
    {
      "@timestamp": "desc"
    }
  ]
}
```

"_source" field contains the original document.


- **Project specific field in searching data, there are two ways:**

```
GET logs-my_app-default/_search
{
  "query": {
    "match_all": { }
  },
  "_source": ["event.etc"],
  "sort": [
    {
      "@timestamp": "desc"
    }
  ]
}
```

The below method where we mark "_source": false is deprecated:
```
GET logs-my_app-default/_search
{
  "query": {
    "match_all": { }
  },
  "fields": [
    "event.etc"
  ],
  "_source": false,
  "sort": [
    {
      "@timestamp": "desc"
    }
  ]
}
```

- **To delete data stream:**

```
DELETE _data_stream/logs-my_app-default
```

- **To delete index:**

```
DELETE /index-name
```
