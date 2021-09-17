導入 SDK
=======

**一、將AAR檔放在專案路徑** ``app\libs\``

\

**二、設定** ``app/build.gradle`` **：**

.. code-block:: groovy

	dependencies {
		implementation fileTree(include: ['*.aar'], dir: 'libs')
	}

**三、設定** ``minSdkVersion`` **為版本 21 以上：**

.. code-block:: groovy

	android {
		defaultConfig {
			minSdkVersion 21 // or bigger than
		}
	}

**四、最後** ``File -> Sync Project with Gradle Files``