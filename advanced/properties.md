
# Properties

There are a wide array of properties that can be adjusted to control the behavior of various aspects of the player, from buffer time (how many seconds of streaming content are buffered before playback begins) to the behavior of the player under various error conditions (whether or not to allow audio-only playback if an unsupported video codec is detected, for example).

Properties can be set and retrieved through:

- setProperty:toValue: (NXPlayer)
- getProperty:value: (NXPlayer)
- getProperty: (NXPlayer)

Properties are identified with an integer identifier from the NXProperty enumeration.

The value of each property is an unsigned integer. For some properties, it may be necessary to cast this to a different type. See the individual property documentation for details. If no type is specified, it is safe to treat the property as an unsigned integer.

## enum NXProperty

Property identifiers.
These identify properties that can be set and retrieved with:

- setProperty:toValue: (NXPlayer)
- getProperty:value: (NXPlayer)
- getProperty: (NXPlayer)

### NXPropertyTimestampDifferenceVDispWait

The number of milliseconds (as a negative number) that video is allowed to run ahead of audio before the player waits for audio to catch up. For example, -20 means that if the current video time is more than 20msec ahead of the audio time, the current video frame will not be displayed until the audio catches up to the same time stamp. This is used to adjust video and audio synchronization.

- **Type:** int(should be negative) 
- **Default:** -20 (20msec) 
- **Units:** msec

### NXPropertyTimestampDifferenceVDispSkip

 The number of milliseconds that video is allowed to run behind audio before the system begins skipping frames to maintain synchronization. For example, 200 means that if the current video time is more than 200msec behind the audio time, the current video frame will be skipped. This is used to adjust video and audio synchronization.

 - **Type:** unsigned int 
 - **Units:** msec 
 - **Default:** 200 (0.2 sec)

### NXPropertySocketConnectionTimeout

Amount of time to wait before timing out when establishing a connection to the server. If the connection to the server (the socket connection) cannot be established within the specified time, an error event will be generated and playback will not start.

Set this to zero to disable timeout (NexPlayer will wait indefinitely for a connection).

- **Type:** unsigned int 
- **Default:** 0 (infinite) 
- **Units:** msec (0 for infinite)

### NXPropertyRTPPortMin 

The minimum port number to be used when receiving RTP data. This sets the minimum possible port number to be used for the RTP port that is created when performing RTSP streaming over UDP.

- **Default:** 12000

### NXPropertyRTPPortMax

The maximum port number to be used when receiving RTP data. The maximum possible port number to be used for the RTP port that is created when performing RTSP streaming over UDP.

- **Default:** 30000

### NXPropertyProxyAddress

Sets the proxy address. :{String} 

- **Default:** null

### NXPropertyProxyPort

Sets the proxy port number. 

- **Type:** integer 
- **Default:** 0
 
### NXPropertyAVInitOption 

Controls when video initialization happens. This can be any of the following **Values:**
 
 - **NXPropertyAVInitOption_Partial** If there is an audio track, wait for audio initialization to complete before initializing video.

 - **NXPropertyAVInitOption_All** Begin video initialization as soon as there is any video data, without any relation to the audio track status.
 
- **Default:** NXPropertyAVInitOption_All

### NXPropertyPlayableForNotSupportAudioCodec

If set to 1, allows media playback even if the audio codec is not supported. The default behavior (if this is 0) is to return an error or generate an error event if the audio codec is not supported.

- **Type:** unsigned int 
- **Default:** 0

### NXPropertyPlayableForNotSupportVideoCodec

If set to 1, allows media playback even if the video codec is not supported. The default behavior (if this is 0) is to return an error or generate an error event if the audio codec is not supported.

- **Type:** unsigned int
- **Default:** 0

### NXPropertyUseEyePleaser

If more than this number of frames are skipped during rendering, the remaining frames up to the next keyframe are forcibly discarded and playback resumes from the next keyframe.

- **Type:** unsigned int 
- **Default:** 0xFFFFFFFF
 

### NXPropertyUserAgentString 

RTSP/HTTP User Agent value. 

-  **Type:** String

### NXPropertyFirstDisplayVideoFrame

Controls what is displayed while the player is waiting for audio data. If this is set to zero, the player will not display the first video frame until the audio is ready to play. Whatever was previously displayed will continue to be visible (typically a black frame) while it is waiting for audio data.

If this is set to 1, and video data becomes available prior to audio data, the first video frame will be displayed as a still image until audio data is available. 

Once audio has started, the behavior for both settings is the same; this only affects what is displayed while the player is waiting for audio data.

