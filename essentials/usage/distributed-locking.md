---
description: >-
  Introduced in version 3.3.0, the <cfRedisLock>  tag offers distributed locking
  for clustered instances.
---

# Distributed Locking

In clustered environments, it is often necessary to prevent multiple instances from executing methods at the same time, thus preventing collisions with data access and modificication.  The `<cfRedisLock>` tag ( `redisLock` in script ) allows the user to place a lock across all running instances in the cluster.

The tag functions exactly like `cflock/lock` with the exception of the `cache` and `bypass` arguments.  The the `bypass` argument can be useful in development environments when not using a distributed cache.

### Tag Usage

```
<cfRedisLock
    name="[ the name of the lock to place ]"
    cache="[ the configured redis cache to use for locking ]"
    throwOnTimeout="[ Defaults to true, whether to throw on failure to lock]"
    expires="[the max duration of the lock entry to exists in seconds - default 60s]"
    timeout="[the max time to wait for a lock to be acquired - default 2s]"
    bypass="[optional - if true will bypass the attempt to lock completely]"
>
.... do locked stuff here ...
</cfRedisLock>
```

### Script Usage

```
redisLock
    name="[ the name of the lock to place ]"
    cache="[ the configured redis cache to use for locking ]"
    throwOnTimeout="[ Defaults to true, whether to throw on failure to lock]"
    expires="[the max duration of the lock entry to exists in seconds - default 60s]"
    timeout="[the max time to wait for a lock to be acquired - default 2s]"
    bypass="[optional - if true will bypass the attempt to lock completely]"
{
.... do locked stuff here ...
}
```
