---
description: Go funky with the Redis extension
---

# Direct Java API

If you need more power or are familiar with the Redis Java API and want to use some features we haven't implemented yet, first [let us know](mailto:support@ortussolutions.com) so we can consider that addition in future version, and then head over to the Java Cluster to get direct access to the Redis Java SDK. Behind the scenes our extension leverages the [Jedis](https://github.com/xetorthio/jedis) library for Redis.

We have created several global CFML functions to interact with Redis

* `redisGetProvider( [cachename=default] )` - Retrieves the underlying Ortus Cache implementation
* `redisGetConnectionPool( [cachename=default] )` - Retrieves the Jedis pool for a specific connection cache
* `redisGetCluster( [cachename=default] )` - Retrieves the Jedis cache cluster
* `redisGetNodes( [cachename=default] )` - Retrieves a struct of the Jedis pool connections to the cluster.

#### `RedisGetProvider()` <a href="#redisgetprovider" id="redisgetprovider"></a>

`RedisGetProvider()` returns an instance to the Java class that Ortus wrote that proxies between the Redis client and Lucee. It implements `lucee.commons.io.cache.Cache`. For the most part you probably won't need this class, but there are a few methods in the Lucee cache interface that aren't available to you via CFML. You can also dump the class and check out all of its functions.

```javascript
// Get the Ortus Java Provider for the default object cache
myProvider = RedisGetProvider();

// Get the Ortus Java Provider for the queryStorage cache
myProvider = RedisGetProvider( "queryStorage" );

// Get all keys in the cache as a java.util.List
keys = myProvider.keys();

// Get all the values in the cache as a java.util.List
values = myProvider.values();
```

#### `RedisGetConnectionPool()` <a href="#redisgetconnectionpool" id="redisgetconnectionpool"></a>

`RedisGetConnectionPool()` Returns access to a cache's Redis Connection Jedis Pool. It implements `redis.clients.jedis.JedisPool` - [https://github.com/xetorthio/jedis/blob/master/src/main/java/redis/clients/jedis/JedisPool.java](https://github.com/xetorthio/jedis/blob/master/src/main/java/redis/clients/jedis/JedisPool.java). This will give you direct access to the Jedis Pool connection for that cache.

```
pool = redisGetConnectionPool( 'sessions' );

// Get funky....
```
