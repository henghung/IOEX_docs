建立節點間的連線
=============

**一、取得節點地址**
------------------------

想要與其他節點建立連線前，需要取得其他節點的地址。

.. code-block:: java
	
	Carrier.getInstance().getAddress(); // return a string

**二、發起節點加入請求**
----------------------------

取得其他節點的地址後，可以使用 API ``addFriend`` 來加入節點；加入完成後會觸發 callback ``onFriendAdded`` ：

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

**三、同意節點加入請求**
-------------

當有其他節點對自己發起加入請求時，會觸發 callback  ``onFriendRequest``；
如果要同意此請求可以使用 API ``acceptFriend``，加入完成後會觸發 callback ``onFriendAdded``：

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

**四、刪除節點**
-------------

想要取消與其他節點的連線關係，可以使用 API ``removeFriend()`` 來刪除節點，
刪除成功後會觸發 callback ``onFriendRemoved``：

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

	加入其他節點使用的是對方的地址，而刪除其他節點是使用對方的 **User ID** 。
	