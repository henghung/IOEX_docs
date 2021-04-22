Connect To Other Carrier Nodes
==============================

Overview
--------

This section will show you how to establish connections with other carrier nodes.

Get Carrier Node Address
------------------------

If you want to connect to other carrier nodes, you must have the address of the other carrier node.

.. code-block:: java
	
	Carrier.getInstance().getAddress(); // return a string

Add Friend
----------

If you have the address of other carrier nodes, you can call ``addFriend()`` to add other carrier nodes.
After adding, callback ``onFriendAdded`` will be called. As follows:

.. thumbnail:: image01-1.svg

.. code-block:: java

	Carrier.getInstance().addFriend(address, message);

``address`` : The target user address of remote carrier node.

``message`` : PIN for target user, or any application defined content.

.. code-block:: java

        @Override
        public void onFriendAdded(Carrier carrier, FriendInfo info) {
		
        }
		
``carrier`` : A handle to the Carrier node instance.
		
``info`` : Information of added friends.

Accept Friend
-------------

When a request from another node is received, 
the callback ``onFriendRequest`` will be called.
If you want to accept the request, you can call ``acceptFriend()``.
After accepting, callback ``onFriendAdded`` will be called. As follows:

.. thumbnail:: image01-2.svg

.. code-block:: java

        @Override
        public void onFriendRequest(Carrier carrier, String userId, UserInfo userInfo, String message) {
            
        }

``carrier`` : A handle to the Carrier node instance.

``userId`` : The user id who want be friend with current user.

``userInfo`` : The user information to userId.

``message`` : The PIN for target user, or any application defined content.

.. code-block:: java

	Carrier.getInstance().acceptFriend(userId);
	
``userId`` : The user id who want be friend with us.

Remove Friend
-------------

Use ``removeFriend()`` to delete a friend, 
and the callback ``onFriendRemoved`` will be called after the deletion is successful.
As follows:

.. thumbnail:: image01-3.svg

.. code-block:: java

	Carrier.getInstance().removeFriend(userId);
	
``userId`` :  The target user id to remove friendship.

.. code-block:: java

        @Override
        public void onFriendRemoved(Carrier carrier, String friendId) {
            
        }
		
``carrier`` : Carrier node instance.

``friendId`` : The friend’s user id.

.. note::
	
	Adding a friend uses the **address ID** but deleting a friend uses the **user ID**.

Carrier Node Information
------------------------

If you need to get all friends information, you can use ``getFriends()``.

.. code-block:: java
	
	Carrier.getInstance().getFriends(); // return a list of FriendInfo structure

Update self user information, you can use ``setSelfInfo()``.
After self user information changed, 
carrier node will update this information to carrier network, 
and thereupon network broadcasts the change to all friends,
and the friends who receive the change will call callback ``onFriendInfoChanged``.

.. code-block:: java
	
	Carrier.getInstance().setSelfInfo(userInfo);
	
``userInfo`` : The user information to update for this carrier node.

.. code-block:: java
		
		@Override
		public void onFriendInfoChanged(Carrier carrier, String friendId, FriendInfo info) {
		
		}
		
``carrier`` : Carrier node instance.

``friendId`` : The friend’s user id.

``info`` : The update friend information.
		
Connection Status
-----------------

When the connection status with other carrier nodes changes,
callback ``onFriendConnection`` will be called.

.. code-block:: java

		@Override
		public void onFriendConnection(Carrier carrier, String friendId, ConnectionStatus status) {
			// status =
			// ConnectionStatus.Connected 
			// or
			// ConnectionStatus.Disconnected
		}
	

``carrier`` : A handle to the Carrier node instance.

``friendId`` : The friend’s user id.

``status`` : The connection status of friend.

	