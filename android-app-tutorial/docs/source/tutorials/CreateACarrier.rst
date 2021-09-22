建立 Carrier
=========================

**一、加入基本控制項目設定：**

.. code-block:: java

        Carrier.Options options = new Carrier.Options();
        options.setUdpEnabled(true);
        options.setLocalDiscoveryEnabled(true);
        options.setPersistentLocation(this.getFilesDir().getAbsolutePath());
        options.setStorageLocation(this.getFilesDir().getAbsolutePath() + "/storage");
        options.setKeyFile(this.getFilesDir().getAbsolutePath() + "/key");

**二、加入影音控制項目設定：**

.. code-block:: java

        Carrier.AvOptions avOptions = new AvOptionsBuilder()
                            .setEncoderThreads(4)
                            .setDecoderThreads(4)
                            .setEncodeDeadline(1)
                            .setDecodeDeadline(1)
                            .setCpuUsedValue(4)
                            .setRateControlMode(0)
                            .setMaxKeyFrameInterval(15)
                            .setRateControlTargetBitrate(250)
                            .setAllowLaggedEncodeFrame(0)
                            .setDropFrame(75)
                            .setAllowResize(true)
                            .setResizeUpThreshold(30)
                            .setResizeDownThreshold(60)
                            .setRateControlUndershootBits(0)
                            .setRateControlOvershootBits(0)
                            .setBufferSize(6000)
                            .setBufferInitialSize(4000)
                            .setBufferOptimalSize(5000)
                            .setInitialKeyframeCount(1)
                            .build();

**三、加入預設的網路節點：**

.. code-block:: java

        ArrayList<Carrier.Options.BootstrapNode> arrayList = new ArrayList<>();
        // 1
        Carrier.Options.BootstrapNode node = new Carrier.Options.BootstrapNode("Bootstrap-1.arctos.tw", null, "10310", "D7jmsDeoVj3H234RDWzRVR2vnG8GCo6FezRtSoVcE3LG");
        arrayList.add(node);
        // 2
        node = new Carrier.Options.BootstrapNode("Bootstrap-2.arctos.tw", null, "10310", "HuvotLiezBNqfFnzKyQsHp8Zs9pR7YJ441KjhqUUc9mq");
        arrayList.add(node);
        // 3
        node = new Carrier.Options.BootstrapNode("Bootstrap-3.arctos.tw", null, "10310", "5WTT7ozhfpznsvLawf7tPEqiTRiFDBqLEDHQHUsezLLc");
        arrayList.add(node);
        // 4
        node = new Carrier.Options.BootstrapNode("Bootstrap-4.arctos.tw", null, "10310", "6nYMtMGs8Ghwom5EwMRrP9Zkw6j1CuPc8VKp9g6fq4Ut");
        arrayList.add(node);
        // 5
        node = new Carrier.Options.BootstrapNode("Bootstrap-5.arctos.tw", null, "10310", "HvLH4duMMWHqAMpwU3ZXyHSYc8axbJME3ACVDmgDHLgV");
        arrayList.add(node);

        options.setBootstrapNodes(arrayList);

**四、初始化 Carrier：**

.. code-block:: java

	Carrier.initializeInstance(options, avOptions, handler); // Create a Carrier instance.

``options`` : The options to set for creating carrier node.

``avOptions`` : The options to set for AV encoder/decoder.

``handler`` : The interface handler for carrier node.
   
**五、啟動 Carrier：**

.. code-block:: java

	Carrier.getInstance().start(interval); // recommended value is 10
		
``interval`` : Internal loop interval, in milliseconds.

1. 當 Carrier 啟動完成後，會觸發 callback ``onReady``。

.. code-block:: java

	@Override
	public void onReady(Carrier carrier) {
	
	}
	
``carrier`` : A handle to the Carrier node instance.
	
2. 當 Carrier 連上組網後，會觸發 callback ``onConnection``。

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