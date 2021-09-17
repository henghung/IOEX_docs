管理節點資訊
==========

**一、設置自己的節點資訊**
-----------------------

.. code-block:: java

	Carrier.getInstance().setSelfInfo(userInfo);

``userInfo`` : The user information to update for this carrier node.

**二、取得所有好友節點資訊**
------------------------

想要取得所有已加入的節點資訊，可以使用 API ``getFriends()``：

.. code-block:: java

	Carrier.getInstance().getFriends(); // return a list of FriendInfo


當有其他節點更新他的 Carrier 資訊時，會觸發 callback ``onFriendInfoChanged`` 來通知資訊的更新：

.. code-block:: java

		@Override
		public void onFriendInfoChanged(Carrier carrier, String friendId, FriendInfo info) {

		}

``carrier`` : Carrier node instance.

``friendId`` : The friend’s user id.

``info`` : The update friend information.

**三、節點的連線狀態**
-------------------

節點間的連線分為以下三種：

 - **直連 (Direct)**
 - **中繼 (Relay)**
 - **離線 (Disconnected)**

當與其他節點的連線狀態改變時，會觸發 callback ``onFriendConnection``：

.. code-block:: java

		@Override
		public void onFriendConnection(Carrier carrier, String friendId, FriendConnectionStatus status) {
			// status =
			// FriendConnectionStatus.Direct
			// 、
			// FriendConnectionStatus.Relay
			// 、
			// FriendConnectionStatus.Disconnected
		}


``carrier`` : A handle to the Carrier node instance.

``friendId`` : The friend’s user id.

``status`` : The connection status of friend.