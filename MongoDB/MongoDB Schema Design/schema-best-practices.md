Each Index minimum size: **8KB**

Ideally you should never have more than **50** indexes per collection

Each Document size limit : **16MB**


### Relationship Types:

1. One to One   
(Put in same collection: embedd)

2. One to Many  
(Put an array of many side in the one side, can embedd the whole data of many side on one side or could just have the index if all details of many side data are not required with the one side data in a single query)

3. One to Squillions  
(Put reference of one side in the many side documents -> don't habve unbounded array)

4. Many to Many  
(Have array reference on both side to each other's side, or could embedd one of the sides into other sides documents but it would lead to duplication)



### General Rules

1. Embedd unless there is a compleiing reason not to
2. Avoid JOINS is they can be avoided, but not at the cost of better schema design
3. Never have unbounded array
4. Needing to access object on its own is a complelling reason not embed it.


> Design you schema based on the unique needs of your application -> the way to use data dicatates the schema design

Refer : <https://www.youtube.com/watch?v=J1RRM53I3kc&list=PL4RCxklHWZ9tB00Sh2nMftVIBaVG_-bmY&index=1>