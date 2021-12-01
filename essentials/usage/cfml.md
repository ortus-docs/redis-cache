# CFML

The first and easiest way to use your new cache is via the built-in cache functions and tags in CFML. You can specify the cache name to use, but by default Lucee will use the cache you have designated as your default `object` cache.

## **Caching Objects**

If you have selected your cache as the default `Object` cache in the admin, you can simply use functions like `cachePut()` and `cacheGet()`. Redis can handle arbitrary snippets of text (like HTML snippets) and even complex objects such as queries, arrays, or structs. The cache will automatically serialize the values and store them as text. They will be reconstituted when you retrieve them from the cache later.

```javascript
// Set a simple value into the default "object" cache for 2 days
cachePut( "key", "value", 2 );
// Get that value back
cacheGet( "key" );

// Set a value into a specific cache for 1 day
cachePut( "key", "value", 1, "myCacheName" );
// Get that value back
cacheGet( "key", "myCacheName" );

// Cache this array for 3 hours
cachePut( "myArray", [1,2,3,4,5], createTimeSpan(0,3,0,0) );
```

## **Caching Function Output**

Once you have selected a cache as the default `function` cache in the admin, you can use Redis to cache the results of oft-run functions. The cache key will be created for you automatically based on a hash of the method arguments thanks to Lucee. Cached functions should therefore be deterministic-- meaning the output of the function is purely a product of its parameters. Using function caching is easy, just add a `cachedwithin` attribute to the `cffunction` tag or function declaration.

```javascript
<!--- Cache results of this function for 5 minutes --->
<cffunction name="myFunc" cachedwithin="#createTimeSpan(0,0,5,0)#">
	<cfargument name="inputText">

	<cfreturn reverse(inputText)>
</cffunction>

<!--- First execution stores result in cache --->
<cfset result = myFunc("Brad Wood")>

<!--- subsequent call skips execution and pulls results from cache --->
<cfset result = myFunc("Brad Wood")>

<!--- Different parameters will create a new cache entry --->
<cfset result = myFunc("Luis Majano")>
```

This is what that function would look like in script

```javascript
function myFunc( inputText ) cachedwithin="#createTimeSpan(0,0,5,0)#" {
	return reverse(inputText);
}
```

{% hint style="danger" %}
**Important**: Lucee only supports caching functions that accept simple values as parameters. Therefore, a function that accepts an array would not be cacheable.
{% endhint %}

## **Caching Queries**

Once you have selected a cache as the default `query` cache in the admin, you can use Redis to cache the results of oft-run database queries. The cache key will be created for you automatically based on a hash of the SQL statement and its parameters thanks to Lucee. Using query caching is as easy as function caching, just add a cachedwithin attribute to your query.

```xml
<!--- Cache results of this query for 15 minutes --->
<cfquery datasource="datasourceName" name="qryTest" cachedwithin="#createTimeSpan(0,0,15,0)#">
	select *
	from [tableName]
</cfquery>
```

## **Per-application Cache Settings**

You can specify what caches are the default storage mechanism for functions, queries, objects, etc in the Lucee server and web administrator. There is one more programmatic level this can be configured as well.

The following settings are available in your `Application.cfc` to override at an application level. Remember, the "object" cache is used by default if no cache name is specified to functions such as `cachePut()` and `cacheGet()`.

You can also define an entire cache in your `Application.cfc` which makes your configuration completely portable.

```javascript
component{

	this.cache[ '<cache-name>' ] = {
		class  	= 'ortus.extension.cache.Redis.RedisCache',
		storage = false,
		custom={
			host = 'localhost',
			port = 6379,
			keyprefix = "lucee-prefix"
		}
	};

	this.cache.function="<cache-name>";
	this.cache.query="<cache-name>";
	this.cache.object="<cache-name>";
	this.cache.resource="<cache-name>";
	this.cache.template="<cache-name>";
}
```
