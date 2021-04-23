Create A Carrier Instance
=========================

Overview
--------

This section will show you how to set up the IOEX Carrier related control and initialize the Carrier node to get the instance. 

Import the Carrier SDK Library
------------------------------

1. Put the ``.aar file`` of the Carrier SDK in the directory ``app\libs\``.

2. Add the Carrier SDK dependency in **build.gradle**, as follows：

.. code-block:: groovy

	dependencies {
		implementation fileTree(include: ['*.aar'], dir: 'libs')
	}

3. The ``minSdkVersion`` can't be smaller than version 21, Check the settings in **build.gradle**, as follows：

.. code-block:: groovy

	android {
		defaultConfig {
			minSdkVersion 21 // or bigger than
		}
	}
	
4. Finally, Sync Project with Gradle Files.

Initialize the carrier instance
-------------------------------
	
Set Options
~~~~~~~~~~~

In this step, you'll set ``Carrier.Options``, the sample code is as follows:

.. code-block:: java

        Carrier.Options options = new Carrier.Options();
        options.setUdpEnabled(true);
        options.setLocalDiscoveryEnabled(true);
        options.setPersistentLocation(this.getFilesDir().getAbsolutePath());
        options.setStorageLocation(this.getFilesDir().getAbsolutePath() + "/storage");
        options.setKeyFile(this.getFilesDir().getAbsolutePath() + "/key");

   
IOEX Carrier has default nodes. If you don't add default nodes, you'll not be able to connect to other nodes. Add the following five default nodes to the ``Carrier.Options``：

.. code-block:: java
   
   
        ArrayList<Carrier.Options.BootstrapNode> arrayList = new ArrayList<>();
        // 1
        Carrier.Options.BootstrapNode node = new Carrier.Options.BootstrapNode("18.162.185.242", "null", "10310", "D7jmsDeoVj3H234RDWzRVR2vnG8GCo6FezRtSoVcE3LG");
        arrayList.add(node);
        // 2
        node = new Carrier.Options.BootstrapNode("18.162.139.208", "null", "10310", "HuvotLiezBNqfFnzKyQsHp8Zs9pR7YJ441KjhqUUc9mq");
        arrayList.add(node);
        // 3
        node = new Carrier.Options.BootstrapNode("18.162.135.106", "null", "10310", "5WTT7ozhfpznsvLawf7tPEqiTRiFDBqLEDHQHUsezLLc");
        arrayList.add(node);
        // 4
        node = new Carrier.Options.BootstrapNode("18.162.77.187", "null", "10310", "6nYMtMGs8Ghwom5EwMRrP9Zkw6j1CuPc8VKp9g6fq4Ut");
        arrayList.add(node);
        // 5
        node = new Carrier.Options.BootstrapNode("18.162.199.223", "null", "10310", "HvLH4duMMWHqAMpwU3ZXyHSYc8axbJME3ACVDmgDHLgV");
        arrayList.add(node);

        options.setBootstrapNodes(arrayList);
   
   
Initialize and Start the carrier
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After setting ``Carrier.Options``, initialize the Carrier instance and start it.
After initialization, you can get the carrier instance.
Finally, the carrier node is asynchronously started to connect to the carrier network.
If successfully connected to the network, the carrier node starts to work.
As follows:

.. code-block:: java

	Carrier.initializeInstance(options, handler); // Create a Carrier instance.
	
``options`` : The options to set for creating carrier node.

``handler`` : The interface handler for carrier node.

.. code-block:: java

	Carrier.getInstance().start(interval); // recommended value is 10
		
``start()`` : Internal loop interval, in milliseconds.

Callback ``onReady`` will be called after running ``start()``.

.. code-block:: java

	@Override
	public void onReady(Carrier carrier) {
	
	}
	
``carrier`` : A handle to the Carrier node instance.

.. note::
	
	You must wait until callback **onReady** is called before you can use the carrier.
	
Connected to the carrier network, callback ``onConnection()`` will be called. 

.. code-block:: java

	@Override
	public void onConnection(Carrier carrier, ConnectionStatus status) {
		// status =
		// ConnectionStatus.Connected
		// or
		// ConnectionStatus.Disconnected
	}
	
``carrier`` : A handle to the Carrier node instance.

``status`` : Current connection status.