Under old versions of the SDK (prior to the addition of this property), the default behavior was as though this property were set to zero.

 - **Type:** boolean 
 - **Default:** 1
 - **Values:**
	- **0:** Show nothing.
	- **1:** Show first video frame.

### NXPropertySourceOpenTimeOut 

Sets the amount of time to wait for an open request to complete. This is used when NexPlayer tries to open new media. If there is no response from the server for longer than the amount of time specified here, the open request will be stopped and `nexPlayer:completedAsyncCmdOpenWithResult:playbackType:` will be called with the result, namely the error code, NXErrorMediaOpenTimeout.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 sec)
- **Default:** 300000 (300 seconds)

### NXPropertySocketOperationTimeout

The maximum waiting time till an HTTP request/response message arrives to NexPlayer. If the reply does not arrive within this time after HTTP request message is sent to the streaming server, it will be regarded as an error.

- **Type:** unsigned int 
- **Default:** 30,000 (30 seconds
- **Units:** msec (0 for infinite)  

### NXPropertySeekRangeFromRAPoint 

Sets the range where NexPlayer will seek to a Random Access point rather than the exact target position provided in the seekToAdjustedTime API.

> **Warning** This property is only valid when the second parameter, exact, in the seekToAdjustedTime API is true.

Setting this value is a kind of option for the seekToAdjustedTime API and can be used to minimize the time required to seek in content by taking advantage of Random Access points in the content. A Random Access point is a specific position that the parser is allowed to seek to directly.

This value sets the range where NexPlayer will seek from a Random Access point given by the parser to a target position that equals msec(milliseconds), the first parameter in the seek() API.

If the exact parameter, the second parameter in the seekToAdjustedTime API, is true and the difference between a Random Access point and the target position is within this value, seekToAdjustedTime will find and seek to the exact target position. If the exact parameter is set to true and the difference between a Random Access point and the target position is beyond this range, seek will give up the accurate target point and will instead seek to and play from the Random Access point.

For example, if NexPlayer is seeking to 10000 ms exactly (exact = true) and there is a Random Access point at 7000 ms, if this property is set to less than 3000 ms, the player will ignore the exact target value and will instead play from 7000 ms. On the other hand, if this property is set to more than 3000 ms, then NexPlayer will seek exactly to 10000 ms and begin playback.

> **Warning** Please remember that in order to seek to a target position, audio or video frames have to be decoded. If too large of a value is set here, it may cause the seek process to consume an excessive amount of time especially in high resolution video content.

- **Type:** unsigned int 
- **Units:** msec (1/1000 sec) 
- **Default:** 10000 (10 seconds)

### NXPropertySetToSkipBFrame 

If set to true, unconditionally skips all B-frames without decoding them.

- **Type:** boolean 
- **Default:** 0

**NXPropertyTooMuchLostFrameDuration** Maximum amount of silence to insert to make up for lost audio frames. Under normal operation, if audio frames are lost (if there is a time gap in received audio frames), silence will be inserted automatically to make up the gap.

However, if the number of audio frames lost represents a span of time larger than the value set for this property, it is assumed that there is a network problem or some other abnormal condition and silence is not inserted.

This prevents, for example, a corruption in the time stamp in an audio frame from causing the system to insert an exceptionally long period of silence (which could possibly prevent further audio playback or cause other unusual behavior).

- **Type:** unsigned int 
- **Units:** msec (1/1000 sec) 
- **Default:** 20000 (20 seconds)

### NXPropertySupportLocal

If set to 1, enables local file playback support.

- **Type:** boolean
- **Default:** 1

### NXPropertySupportPD

If set to 1, enables progressive download support.

- **Type:** boolean
- **Default:** 1

### NXPropertySupportWMS 

If set to 1, enables Microsoft Windows Media Streaming support.

- **Type:** boolean
- **Default:** 0

### NXPropertySupportRDT 

If set to 1, enables Real Media Streaming support.

- **Type:** boolean
- **Default:** 0

### NXPropertySupportAppleHTTP

If set to 1, enables Apple HTTP Live Streaming (HLS) support.
 
- **Type:** boolean
- **Default:** 1

### NXPropertySupportDash 

If set to 1, enables DASH support.

- **Type:** boolean
- **Default:** 1

### NXPropertyH264Profile

Limits the H.264 profile that can be selected from an HLS playlist. Under normal operation, the track with the highest supported H.264 profile is selected from an HLS playlist. If this property is set, no track with a profile higher than this value will be selected. This should be set to zero for no limit.

- **Type:** unsigned integer
- **Default:** 0 (use any profile),

### NXPropertyIgnoreAudioLostFrame 

Suppresses automatic silence insertion for lost audio frames. During normal RTSP streaming operation, if an audio frame is lost (for example, due to a bad connection), the NexPlayer engine inserts a frame of silence into the audio stream to maintain synchronization. Enabling this setting suppresses that function. This may improve performance in some cases where the RTSP server doesn’t send an audio stream. This should be used with caution as it can cause the audio and video streams to lose synchronization.

- **Default:** 0 (disabled)
- **Values:**
	- **0:** disabled
	- **1:** enabled

### NXPropertyIgnoreAVSync

Bypasses AV synchronization. When this property is enabled, AV synchronization is bypassed. As soon as data is received, it is immediately presented to the user.

> **Warning** This will almost certainly cause the audio and video to lose synchronization, and video playback speed will be unpredictable and vary depending on the speed of the connection and the speed by which the local system can decode frames. This may be useful for playing back a live video feed where frames are sent by the server at the correct intervals for playback.
 
- **Default:** 0 (disabled)
- **Values:**
	- **0:** disabled
	- **1:** enabled

### NXPropertySupportMSSmoothStreaming 

If set to 1, this enables MS Smooth Streaming support.

 - **Type:** boolean
 - **Default:** 1

### NXPropertyHTTPCredentials 

Adds additional HTTP headers to use to supply credentials when a 401 response is received from the server. The string should be in the form of zero or more HTTP headers
(header name and value), and each header (including the last) should be terminated with a CRLF sequence, for example:
 
```id: test1\r\npw: 12345\r\n```

The particulars of the headers depend on the server and the authentication method being used.

- **Type:** String
 

### NXPropertyUseSyncTask

Sets whether or not NexPlayer should use SyncTask feature. SyncTask may improve decoding performance.

> **Note** This property must be set before initializing NexPlayer or opening and playing content.

- **Type:** unsigned int
- **Default:** 0 
- Values :
	- **0:** Do not use SyncTask.
	- **1:** Use SyncTask.

### NXPropertySetCookie 

Controls whether the player honors cookies sent by the server.
 
- **Type:** unsigned int
- **Default:** 1
- **Values:**
	- **0:** Ignore HTTP cookie headers sent by the server.
	- **1:** Cookie headers received from a streaming server along with the initial manifest or playlist are included with further HTTP requests during the session.

### NXPropertySetLiveBackOff 

Sets the SmoothStreamingLiveBackOff property when playing Smooth Streaming content. This property sets the duration of content (closest to live) that cannot yet be accessed or downloaded by the player. It is like setting how long to wait before asking for the latest fragment in a live presentation, and thus basically sets the played "live" point back from the actual live content available on the server.

The end-to-end latency of the player (what is being played "live" in the player compared to what is available live on the server) is at least the duration ofLiveBackOff added to the duration set for LivePlaybackOffset with NXPropertySetLiveBackOffset.

- **Type:** unsigned int
- **Units:**msec
- **Default:** 6000

### NXPropertySetLiveBackOffset 

Sets the Smooth Streaming LivePlaybackOffset property when playing Smooth Streaming content. This property sets the duration away from the live position to start playback when joining a live presentation when the LiveView option is set to "Recent", but excludes the `LiveBackOff` duration (set by NXPropertySetLiveBackOff).

As a result, live content will be played behind the actual live position by a duration determined by BOTH `LiveBackOff` and the value for `LivePlaybackOffset` set here.

Setting this property enables faster startup because it allows a buffer to be built up as fast as bandwidth will support (potentially faster than real time), which creates a buffer against network jitter. It does however also increase end-to-end latency, which means what is played "live" in the player is farther behind the actual live playing point of the content.

- **Type:** unsigned int 
- **Units:** msec
- **Default:** 7000

### NXPropertyIgnoreAbnormalSegmentTimestamp 

Ignores abnormal segment timestamps. If it is 1 or enabled, NexPlayer will ignore abnormal segment timestamps. If it is 0 or disabled, NexPlayer will not ignore any abnormal segment timestamps.

 - **Type:** boolean
 
> **Warning** This property is not supported in this API version.

### NXPropertyEnableModifyHTTPRequest 

Allows the application to modify the content of an HTTP Request that NexPlayer is about to send to a remote HTTP server. When this property is set equal to 1 (enabled), NexPlayer invokes `nexPlayer:onModifyHttpRequest:` with the HTTP Request as an argument. The application can return the modified version of the HTTP Request that will actually be sent.

- **Values:**
	- **0:** Disabled. Don’t deliver any HTTP Request.
	- **1:** Enabled. Deliver HTTP Request to modify on the application side.

> **See Also** `NXPlayerDelegate.h::NXPlayerDelegate:nexPlayer:onModifyHTTPRequest:` for more information.

### NXPropertyOpenMediaFileFromSpecifiedTS 

Allows NexPlayer to begin downloading content media files from a specified time stamp in the content.

> **Warning** This property is currently only supported for VOD in HTTP Live Streaming (HLS).
 
NexPlayer allows users to start playback in the middle of a content file with the start api, but typically, before playback can begin, the player still opens content from the first media file available and then has to receive all of the media files between the first file and the point where the user would like to start playback.

When playback is to start in the middle of content, this property allows the player to skip receiving the unneeded earlier media files based on the time stamp value set by the application, and instead begin downloading media files from a position closer to the specified time stamp instead.

This property can thus reduce the time needed to open and start playing a media file in the middle of VOD content.

> **Note** This property must be set before NexPlayer.open is called.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 s)
- **Default:** 0xFFFFFFFF


