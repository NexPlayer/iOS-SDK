# Controlling the Buffer

NexPlayer loads content data into buffers in a device’s memory to prepare for playback (the so-called Prefetch buffer in NexPlayer). Buffer settings can be adjusted in multiple ways with the properties listed below:

### Control Buffer Size

* `NXPropertyPrefetchBufferSize` The size of the prefetch buffer to prepare for playback. If the buffer status satisfies either limit set by NXPropertyMaxBufferRate or NXPropertyMaxBufferDuration, the filling of the prefetch buffer will be stopped even though there may be spare space still available in the prefetch buffer. 

### Control Buffering Duration

NexPlayer use two separate properties to determine buffering time, `NXPropertyInitialBufferingDuration` and `NXPropertyReBufferingDuration`.

* `NXPropertyInitialBufferingDuration`: This property defines the number of seconds to buffer initially before beginning streaming playback (HLS, RTSP, etc.). If this is set to zero, which is the default value, NexPlayer will automatically select the recommended buffering time based on the content type (longer for HLS, shorter for other streaming types).
* `NXPropertyReBufferingDuration`: This property defines the number of seconds to buffer if additional buffering is required during streaming playback (HLS, RTSP, etc.). The default value is zero, in that case NexPlayer will automatically select the recommended buffering time based on the content type (longer for HLS, shorter for other streaming types).

### How Buffering Operates in General

NexPlayer will start filling the prefetch buffer automatically when the amount of data loaded in memory becomes less that the value set by a property defining the buffering minimum. Similarly, the buffer will stop loading data segment when the memory is filled more that the value set by a property defining a maximum buffered amount. The actual properties defining this behavior operate differently depending on the protocol type of the content, but these operations will run automatically in the background and can be adjusted with the following properties:

- **For Non-HTTP Protocols** :

 - `NXPropertyMinBufferRate`: If the prefetch buffer is less full than the value set by this property, the buffer will resume filling until the buffer status meets one of the conditions set by either *NXPropertyMaxBufferRate* or *NXPropertyMaxBufferDuration*. The default value is 30%.
 - `NXPropertyMaxBufferRate`: If the prefetch buffer is more than this value percent full, buffering will be paused until the buffer status meets the condition set by the property NXPropertyMinBufferRate. The default value is 90%.
 - `NXPropertyMinBufferDuration `: If the duration of content available in the filling buffer is less than this value, buffering will resume filling the buffer until its status meets one of the conditions set by either NXPropertyMaxBufferRate or NXPropertyMaxBufferDuration. The default value is 30 seconds.
 - `NXPropertyMaxBufferDuration`: If the duration of content available in the filling prefetch buffer is greater than this value, buffering will be paused until the buffer status meets the condition of NXPropertyMinBufferDuration again. The default value is 300 seconds.

- **For HTTP Protocols** : For HTTP protocols, only properties defining buffering maximums, NXPropertyMaxBufferDuration and NXPropertyMaxBufferRate, are available. The properties work in the same way as for non-HTTP protocols. After being paused automatically, buffering will automatically resume after 10% of the buffer is exhausted. Note that when NXPropertyMaxBufferDuration and NXPropertyMaxBufferRate are both set, NexPlayer will apply the first maximum value that is met. For example, if the percentage set by NXPropertyMaxBufferRate is passed first, the prefetch buffering will automatically pause even if the buffer is less full than the duration value set for NXPropertyMaxBufferDuration.


## Properties

### NXPropertyAlwaysBuffering (120)

This is used to force NexPlayer to begin buffering as soon as all available audio frames have been processed, without regard to the state of the video buffer.

Under normal operation, when there are no audio frames left in the audio buffer, NexPlayer switches to buffering mode and temporarily suspends playback.

There is an exception if the video buffer is more than 60% full. In this case, NexPlayer will continue video playback even if there is no more audio available.

Setting this property to true(1) bypasses this exception and forces the system to go to buffering immediately if there are no audio frames left to play.

**Default:** 0

### NXPropertyInitialBufferingDuration (9)

The number of milliseconds of media to buffer initially before beginning streaming playback (HLS, RTSP, etc.).

