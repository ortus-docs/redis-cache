---
description: Learn how to configure the extension for operation
---

# Configuration

Once the extension is installed, you can begin to create cache connections and configure them either via the administrator, via the Application.cfc or via a CFConfig json file.

## Admin Cache Connection

![](<../.gitbook/assets/image (7).png>)

To add a new cache, click on `Services > Cache` and you should see a list of existing caches. If there are no existing caches, you should be taken straight to the `create` screen.

![Creating a cache connection](<../.gitbook/assets/Screen Shot 2021-11-19 at 10.27.51 AM.png>)

You have two cache options with our extension:

* **Ortus Redis Cache** : For standalone or connecting to a single Redis instance
* **Ortus Redis Cluster Cache** : For connecting to a Redis Cluster

You will then be taken to a page of options for each of the Redis Cache implementations.

### RedisCache

<figure><img src="../.gitbook/assets/Single-Cache-Admin.jpg" alt=""><figcaption></figcaption></figure>

The `RedisCache` is used for connecting to a single instance of Redis. That instance could be replicated, but that's another story. Let's check out the different options:

#### Storage

Check the `Storage` box if you want to be able to use this cache for session or client storage distribution.

#### Host

Enter the Redis server IP address or host name.

#### Port

The port of the Redis server.

#### Logical Database

The logical database to connect to in Redis. By default we connect to database 0.

#### Username

