---
description: Use Redis as a virtual file storage
---

# RAM Resources

Lucee has the concept and feature of virtual file systems. Our extension taps into it by allowing you to leverage the [`ram://`](ram://) resource to talk to Redis for storing documents and treating Redis like a big file system. This means that any `file` or `directory` related tag/function can work with a Redis RAM resource like: `fileRead(), fileWrite(), fileDelete(), directoryNew(), directoryList(), include`, etc. It even works when defining application mappings. You can define Redis to be the default cache for `resources` by selecting the `default` element in the cache details page and pointing it to `resource`.

{% hint style="danger" %}
**Important**: Please note that Lucee only allows you to determine 1 cache connection to be the default for either object, template, query, resource or function caching. You might end up creating different cache connections if you want to leverage them as **default** cache locations.
{% endhint %}

Once you setup Redis to be your default `resource` cache you can leverage it in many ways:

```javascript
// Create a mapping to it
this.mappings[ "/cluster-fs" ] = "ram://";


// Do some file operations
fileWrite( "/cluster-fs/suzi.txt", myContent );
include template="/cluster-fs/aop.cfm";
directoryList( "/cluster-fs/caches" );
```
