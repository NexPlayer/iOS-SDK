# Offline Playback

In the offline playback, each store operation will create a file that contains stored info instead of a database. Using this file and calling this API once will enable *Continue Store* and *Retrieve*.

### How to store content with NXPlayer

The **NXHTTPStoreDelegate** allow you to store content:  

This protocol defines a delegate protocol for the HLS offline storage feature in NexPlayer.  
Any application that will handle HLS offline storage must implement this protocol.

In order to store content for online playback you have to.
1. NXPlayer should set a desired bitrate using the setVideoBitrates:len:withOption.
2. The *NXHTTPStoreDelegate* should be implemented. The `HTTPStore:url:storeOffset:receivedLength:storeBuffer:retrievedSize:` method will be called when HLS contents need to be stored.
3. The player should be opened with a call to mode: *NXOpenModeStoreStream*.
4. Then the player should be started with a call to `nexPlayer:completedAsyncCmdOpenWithResult:playbackType:` from the NXPlayer delegate.
5. After contents are stored, stop: should be called once the event `nexPlayerDidReachEndOfContent` is received by `NXPlayerDelegate`.

Once content is stored for offline playback, an application can implement *NXHTTPRetrieveDelegate* to retrieve the stored HLS scontent and play it back.

### How to retrieve stored content by NXPlayer

The **NXHTTPRetrieveDelegate** protocol allows you to retrieve stored content:  

This protocol defines a delegate protocol for the retrieval and `offline playback` of HLS content stored with NexPlayer.  
Any application that will handle retrieval of HLS content stored for offline playback must implement this protocol.  

Once content has been stored by nexPlayer, to retrieve and play the content offline:
1. Set the bitrate using setVideoBitrates:len:withOption:to the same bitrate used to store the content.
2. Implement the `NXHTTPRetrieveDelegate` protocol and call the `HTTPRetrieve:url:retrieveOffset:receivedLength:outputBuffer:retrievedSize:` function to retrieve offline content.
3. Open, start, and stop the player normally as with any content (except that the previously stored content will be played).

Refer to the *NXHTTPStoreDelegate* protocol for details on how HLS content can be stored so that it can be retrieved with this delegate protocol.

### Properties

#### NXOpenMode:NXOpenModeStoreStream

One of the possible argument values for *NXOpenMode* in open is NXOpenMode:NXOpenModeStoreStream.

#### NXPropertyRFCBufferCount

Controls the maximum number of pages the player can allocate for the remote file cache. The remote file cache stores data that has been read from disk or received over the network (this includes local, streaming, and progressive content). In general, this value should not be changed, as an incorrect setting can adversely affect performance, particularly when seeking.

In order to play multiplexed content, at least one audio chunk and one video chunk must fit inside a single RFC buffer page. For certain formats (PIFF, for example) at very high bitrates, the chunks may be too big to fit in a single page, in which case the RFC buffer page size will need to be increased.

If the system has limited memory resources, it may be necessary to decrease the buffer count when increasing the page size.

Increasing the page size can increase seek times, especially for data received over the network (progressive download and streaming cases), so this value should not be changed unless there are issues playing specific content that cannot be solved in another way.

* **Type:** unsigned int
* **Units:** number of buffers
* **Default:** 20