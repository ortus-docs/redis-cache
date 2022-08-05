---
description: Getting started with the Ortus Redis Extension
---

# Installation

## Redis Setup <a href="#redis-setup" id="redis-setup"></a>

You will need to install a [Redis Server](https://redis.io) separately. Your Redis cluster can be a single node, or multiple nodes. The nodes can be installed along side your web servers, or on a server farm of their own-- it's entirely up to you. You can also use [Docker](https://www.docker.com) to spin up a Redis instance. You can use the following Docker compose file for quick testing:

```yaml
version: '3'
services:

  redis_standalone:
    image: redis:6
    ports:
      - "6379:6379"
  redis_insight:
    image: redislabs/redisinsight:latest
    ports:
      - 8001:8001

  redis_cluster:
    image: grokzen/redis-cluster:6.2.0
    ports:
      - 8002-8007:7000-7005
    environment:
      - IP=0.0.0.0

```

{% hint style="info" %}
Using Docker, this will spin up a standalone Redis instance, a Redis cluster, and Redis insight for database inspection.
{% endhint %}

[Redis Insight](https://redis.com/redis-enterprise/redis-insight/) is a great product that it will give you full insights into your running Redis server or cluster.  It will help you analyze issues, inspect keys, values and much more.  Just navigate to the assigned port (8001) and start inspecting!

![Redis Insight](<../.gitbook/assets/image (3).png>)

{% embed url="https://redis.com/redis-enterprise/redis-insight/" %}

## Lucee Setup

The Redis extension is installed as a Lucee extension into any Lucee Server version `5.1.0` and above. The extension has to be installed at the **server level context**.

![](<../.gitbook/assets/image (1) (1).png>)

If installed in the server context, you can create server-level caches that are available to all web contexts in Lucee. The driver will also be available to all web contexts to add their own local caches or override caches if they need too as well.

### **ForgeBox Extension Provider**

In your Lucee Administrator under `Extension > Providers` paste in your Ortus provider URL ([https://www.forgebox.io](https://www.forgebox.io)) and click `save`. Once added, the new provider URL should show up in the list as verified.&#x20;

{% hint style="warning" %}
Lucee has added ForgeBox as an extension provider as core to the project, so you might not need to do this step.
{% endhint %}

### **Installing the Extension**

Now click `Extensions > Applications` and wait for the list to load. There should be an item in the list called `Ortus Redis Cache`. You can activate it as a trial or as a full version with a license key after you install.

![](<../.gitbook/assets/image (5) (1).png>)

Click it and then click the `install` button to begin the installation process.

{% hint style="danger" %}
We recommend a complete server install so changes can take effect.
{% endhint %}

![](<../.gitbook/assets/image (3) (1).png>)

#### Manual/Docker Installation

Lucee also allows you to deploy the extension file (.lex) into a special folder.  Lucee will detect the extension and automatically install it for you.  The location is the following

```
{lucee-server}/WEB-INF/lucee-server/deploy
```

Just drop the [ortus-redis-cache-2.0.0.lex](https://s3.amazonaws.com/downloads.ortussolutions.com/ortussolutions/lucee-extensions/ortus-redis-cache/2.0.0/ortus-redis-cache-2.0.0.lex) file in that folder, wait a few seconds and it will automatically install. You can drop the file there before the server is started or during a started server.

If anything goes wrong during the installation please verify the deploy logs in the following location

```
{lucee-server}/WEB-INF/lucee-server/context/logs/deploy.log
```

### **Activating the Extension**

![](<../.gitbook/assets/image (2).png>)\
\
Once the extension installs, you will now see a new menu item in the admin called `Ortus` with a sub menu called `Redis Cache`. Click this menu and you'll see the activation screen where you can enter the `license key` and `license email` with which you purchased the extension with.

{% hint style="warning" %}
If you do not see the menu, please do a complete restart of your Lucee Server.
{% endhint %}

You will also have to determine the type of server you are installing the extension to. Development or non-public facing servers are FREE of charge and by default receive up to 4 activations.

Production servers get only 1 activation, so make sure you choose the correct server type. Once you get all your information in the form, click on the `activate` button to finalize the installation. Choose the trial option if you don't have a license and just want to try out the extension. When the trial expires, the cache provider will stop working! **The trial is not for production use**.

![](<../.gitbook/assets/image (4) (1).png>)

{% hint style="warning" %}
Development and staging servers are FREE of charge and each license includes up to 4 activations. Production licenses are on a per Lucee instance and are allowed 1 activation. If you have any activation issues, please contact us at [support@ortussolutions.com](mailto:support@ortussolutions.com). Also, make sure you have a valid internet connection in order to activate your product.\\
{% endhint %}

The Ortus Lucee Redis Extension should now be installed on your server and ready to use.

{% hint style="danger" %}
**Important**: Please note that the Redis Extension is licensed on a per-JVM basis or on a per container pack (5-container pack). You will need a license for each separate JVM, regardless of how many contexts (sites) are deployed in your Lucee installation. The typical setup is one JVM per physical/virtual server. Please email us at [support@ortussolutions.com](http://127.0.0.1:49339/docs/support@ortussolutions.com) if you have licensing questions.
{% endhint %}

### Downloading The Extension

If you will be using an offline installation or a Docker based installation, you can either follow the process above or download the extension and leverage a continuous integration server to build your images or server configurations.

[https://downloads.ortussolutions.com/#/ortussolutions/lucee-extensions/ortus-redis-cache/](https://downloads.ortussolutions.com/#/ortussolutions/lucee-extensions/ortus-redis-cache/)

From our artifact repository, download the appropriate `lex` file and drop it into your Lucee deploy folder: `{lucee-server}/WEB-INF/lucee-server/deploy`. Once the engine starts, it will deploy the extension for you automatically.

#### Automatic Activation <a href="#automatic-activation" id="automatic-activation"></a>

If you will be using Kubernetes, Docker Swarm or any other orchestrator, you will most likely want the server warmed up and ready to go. Once you do the deploy extension from the previous section, you will create a `properties` file that will indicate your extension's activation code.

To get your activation code, please contact Ortus Solutions via the [helpdesk](https://ortussolutions.atlassian.net/servicedesk/customer/portal/9) or via email at [support@ortussolutions.com](mailto:support@ortussolutions.com)

Create a `license.properties` file with the following content:

```bash
email=youremail@yourdomain.com
licenseKey=your key
activationCode=your activation code
serverType=Production
```

And place it in the following location: `{lucee-server}/WEB-INF/lucee-server/context/context/ortus/redis/license.properties`

That's it!
