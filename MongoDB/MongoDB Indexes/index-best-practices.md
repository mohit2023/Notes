> **Remember ESR Rule**

Note: If there is a query to find all documents, basically .find({}), and I project only few fields, even if they are covered by an existing index, mongodb won't even consider a plan to use the index (unless you specifically hint mongodb to use an index). Basically here the empty query which does not match the prefix of any index.