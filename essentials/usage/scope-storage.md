---
description: Use Redis for session distribution
---

# Scope Storage

Lucee will allow you to seamlessly defer storage of your **session** and/or **client** scopes to Redis. You will set and access the scopes like you normally would in CFML, but behind the scenes Lucee stores a cache entry for each user containing their session/client variables in the Redis cluster.

This serves several purposes:

* Scopes are persisted across server restarts
* Lower memory usage since variables are **NOT** stored in the JVM's heap
* User sessions can be shared across web servers (**No more sticky sessions**)
* Redis cluster can be scaled out to handle whatever amount of users you need in a distributed fashion

This means you could take your single-server application with a heavy dependence on session/client variables, and scale it out to as many web servers as necessary behind a round-robin load balancer. Users are free to roam to any web server they want, and their session variables will follow them anywhere with no extra overhead. Perhaps you have millions of web site visitors and you're running out of heap space due to all the session storage. Push those sessions off to a distributed Redis layer that can scale out to meet demand, and that is no longer a bottleneck.

### Storage Option

For both session and client storage, you will need to check the `Storage` box when creating or editing the cache connection you want to use in the Lucee admin. Remember you can create multiple buckets in Redis to help manage your documents and segregate RAM.

![Storage Option](http://127.0.0.1:49339/docs/includes/shots/storage.png)

Set a cache as usable for `session` or `client` storage

### **Session**

Once the cache is created, enabling session storage is easy. In your Application.cfc simply confirm `sessionManagment` is turned on and set the following two settings as well in the `this` scope:

* `sessionType` : This is the type of session to use, valid values are `cfml` and `j2ee`. Make sure that you select `cfml` or the extension will NOT work.
* `sessionStorage` : This is the name of the cache defined in your Lucee administrator that you wish to store sessions in
* `sessionCluster` : This controls how/when session data is sent and retrieved from the cache.
  * `true`: Session data is primarily stored in cache. It is always pulled from the cache at the start of each request, and backed up at the end. Use this setting if you have multiple applications using cached storage and you want the full benefit of distributed sessions.
  * `false`: Session data is primarily stored in memory but backed up on every request to the cache. Session data is only pulled from the cache if it doesn't exist in memory. Set this to false if you only have one application using session cache storage and you simply want to persist session storage across restarts.

```javascript
component{
	this.name = "myApp";

	this.sessionType = "cfml";
	this.sessionManagement = true;
	this.sessionTimeout = createTimeSpan(0,0,30,0);

	// This is the name of the Redis cache to use
	this.sessionStorage = "SessionStorageCache";
	// Set this to true if you have more than 1 application
	this.sessionCluster = true;
}
```

{% hint style="danger" %}
**Important**: Make sure your session type is set to **cfml** or our extension will NOT work.
{% endhint %}

### **Client**

Storing your client scope in Redis is just as easy as session storage. In your Application.cfc confirm `clientManagement` is turned on and set the following two settings in the `this` scope:

* `clientStorage`: This is the name of the cache defined in your Lucee administrator that you wish to store client data in
* `clientCluster`: This controls how/when client data is sent and retrieved from the cache.
  * `true`: Client data is primarily stored in cache. It is always pulled from the cache at the start of each request, and backed up at the end. Use this setting if you have multiple applications using cached storage and you want the full benefit of distributed client data.
  * `false`: Client data is primarily stored in memory but backed up on every request to the cache. Client data is only pulled from the cache if it doesn't exist in memory. Set this to false if you only have one application using client cache storage and you simply want to persist client storage across restarts.

```javascript
component{
	this.name = "myApp";

	this.clientManagement = true;
	this.clientTimeout = createTimeSpan(25,0,0,0);

	// This is the name of the Redis cache to use
	this.clientStorage = "CientStorageCache";
	// Set this to true if you have more than 1 application
	this.clientCluster = true;
}
```