### NXPropertyWebVTTWaitOpen 

Avoids waiting for the first WebVTT segment to download when starting to play content. This property can be used when playing WebVTT content. By default, NexPlayer waits until the first WebVTT segment is downloaded before content begins to play so that no caption text will be missed.

However, if this property is disabled (set to 0), the player will start playing content as soon as possible (instead of waiting until the first WebVTT segment is fully downloaded). This may be preferred if content should start playing as quickly as possible (although initial WebVTT text may be missed).

This property should be called once, immediately after calling init but before calling open.

- **Type:** boolean
- **Default:** 1
- **Values:**
	- **0:** Content starts playing before first WebVTT segment is downloaded.
	- **1:** Content starts playing after first WebVTT segment is downloaded.


### NXPropertySegmentTSReliable 

Sets whether or not to trust a content segment’s timestamp when playback starts. 

> This property should be called after init but before calling open.

- **Type:** int
- **Default:** 1
- **Values:**
	- **0:** Adjust the timestamp during playback.
	- **1:** Trust the timestamp during playback.

### NXPropertySuggestedPresentationDelayTime 

This property overrides the suggestedPresentationDelay value of the DASH manifest.

> This property should be called after init but before calling open.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 sec)
- **Default:** 2000 (2 sec)

### NXPropertyEnableSpdSyncToGlobalTime 

