### Types of deployments

1. **Recereate Deployment**  
Put down all running instances -> then spin up all new instances (there is a downtime in b/w)

2. **Rolling Update**  
Put one instance down -> then roll up a new one (do this for all instance one after another untill all old instances are updated) -> at any time during the deployment, we have old instances as well as new instances running at same time

3. **Blue Green Deployments**    
Put all new instances up side by side to old instances, but while doing so all traffic should be routed to old instances only -> then once new instances are tested and up and running properly then switch traffic from old instances to the new ones (limited percentage of traffic can also be routed to it) -> then put down the old instances


### Useful Schema Patterns for Migration

1. **Polymorphic Pattern**  
Different type of data, maybe having different schemas can be present in same collection, ex: no need to have separate cat, dog collection, instead have one single Animnal collection.

2. **Schema Versoning Pattern**  
Have a field in document which mentions the version of the data -> usage handled in application side.

### Migration Techniques

1. **Async Migrations**    
Run migration job of data in background -> Eventual data consistency -> Eventual data availability

2. **On Demand Migrations (Lazy)**    
Migrate when data is accessed, check if data is in old version, then update it at that time and then return result. Consistent and highly available. Stale Data : If some data is not read then it won't get migrated
