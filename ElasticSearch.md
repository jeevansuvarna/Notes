# ElasticSearch

### Install ES

https://www.elastic.co/guide/en/elasticsearch/reference/current/install-elasticsearch.html


# Index:

Elasticsearch stores its data in one or more indices. Taking SQL as references, indexing is similar to a database. It is used to store the documents which consists of fields and read them. As said before Elasticsearch use Apache Lucene Library to write and read the data from the index. Elastic search index may be built of more than a single Apache Lucene Index by using “Shards”.


### Document:
Document is the main part in the Elastic search. Elastic search is all about searching and analyzing these documents. Document consists of fields, and each field identified by its name and can contain one or more values. Since it’s in JSON, it doesn’t have any structure which means each document may have different set of fields.


### Type:
Each document in Elasticsearch has its type defined. This allows us to store various documents types in one index and different mapping for different documents types.


### Mapping:
All documents are analyzed before being indexed. The input text is divided into tokens and later the tokens are filtered out or some additional processing is done such as stemming, case conversion, ngrams and so on.


### Cluster:
Cluster is a set of Elastic search nodes that works together. The distributed nature of Elasticsearch allows us to easily handle data that is too large for single node to handle. Node is referred as the single instance of the Elasticsearch server is called a node.


### Shards:
As said earlier, clustering helps in storing information volumes that exceed abilities of a single server. To achieve this Elasticsearch spreads data to several physical Lucene indices these indices are called Shards.

### Replica:
Sharding helps in pushing more data into Elasticsearch that is possible for a single node to handle. The idea is simple create an additional copy of shard, what can be used for queries just as original, primary shard.


# create index

```elasticsearch
PUT /employees
```


# Mapping

Mapping is the process that define how a document and fields it contains are stored and indexed. Each document is a collection of fields, in which each have their own data type. When mapping the data, we create a mapping definition, which contains a list of fields that are relevant to the document.

```
PUT "localhost:9200/employee/_mapping
{
  "mappings": {
    "properties": {
      "age":    { "type": "integer" },  
      "email":  { "type": "keyword"  }, 
      "name":   { "type": "text"  }     
    }
  }
}
```


# Text analysis

Text analysis is the process of converting unstructured text, like the body of an email or a product description, into a structured format that’s optimized for search.

## Tokenization
Analysis makes full-text search possible through tokenization: breaking a text down into smaller chunks, called tokens. In most cases, these tokens are individual words.

If you index the phrase the quick brown fox jumps as a single string and the user searches for quick fox, it isn’t considered a match. However, if you tokenize the phrase and index each word separately, the terms in the query string can be looked up individually. This means they can be matched by searches for quick fox, fox brown, or other variations.


## Normalization 
Tokenization enables matching on individual terms, but each token is still matched literally. This means:

A search for Quick would not match quick, even though you likely want either term to match the other
Although fox and foxes share the same root word, a search for foxes would not match fox or vice versa.
A search for jumps would not match leaps. While they don’t share a root word, they are synonyms and have a similar meaning.
To solve these problems, text analysis can normalize these tokens into a standard format. This allows you to match tokens that are not exactly the same as the search terms, but similar enough to still be relevant. For example:

* ``` Quick ``` can be lowercased: ```quick``.
* ```foxes``` can be stemmed, or reduced to its root word: ```fox```.
* ```jump ```and ```leap``` are synonyms and can be indexed as a single word: ```jump```.

## Customized Analyser

Text analysis is performed by an analyzer, a set of rules that govern the entire process.

Elasticsearch includes a default analyzer, called the standard analyzer, which works well for most use cases right out of the box.

If you want to tailor your search experience, you can choose a different built-in analyzer or even configure a custom one. A custom analyzer gives you control over each step of the analysis process, including:

* Changes to the text before tokenization
* How text is converted to tokens
* Normalization changes made to tokens before indexing or search



### Mapping and Analyser

```
PUT employee
{
  "settings": {
    "analysis": {
      "analyzer": {
        "std_folded": { 
          "type": "custom",
          "tokenizer": "standard",
          "filter": [
            "lowercase",
            "asciifolding"
          ]
        }
      }
    }
  },
  "mappings": {
    "properties": {
      "my_text": {
        "type": "text",
        "analyzer": "std_folded" 
      }
    }
  }
}
```

# Search Text

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


# DSL Query

Refer
https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html
