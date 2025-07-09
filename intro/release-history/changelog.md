---
description: All notable changes to this project will be documented in this file.
---

# Changelog

## Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

***

### \[3.5.0] => 2025-JUL-09

#### Added

* Redis v8 Test Coverage and Compatibility
* Lucee 6 CI Matrix Test Coverage

#### Changed

* [LRE-63](https://ortussolutions.atlassian.net/browse/LRE-63) - Redis Client Library ( Jedis ) to v6.0.0

### \[3.4.1] => 2025-JUN-20

#### Added

* Lucee 6 Compatibility

### \[3.4.0] => 2024-DEC-04

#### Changed

* Redis Client Library ( Jedis ) to v5.2.0

#### Fixed

* Fixes connection release issues with distributed lock and Redis single-node mode

### \[3.3.2] => 2024-DEC-02

#### Fixed

* LRE-62 - Resolve issue where distributed lock connections were not being released

### \[3.3.1] => 2024-APR-03

#### Fixed

* Fixed cluster authentication being lost due to upstream java object close-with-resources behavior

### \[3.3.0] => 2024-FEB-15

#### Added

* Adds `cfredislock` and `redisLock` tags for tag-based and script syntax
* Adds `maxIdleConnections` and `maxIdleTime` configuration settings for Redis Cluster cache
* Adds getCache method to `RedisCacheUtils`

#### Fixed

* LRE-57 : Cluster cache commands was not closing the jedis pool on some operations

#### Updated

* Github actions to latest versions

### \[3.2.0] => 2023-NOV-25

#### Added

* Add settings for `poolWaitTimeout` and `socketTimeout` for RedisCache and RedisClusterCache connections

#### Changed

* Redis Client Library ( Jedis ) to v4.4.6
* Changed default max connections to 100 for initial reliability in HA deployments

### \[3.1.0] => 2023-SEP-11

#### Fixed

* Fixed unparseable date format by Lucee admin

### \[3.0.0] => 2023-JUL-19

#### Changed

* Converted extension build to Gradle OSGI Bundle
* Redis Client Library ( Jedis ) to v4.4.3

#### Added

* Added SSL and username support to RedisClusterCache configuration
* Added username support to RedisCache ( non-cluster ) configuration

### \[2.2.1] => 2022-APR-06

#### Fixed

* Fixes an issue with property file license activation

### \[2.2.0] => 2022-MAR-31

#### Added

* Added support for cluster password authentication
* Added cluster cache configuration for read timeouts
* Added cluster cache configuration for max number of pool connections

### \[2.1.0] => 2022-MAR-16

#### Fixed

* Fixes an issue with Cluster cache connections due to uninstantiated connection manager

#### Added

* Added support for environmental configuration of license variables
  * `REDIS_EXTENSION_EMAIL`
  * `REDIS_EXTENSION_LICENSE_KEY`
  * `REDIS_EXTENSION_SERVER_TYPE`
  * `REDIS_EXTENSION_ACTIVATION_CODE`
* Added support for an array of hostnames and ports to the configuration ( e.g. hosts=redis1.myhost.com,redis2.myhost.com port=6379,6377 )

### \[2.0.0] => 2022-AUG-05

#### Fixed

* [LRE-35](https://ortussolutions.atlassian.net/browse/LRE-35) cache filters for getting entries was not working
* [LRE-32](https://ortussolutions.atlassian.net/browse/LRE-32) getting all values/entries was not passing a built key, so return struct was always null
* [LRE-23](https://ortussolutions.atlassian.net/browse/LRE-23) LicenseHelper not validating all editions of similar product skus

#### Added

* [LRE-41](https://ortussolutions.atlassian.net/browse/LRE-41) Ability to choose which database to connect to in Redis, apart from 0 being the default
* [LRE-40](https://ortussolutions.atlassian.net/browse/LRE-40) Migration of docs to gitbook
* [LRE-39](https://ortussolutions.atlassian.net/browse/LRE-39) New redisSubscribe() so you can subscribe with closures/lambdas or CFCs to listen to Redis messages
* [LRE-38](https://ortussolutions.atlassian.net/browse/LRE-38) New redisPublish() UDF so you can publish messages into the Redis cluster
* [LRE-37](https://ortussolutions.atlassian.net/browse/LRE-37) New UDF redisGetClusterNodes() to get a map of cluster node objects
* [LRE-36](https://ortussolutions.atlassian.net/browse/LRE-36) Redis Cluster protocol support (RedisCluster, Sentinel, AWS, DigitalOcean)
* [LRE-33](https://ortussolutions.atlassian.net/browse/LRE-33) Redis publish and subscribe features
* [LRE-31](https://ortussolutions.atlassian.net/browse/LRE-31) New native cfml function: redisGetCluster() to get access to the native redis cluster manager
* [LRE-30](https://ortussolutions.atlassian.net/browse/LRE-30) Improve all exception handling to show exception messages
* [LRE-29](https://ortussolutions.atlassian.net/browse/LRE-29) Creation of a base class to share between cache implementations
* [LRE-28](https://ortussolutions.atlassian.net/browse/LRE-28) Add docker redis cluster support
* [LRE-27](https://ortussolutions.atlassian.net/browse/LRE-27) Update Jedis to 2.9.3
* [LRE-25](https://ortussolutions.atlassian.net/browse/LRE-25) Allow for a new setting to allow for case-sensitive mode instead of case-insensitive mode (default)

### \[1.4.0] => 2019-NOV-5

* `New Features`
  * Added a log4j bridge and custom appender so all log messages from the Redis library will not go out to the out logs in Lucee
* `Improvements`
  * Added all members of the `RedisConnection` class to be public/static so they can be inspected and reused
  * Added a `getConnectionKeys()` in the `RedisConnection` class to see which caches are configured and how
  * Added `RuntTimeExceptions and IOExceptions` whenever a Redis connection cannot be made to improve errors
  * Added more context when exceptions happen to the error messages
  * Converted all connection pool access to try's with resources for auto-closing and better code visibility
  * Coverted all `valueList()` and `entryLIst()` to leverage parallel streams for performance
* `Bugs`
  * Fixes an issue which caused the extension to fail on Lucee v5.2.9 and v5.3.x

### \[1.3.0] => 2019-SEP-30

* Added ability to set the following new settings on a cache connection:
  * Timeout
  * use SSL
  * Password
  * Max Connections
  * Max Idle Connections

### \[1.2.0] => 2019-MAR-05

* Init methods on the cache constructor are not static - https://ortussolutions.atlassian.net/browse/LRE-1
* Auto publishing
* S3 Publishing automated
* Added more verbose logging
* Added more logging for exception handling
* Major fix for session expirations when using session clusters with Lucee
* Removed tests source from final package to reduce binary size

### \[1.1.0] => 2018-JAN-16

* Minor fixes on Logging