The Redis cluster username - only used when enabling [user-level access](https://docs.redis.com/latest/rs/security/access-control/manage-users/add-users/).

#### Password

The password of the Redis server, if any.

#### SSL

Enable SSL on the connection to the Redis Server.

#### Connection Timeout

The time in milliseconds to wait for a connection or throw an exception.

#### Socket Timeout

The cluster connection socket timeout in milliseconds

#### Pool Timeout

The the maximum amount of time, in milliseconds, to wait for a connection pool resource to become available

#### Max Connections

The maximum number of connections to allow to the Redis server.

#### Idle Connections

The maximum number of idle connections to keep in the pool to the Redis server

#### Cache Key Prefix

The default key prefix is `lucee-cache`. This will automatically prefix EVERY single cache item that goes into Redis. This will allow you to avoid collisions if you decide to register many Lucee caches or just to distinguish what comes from which cache connection.

#### Cache Key Case Sensitivity

By default all cache keys are transformed to lowercase to avoid any casing issues. However, if you want case sensitivity, then turn this option on.

#### Default

This is a Lucee feature where you can set the cache connection to be the default for all cache operations in Lucee (cacheGet(), cachePut(), etc). This can be one of the following or none at all.

![](<../.gitbook/assets/image (5).png>)

### RedisClusterCache

<figure><img src="../.gitbook/assets/Cluster-Cache-Admin.jpg" alt=""><figcaption></figcaption></figure>

The `RedisClusterCache` is used for connecting to a cluster of Redis instances. This can be using Sentinel, or vanilla clustering or Redis Enterprise or Redis AWS/DigitalOcean. Let's check out the different options:

#### Storage

Check the `Storage` box if you want to be able to use this cache for session or client storage distribution.

#### Host(s)

Enter a comma-delimited list of all the IPs or hosts in the cluster. Not all are needed, but you should at least enter some to have redundancy.

#### Port

The port of the Redis cluster.

#### SSL

Whether SSL transport is enabled

#### Username

The Redis cluster username - only used when enabling [user-level access](https://docs.redis.com/latest/rs/security/access-control/manage-users/add-users/).

#### Password

The Redis cluster password

#### Connection Timeout

The time in milliseconds to wait for a connection or throw an exception.

#### Read Timeout

The timeout for a read of data from the cluster - defaults to the connection timeout

#### Socket Timeout

The cluster connection socket timeout in milliseconds

#### Pool Timeout

The the maximum amount of time, in milliseconds, to wait for a connection pool resource to become available

#### Max Connections

The  maximum number of connections to the cluster allowed per pool - defaults to 50

#### Idle Timeout

The max idle time, in milliseconds, for a connection to remain in the pool.

#### Max Idle Connections

The maximum number of concurrently idle connections to retain in the pool

#### Max Attempts

The maximum number of connection attempts to make to the cluster.

#### Cache Key Prefix

The default key prefix is `lucee-cache`. This will automatically prefix EVERY single cache item that goes into Redis. This will allow you to avoid collisions if you decide to register many Lucee caches or just to distinguish what comes from which cache connection.

#### Cache Key Case Sensitivity

By default all cache keys are transformed to lowercase to avoid any casing issues. However, if you want case sensitivity, then turn this option on.

#### Default

This is a Lucee feature where you can set the cache connection to be the default for all cache operations in Lucee (cacheGet(), cachePut(), etc). This can be one of the following or none at all.

![](<../.gitbook/assets/image (5).png>)\\

## Application.cfc Connections

You can also add cache connections via your `Application.cfc` and avoid using the admin. Just open your `Application.cfc` and create a section under the pseudo-constructor (before the first function)

### RedisCache

```javascript
this.cache.connections["sessions"] = {
  class: 'ortus.extension.cache.redis.RedisCache', 
  storage: true, 
  custom: {
		"host":"127.0.0.1",
		"port":"6379"
		"username" : "",
		"password":"",
		"database" : "0",
		"useSSL": false,
		"timeout" : 2000,
		"socketTimeout" : 2000,
		"poolWaittimeout" : 1000,
		"maxConnections": 1000,
		"idleConnections": 10,
		"keyprefix":"lucee-cache",
		"cacheKeyCaseSensitivity" : false
	}, 
	default: 'object'
};
```

Please refer to the previous section to find out about what the custom options mean.

### RedisClusterCache

```javascript
this.cache.connections[ "myClusterCache" ] = {
  class: 'ortus.extension.cache.redis.RedisClusterCache', 
  storage: true, 
  custom: {
	"hosts":"127.0.0.1",
	"port":"7000",
	"username" : "",
	"password":"",
	"useSSL" : "",
	"timeout" : 2000,
	"readTimeout" : 2000,
	"socketTimeout" : 2000,
	"poolWaittimeout" : 1000,
	"maxAttempts" : 10,
	"maxConnections": 1000, 
	"maxIdleTime" : 30000,
	"maxIdleConnections" : 20, 
	"keyprefix":"lucee-cluster",			
	"cacheKeyCaseSensitivity" : false
}, 
default: 'object'
};
```

## CFConfig Connections

You can also leverage a `cfconfig.json` file to store the cache configurations and automatically load them into your CFML server via CommandBox.

```javascript
{
    "adminPassword" : "redis",
    "systemErr":"System",
    "systemOut":"System",
    "applicationTimeout":"1,0,0,0",
    "cacheDefaultObject":"sessions",
    "caches":{
        "sessions": {
            "class":"ortus.extension.cache.redis.RedisCache",
            "custom":{
                "cacheKeyCaseSensitivity":"false",
                "database" : "0",
                "idleConnections":"5",
                "maxConnections":"50",
		"username":"${REDIS_USERNAME}",
                "password":"${REDIS_PASSWORD}",
                "timeout":"2000",
                "useSSL":"false",
                "host":"${REDIS_HOST:127.0.0.1}",
                "keyprefix":"lucee-cache",
                "port":"${REDIS_PORT:6379}"
            },
            "readOnly":"false",
            "storage":"true"
        },
	"rediscluster": {
            "class":"ortus.extension.cache.redis.RedisClusterCache",
            "custom":{
                "hosts":"${REDIS_CLUSTER_HOSTS:127.0.0.1}",
                "keyprefix":"lucee-cluster",
                "username" : "${REDIS_CLUSTER_USERNAME}",
                "password" : "${REDIS_CLUSTER_PASSWORD}",
                "port":"${REDIS_CLUSTER_PORT:7000}",
		"useSSL" :"${REDIS_CLUSTER_USE_SSL:false}"
            },
            "readOnly":"false",
            "storage":"true"
        }
    },
    "inspectTemplate":"always",
    "requestTimeout":"0,0,0,50",
    "sessionMangement":"yes",
    "sessionTimeout":"0,0,30,0"
}
```

Please refer to the previous section to find out about what the custom options mean.
