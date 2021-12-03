---
description: >-
  The Ortus Redis Extension is a native Lucee Extension that allows your CFML
  server to connect to a Redis or a Redis Cluster and leverage it for built-in
  caching, session storage, Pub/Sub Messaging, and document storage.
---

# Introduction

## Ortus Redis Extension v2.x Docs

![](.gitbook/assets/redis-lucee-logo.png)

The [Ortus Redis Extension](https://www.ortussolutions.com/products/redis-lucee) is a **native** Lucee Extension that allows your CFML server to connect to a Redis server or a Redis Cluster and leverage it for built-in caching, session storage, Pub/Sub Messaging, and document storage.

> Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperlogs and geospatial indexes with radius queries. Redis has built-in replication, Lua scripting, LRU eviction, transactions and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster. [Learn More](https://redis.io/topics/introduction)

### Requirements

* Lucee 5.1.0 and above
* Redis Standalone or Cluster 4.0.X and above

### Commercial Product

This Lucee extension is a commercial product by Ortus Solutions.  You will need to purchase a license: [https://www.ortussolutions.com/products/redis-lucee](https://www.ortussolutions.com/products/redis-lucee).

### Features In A Nutshell

* Add Redis native functionality to any Lucee server
* Install at server level (Available to all contexts)
* Create Cache connections in the Lucee web administrator or via `Application.cfc` to connect to any network-accessible Redis cluster
* Set and get objects from Redis via standard CFML functions and tags (`cachePut(), cacheGet(), cfcache action="get|put"`)
* Fully supports all built-in Lucee cache functions including wildcard filters
* Seamlessly distribute storage of the following to any Redis Cluster
  * Lucee session storage
  * Lucee client storage
  * Lucee Ram resources (ram://...)
* Seamlessly cache the following to any timeout-sensitive Redis key
  * Results of database queries
  * Results of deterministic functions
  * Complex or simple objects in your application's code
  * Cached templates (`cfcache action="content|cache|serverCache"`)
* Extremely lightweight and fast
* Ability to publish and subscribe to Redis channels for pub/sub capabilities: https://redis.io/topics/pubsub
* Native Redis functions:
  * `RedisGetCluster( cacheName )`
  * `RedisGetClusterNodes( cacheName )`
  * `RedisGetConnectionPool( cacheName )`
  * `RedisGetProvider( cacheName )`
  * `RedisPublish( channel, message, cacheName )`
  * `RedisSubscribe( subscriber, channels, cacheName )`

### Support

The Ortus Redis Extension is a commercial product by Ortus Solutions. If you have purchased a license then you are entitled to customer support.  You can either visit our support page to contact us or create an issue in our bug tracker.

* Support Page: [https://www.ortussolutions.com/services/support](https://www.ortussolutions.com/services/support)
* Bug Tracker: [https://ortussolutions.atlassian.net/browse/LRE](https://ortussolutions.atlassian.net/browse/LRE)
