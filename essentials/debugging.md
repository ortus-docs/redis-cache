---
description: Issues? We all have them, learn how to cope with them
---

# Debugging

Here's a general list of troubleshooting steps if you're getting errors. The log files are VERY important since the error Lucee throws doesn't always contain the information you need. You will have to crack open your Lucee logs to get the actual error out.

* Look in the "out" and "err" logs for information. These are usually found in the servlet container's log directory. For instance, if you're using Tomcat, look in Tomcat's log directory. There are often messages logged there that never make it up to the CFML engine.
* The Log4J output of the underlying Redis Java SDK will be redirected to your Lucee server's "Application" log. Adjusting the logging level for this log will affect how much information you get from Redis.
* Always scroll to the bottom of Java stack traces to look for a "caused by" section which is the original error.
* If you are getting connection errors or Null pointer exceptions, check the spelling of your hostnames and ports and make sure Redis is actually running with the bucket name you specified in the config.
* Once the library connects, you should see lines in the "out" log showing the servers being connected to successfully.
* Open up the Redis web admin on one of your nodes and watch the "Ops per second" graph while you hit your app. If you see spikes in the graph every time you hit the app, then it's working!