Enables synchronization to UTC time(SPD).  

> This property should be called after init but before calling open.

- **Type:** int
- **Default:** 0
- **Values:**
	- **0:** SPD disabled.
	- **1:** SPD enabled.

### NXPropertySpdSyncDiffTime 

If the current playback is not more synchronized than this value, the player will speed up playback and make sync.

> This property should be called after init but before calling open.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 sec)
- **Default:** 300 (300 msec)

### NXPropertySpdTooMuchDiffTime 

If playback is out of sync than this value, the player will jump to synchronize the video rather than make it by speeding up.

> This property should be called after init but before calling open.

- **Type:** unsigned integer
- **Unit:** msec (1/1000 sec)
- **Default:** 5000 (5 seconds)

### NXPropertySetHWdecoderPixelFormat 

Sets iOS HW decoder pixel format of output property `kCVPixelBufferPixelFormatTypeKey`. This property is to set a pixel format for decoded video format. Have to set it before start to play.

- **Type:** int
- **Default:** 0 (kCVPixelFormatType_420YpCbCr8BiPlanarVideoRange)
- **Values:**
	- **0:** If you want to develop iOS application, you should use this.`kCVPixelFormatType_420YpCbCr8BiPlanarVideoRange`
	- **1:** If you want to develop Unity application, you should use this. `kCVPixelFormatType_32BGRA`

### NXPropertySetMaxCaptionLength 

Set it to extend max caption length.

> This property should be called after init but before calling open.

- **Type:** int
- **Default:** 8192

### NXPropertyRFCBufferPageSize 

Controls the size of each page in the remote file cache. Use caution when adjusting this value. Improper settings may adversely affect performance, or may cause some content to fail to play.

See NXPropertyRFCBufferCount for a detailed description.

- **Type:** unsigned int
- **Units:** kilobytes
- **Default:** 512

### NXPropertyCEA608TextMode 

This property sets whether CEA 608 closed captions should be rendered in caption mode or text mode. 

- **Type:** boolean
- **Default:** 0
- **Values:**
	- **0:** Render CEA 608 closed captions in caption mode.
	- **1:** Render CEA 608 closed captions in text mode.
