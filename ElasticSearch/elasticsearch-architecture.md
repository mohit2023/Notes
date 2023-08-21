ElasticSearch(ES) is based on Lucene library. It is a distributed database management system. 

Data unit in ES is called Index (analogus to table in sql).  
Each Index is subdivided into shards. Each shard is a unit of lucene.  
This lucene is broken down into segments -> which is the collection of inverted index of each field.  
Look at each segment as a collection of some documents which stores them in a particular way to provides the search functionality over those documents.  
A segment is immutable. In case of updates the docuemnt is marked deleted in old segment and written into new segment.  

**Lucene Reopen** -> make data available for search -> but does not gurantee presence of data in disc.

**Lucene Commits** -> Data persisted in disc and also available for search -> resource expensive operation.

**Translog** -> All write operations in a shard are done on in-memory buffer and written in translog before acknowledgement -> used for shard recovery for acknowledged operations that are not committed.

**Refresh** -> The In-memory buffer in emptied and its content is written to newly created segment in the memory -> data is availbale for search -> by default happens every 1 second -> can be set by index.refresh_index property.

**Flush** -> in-memory buffer written to new segment and all in memory segments committed to disk -> both translog and in-memory buffer gets emptied

