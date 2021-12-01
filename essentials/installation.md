# Installation

## Redis Setup <a href="#redis-setup" id="redis-setup"></a>

You will need to install a Redis Server separately. Your Redis cluster can be a single node, or multiple nodes. The nodes can be installed along side your web servers, or on a server farm of their own-- it's entirely up to you. You can also use docker to spin up a Redis instance. You can use the following docker compose file for quick testing:

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
    image: grokzen/redis-cluster:latest
    ports:
      - 7000-7005:7000-7005
    environment:
      - IP=0.0.0.0

```

{% hint style="info" %}
This will spin up using Docker a standalone redis instance, a redis cluster, and redis insight for database inspection.
{% endhint %}

## Lucee Setup

The Redis extension is installed as a Lucee extension into any Lucee Server version `5.1.0` and above. The extension has to be installed at the **server level context**.

![](<../.gitbook/assets/image (1).png>)

If installed in the server context, you can create server-level caches tha are available to all web contexts in Lucee. The driver will also be availble to all web contexts to add their own local caches or override caches if they need to.

### **Add Extension Provider**

In your Lucee Administrator under `Extension > Providers` paste in your Ortus provider URL ([https://www.forgebox.io](https://www.forgebox.io)) and click `save`. One added, the new provider URL should show up in the list as verified.

### **Installing the Extension**

Now click `Extensions > Applications` and wait for the list to load. There should be a item in the list called `Ortus Redis Cache`. You can activate it as a trial or as a full version with a license key after you install.

![](<../.gitbook/assets/image (5).png>)

Click it and then click the `install` button to begin the installation process.

![](<../.gitbook/assets/image (3).png>)\


### **Activating the Extension**

![](<../.gitbook/assets/image (2).png>)\
\
Once the extension installs, you will now see a new menu item in the admin called `Ortus` with a sub menu called `Redis Cache`. Click this menu and you'll see the activation screen where you can enter the `license key` and `license email` with which you purchased the extension with.

You will also have to determine the type of server you are installing the extension to. Development or non-public facing servers are FREE of charge and by default receive up to 4 activations.

Production servers get only 1 activation, so make sure you choose the right server type. Once you get all your information in the form then click on the `activate` button to finalize the installation. Choose the trial option if you don't have a license and just want to try out the extension. When the trial expires, the cache provider will stop working! **The trial is not for production use**.

![](<../.gitbook/assets/image (4).png>)

{% hint style="warning" %}
**Note** : Development and staging servers are FREE of charge and each license includes up to 4 activations. Production licenses are on a per Lucee instance and are allowed 1 activation. If you have any activation issues please contact us at [support@ortussolutions.com](mailto:support@ortussolutions.com). Also, make sure you havea valid internet connection in order to activate your product.\

{% endhint %}

The Ortus Lucee Redis Extension should now be installed on your server and ready to use. Make sure your Redis cluster is running and proceed on to the next step `--->` creating a cache.

{% hint style="danger" %}
**Important**: Please note that the Redis Extension is licensed on a per-JVM basis or on a per container pack (5-container pack). You will need a license for each separate JVM, regardless of how many contexts (sites) are deployed in your Lucee installation. The typical setup is one JVM per physical/virtual server. Please email us at [support@ortussolutions.com](http://127.0.0.1:49339/docs/support@ortussolutions.com) if you have licensing questions.
{% endhint %}

### Downloading The Extension

If you will be using an offline installation or a docker based installation, you can either follow the process above or download the extension and leverage a continous integration server to build your images or server configurations.

[https://downloads.ortussolutions.com/#/ortussolutions/lucee-extensions/ortus-redis-cache/](https://downloads.ortussolutions.com/#/ortussolutions/lucee-extensions/ortus-redis-cache/)

From our artifact repository download the appropriate `lex` file and drop it into your lucee deploy folder: `{lucee-server}/WEB-INF/lucee-server/deploy`. Once the engine starts, it will deploy the extension for you.

#### Automatic Activation <a href="#automatic-activation" id="automatic-activation"></a>

If you will be using Kubernetes, Docker Swarm or any other orchestrator, most likely you want the server warmed up and ready to go. Once you do the deploy extension from the previous section you will create a `properties` file that will indicate your extension's activation code.

To get your activation code, please contact Ortus Solutions via the [helpdesk](https://ortussolutions.atlassian.net/servicedesk/customer/portal/9) or via email at [support@ortussolutions.com](mailto:support@ortussolutions.com)

Create a `license.properties` file with the following content:

```bash
email=youremail@.com
licenseKey=your key
activationCode=your activation code
serverType=Production
```

And place it in the following location: `{lucee-server}/WEB-INF/lucee-server/context/context/ortus/redis/license.properties`

That's it!
