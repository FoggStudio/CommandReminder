[<- Home](README.md)

# ElasticSearch
## Informations
By default ElasticSearch will be on port 9200 and Kibana on port 5601.
ElasticSearch will open an another port on 9300 for his own cluster communication.
If multiple nodes are open, you can access the REST API by the ports between 9200-9300 and the nodes communicates using ports from 9300 to 9400.

Elastic query types : 
 - **bool** : The default and most-used query type. Used for combining query clauses.
 - **dis_max** : A query which accepts multiple queries, and returns any documents which match any of the query clauses.
 - **constant** : All matching documents are given the same “constant” _score.
 - **range** : Returns documents that contain terms within a provided range. Parameters: gt,gte,lt,lte,format.
 - **match**: The standard query for performing full text queries, including fuzzy matching and phrase or proximity queries.
 - **multi_match**: The multi-field version of the match query.
 - **wildcard** : Returns documents that contain terms matching a wildcard pattern.
 - **regexp** : Returns documents that contain terms matching a regular expression.
 - **fuzzy** : Returns documents that contain terms similar to the search term.

Elastic clauses to combine in bool queries:
 - **must** : Is like the AND boolean operator. It will return only items that match EVERY sub-queries.
 - **should** : Is like the OR boolean operator. It will return every items that match ONE sub-queries.
 - **should_not** : Is like the NOR boolean operator. It will return items that match ANY sub-queries.
 - **must_not** : Is like the NAND boolean operator. It will return items that doesn't match ONE OF sub-queries.
 - **filter** : Works like must but scoring is ignored and clauses are considered for caching.
 
## Backup index
First get repositories with: 
```json
GET _snapshot
```
Then save indices you need:
```json
PUT _snapshot/oneOfTheRepositories/nameOfSnapshot
{
  "compressed":true,
  "indices": "indice",
  "include_global_state": false
}
```
Go in folder referenced as location path and zip it.

Then create repository on local machine and unzip data in it.

Restore with POS command:
```json 
POST _snapshot/Backup/statisticbackup/_restore
{
  // options see : https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-restore-snapshot.html
}

```

## Increase max mapping fields

```json
PUT indexName/_settings
{
  "settings": {
    "index.mapping.total_fields.limit": 2000
  }
}
```

## Copy index to a new one 

```json
POST _reindex
{
  "source": {
    "index": "my-index"
  },
  "dest": {
    "index": "my-new-index"
  }
}
```

## Get all from an index

```json
GET indexName/_search
{
  "query": {
    "match_all": {}
  }
}
```

## Delete data from an index

```json
POST indexName/_delete_by_query
{
  "query": {
    "bool": {
      "must": [
        {"match": {
          "property": "value"
        }}
      ]
    }
  }
}
```