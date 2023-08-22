- **Basic search query:**

```
GET /my-index-000001/_search
{
  "query": {
    "match": {
      "user.id": "kimchy"
    }
  }
}
```

**Example Output:**

```
{
  "took": 5,
  "timed_out": false,
  "_shards": {
    "total": 1,
    "successful": 1,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 1,
      "relation": "eq"
    },
    "max_score": 1.3862942,
    "hits": [
      {
        "_index": "my-index-000001",
        "_type": "_doc",
        "_id": "kxWFcnMByiguvud1Z8vC",
        "_score": 1.3862942,
        "_source": {
          "@timestamp": "2099-11-15T14:12:12",
          "http": {
            "request": {
              "method": "get"
            },
            "response": {
              "bytes": 1070000,
              "status_code": 200
            },
            "version": "1.1"
          },
          "message": "GET /search HTTP/1.1 200 1070000",
          "source": {
            "ip": "127.0.0.1"
          },
          "user": {
            "id": "kimchy"
          }
        }
      }
    ]
  }
}
```

By deafult top 10 documents matching the query are returned in the "hits.hits" property.  

The "took" property tells the time taken in milliseconds.  