This is the initial amount of audio and video that NexPlayer buffers when it begins playback. To set this property separately, it must be set by calling setProperty after calling open() and before start() is called.

If further buffering is required later in the playback process, the value of the property `NXPropertyReBufferingDuration` will be used instead.

**Unit:** msec (1/1000 sec)

**Default:** 5000 (5 seconds)

### NXPropertyReBufferingDuration (10)

The number of milliseconds of media to buffer if additional buffering is required during playback.

This is the amount of audio and video that NexPlayer buffers when the buffer becomes empty during playback (requiring additional buffering). After open() is called, this property can be set at any time during playback by calling setProperty.

For the initial buffering, the value of the property NXPropertyInitialBufferingDuration is used instead.

**Unit:** msec (1/1000 sec)

**Default:** 5000 (5 seconds)

### NXPropertyPartialPrefetch (519)

Sets whether or not to begin playback after a part of the TS file is downloaded.

By default, this property is set to 0 to download the first TS file completely to play content.

**Default:** 0

**Values:**

- 0 : Partial prefetch ignored; playback will begin after downloading the first TS file completely.
- 1 : Partial prefetch enabled; playback will begin after a part of the TS file is downloaded.

### NXPropertyPrefetchBufferSize (16)

The size of the prefetch buffer to prepare for playback.

If the buffer status satisfies either limit set by NXPropertyMaxBufferRate or NXPropertyMaxBufferDuration, the filling of the prefetch buffer will be stopped even though there may be spare space still available in the prefetch buffer.

If this value is set to 20MB, 1/4 (5MB) is allocated to the past (content already played) and 3/4(15MB) is allocated to the future (content yet to be played).

?> Setting too large of a value here may lead to a large consumption of data packets under 3G or LTE network conditions.
 
**Unit:** bytes

**Default:** 50x1024x1024 (50MB)

### NXPropertyMaxBufferDuration (143)

The maximum duration of prefetch buffer to pause filling the buffer.

If the duration of content available in the filling prefetch buffer is greater than this value, filling of the buffer will be paused until the buffer status meets the condition of NXPropertyMinBufferDuration.

?> Note that when setting `NXPropertyMaxBufferDuration` to a specific value, the value chosen must be at least twice the value of `NXPropertyReBufferingDuration`. If a smaller value is chosen, the value of `NXPropertyMaxBufferDuration` will automatically be increased to twice the value of `NXPropertyReBufferingDuration`. For example, if `NXPropertyReBufferingDuration=5000` ms and one tries to set `NXPropertyMaxBufferDuration` to 7000 ms, `NXPropertyMaxBufferDuration` will automatically be set to 10000 ms instead.
 
**Unit:** milliseconds

**Default:** 300000 (300s)

### NXPropertyMinBufferDuration (142)

The minimum duration of prefetch buffer to resume filling the buffer.

If the duration of content available in the filling buffer is less than this value, filling of the buffer will be resumed until the buffer status meets a condition set by either NXPropertyMaxBufferRate or NXPropertyMaxBufferDuration.

**Unit:** milliseconds (ms)

**Default:** 30000 (30s)

### NXPropertyMaxBufferRate (141)

The maximum filled percentage of the prefetch buffer to pause filling the buffer.

If the prefetch buffer is more than this value percent full, filling the buffer will be paused until the buffer status meets the condition set by the property `NXPropertyMinBufferRate`.

**Unit:** percent

**Default:** 90 (90%)
 
### NXPropertyMinBufferRate (140)

The minimum filled percentage of the prefetch buffer to resume filling the buffer.

If the prefetch buffer is less full than the value set by this property, the buffer will resume filling until the buffer status meets a condition set by either NXPropertyMaxBufferRate or NXPropertyMaxBufferDuration.

**Unit:** percent

**Default:** 30 (30%)

### NXPropertyContinueDownloadAtPause (561)

Sets whether or not to continue downloading data in pause state when playing content.

When this property is set, content data will continue to be downloaded even when NexPlayer is paused.

This property should be called after init and before calling open.

**Default:** 0

**Values:**

- **0:** Stop downloading in pause state.
- **1:** Continue downloading in pause state.


