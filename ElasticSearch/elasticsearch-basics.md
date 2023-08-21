Elasticsearch(ES) indexes all data in each field using an optimized datastructure by default.  
test fields -> inverted indices  
numeric and geo fields -> BKD trees  

When dynamic mapping is enabled, ES automatically detects and adds new fields to the index with their appropriate data types.  
We can also define our own mappings.  
geo_point and geo_shape cannot be automatically detected.  

Same field can be indexed in multiple ways, eg: a string field can be indexed as text-field for full-text search and as keyword field for sorting and aggregation operations.

General rule to avoid gazillion shards problem -> number of shards per GB of heap space should be less than 20, and average shard size should be between few GB to few tens of GB.  

**Architecture basics:**  

Cluster -> have multiple nodes(servers)  
Index -> divided into shards  
Shards -> primary and replica    
One shard -> lives inside one node (can not be divided into multiple nodes)  
Though one node can contain multiple shards  

Cross cluster replication(CCR) -> synchronize indices from primary cluster to a secondary remote cluster that can work as a backup when primary cluster fails. CCR can also be used to create secondary clusters to serve read-requests in geo-proximity. Writes are done only on primary cluster.

