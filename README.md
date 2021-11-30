---
description: >-
  The Ortus Redis Extension is a native Lucee Extension that allows your CFML
  server to connect to a Redis or a Redis Cluster and leverage it for built-in
  caching, session storage, Pub/Sub Messaging, an
---

# Introduction

## Ortus Redis Extension

The Ortus Redis Extension is a \*\*native\*\* Lucee Extension that allows your CFML server to connect to a Redis server or a Redis Cluster and leverage it for built-in caching, session storage, Pub/Sub Messaging, and document storage.

> Redis is an open source (BSD licensed), in-memory data structure store, used as a database, cache and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries. Redis has built-in replication, Lua scripting, LRU eviction, transactions and different levels of on-disk persistence, and provides high availability via Redis Sentinel and automatic partitioning with Redis Cluster. [Learn More](https://redis.io/topics/introduction)

### Requirements

* Lucee 5.1.0 and above
* Redis 4.0.X and above

### Features In A Nutshell

* Add Redis native functionality to any Lucee server
* Install at server level (Available to all contexts)
* Create Cache connections in the Lucee web administrator or via `Application.cfc` to connect to any network-accessable Redis cluster
* Set and get objects from Redis via standard CFML functions and tags (`cachePut(), cacheGet(), cfcache action="get|put"`)
* Fully supports all built-in Lucee cache functions including wildcard filters
* Seamlessly distribute storage of the following to any Redis Cluster
  * Lucee session storage
  * Lucee client storage
  * Lucee Ram resouces (ram://...)
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
