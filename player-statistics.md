# Player Statistics

Once you have a player up and running is interesting to get the statistics about the url/local video you are playing, this can help to locate problems related to the content you are using and give you several hints about performance.

## Sample Implementation

Following example retrieves statistical information about how content is currently being handled by NexPlayer. If statistics like the rate of video frames being dropped or of frames being rendered are desired, this property can be used to retrieve the FPS (frames per second) for short intervals (about 2 seconds) of content, as well as the total number of decoded video frames and the number of frames rendered during that interval of content.

```swift 
func setupTimer(player: NXPlayer) {
	statisticsAPI = NXStatisticsAPI(player: player)
	statTimer = Timer.scheduledTimer(timeInterval: 2.0, target: self, selector: #selector(NexVideoPlayer.updateStats), userInfo: nil, repeats: true) 
}
    
@objc func updateStats() {
          
    print("------PLAYER STATS------")
    print("avgAudioBitrate                  : \(player.statsInfo.avgAudioBitrate)")
    print("avgTimeDecodingVideoFrames       : \(player.statsInfo.avgTimeDecodingVideoFrames)")
    print("avgTimeRenderingVideoFrames      : \(player.statsInfo.avgTimeRenderingVideoFrames)")
    print("avgVideoBitrate                  : \(player.statsInfo.avgVideoBitrate)")
    print("decodedVideoFramesLastInterval   : \(player.statsInfo.decodedVideoFramesLastInterval)")
    print("decodedVideoFramesPerSec         : \(player.statsInfo.decodedVideoFramesPerSec)")
    print("numDecodingVideoFrames           : \(player.statsInfo.numDecodingVideoFrames)")
    print("numRenderingVideoFrames          : \(player.statsInfo.numRenderingVideoFrames)")
    print("renderedVideoFramesLastInterval  : \(player.statsInfo.renderedVideoFramesLastInterval)")
    print("renderedVideoFramesPerSec        : \(player.statsInfo.renderedVideoFramesPerSec)")
    print("timeDecodingSingleVideoFrame     : \(player.statsInfo.timeDecodingSingleVideoFrame)")
    print("timeRenderingSingleVideoFrame    : \(player.statsInfo.timeRenderingSingleVideoFrame)")
    print("totalAudioFrameBytes             : \(player.statsInfo.totalAudioFrameBytes)")
    print("totalVideoFrames                 : \(player.statsInfo.totalVideoFrames)")
    print("totalDecodedVideoFrames          : \(player.statsInfo.totalDecodedVideoFrames)")
    print("totalDroppedVideoFrames          : \(player.statsInfo.totalDroppedVideoFrames)")
    print("totalRenderedVideoFrames         : \(player.statsInfo.totalRenderedVideoFrames)")
    print("videoFramesLastInterval          : \(player.statsInfo.videoFramesLastInterval)")
    
    print("------BUFFER STATS------")
    print("video buffer rate                : \(statisticsAPI.bufferInfo.bufferRate(NXBufferInfoMediaType.video))")
    print("audio buffer rate                : \(statisticsAPI.bufferInfo.bufferRate(NXBufferInfoMediaType.audio))")
    print("video buffer size                : \(statisticsAPI.bufferInfo.bufferSize(NXBufferInfoMediaType.video))")
    print("audio buffer size                : \(statisticsAPI.bufferInfo.bufferSize(NXBufferInfoMediaType.audio))")
        
    print("------Streaming STATS------")
    print("curNetworkBw                     : \(statisticsAPI.rtStreamingInfo.curNetworkBw)")
    print("curTrackBw                       : \(statisticsAPI.rtStreamingInfo.curTrackBw)")
    print("numOfBytesRecv                   : \(statisticsAPI.rtStreamingInfo.numOfBytesRecv)")
    print("numOfRedirect                    : \(statisticsAPI.rtStreamingInfo.numOfRedirect)")
    print("numOfSegmentDownRate             : \(statisticsAPI.rtStreamingInfo.numOfSegmentDownRate)")
    print("numOfSegmentRecv                 : \(statisticsAPI.rtStreamingInfo.numOfSegmentRecv)")
    print("numOfSegmentRequest              : \(statisticsAPI.rtStreamingInfo.numOfSegmentRequest)")
    print("numOfSegmentInBuf                : \(statisticsAPI.rtStreamingInfo.numOfSegmentInBuf)")
    print("numOfSegmentTimeout              : \(statisticsAPI.rtStreamingInfo.numOfSegmentTimeout)")
    print("numOfTrackSwitchUp               : \(statisticsAPI.rtStreamingInfo.numOfTrackSwitchUp)")
    print("numOfSegmentFailToParse          : \(statisticsAPI.rtStreamingInfo.numOfSegmentFailToParse)")
    print("numOfSegmentFailToRecv           : \(statisticsAPI.rtStreamingInfo.numOfSegmentFailToRecv)")
    print("numOfTrackSwitchDown             : \(statisticsAPI.rtStreamingInfo.numOfTrackSwitchDown)")
    print("numOfTrackSwitchUp               : \(statisticsAPI.rtStreamingInfo.numOfTrackSwitchUp)")
    print("numOfSegmentInBuf                : \(statisticsAPI.rtStreamingInfo.numOfSegmentInBuf)")
}
```

## API Reference

### NXStatsInfo Class

This interface provides playback statistics about the current content in NexPlayer.

This interface can be used to retrieve playback statistics such as the decoded frame rate and the rate of frames being rendered in the player over a short interval of content playback, which may be useful in monitoring player performance and user experience.

#### avgAudioBitrate

The average bitrate of the audio content currently playing.

#### avgTimeDecodingVideoFrames

The average time took to decode a video frame.

#### avgTimeRenderingVideoFrames

The average time took to render a video frame.

#### avgVideoBitrate

The average bitrate of the video currently playing.

#### decodedVideoFramesLastInterval

Number of video frames decoded by NexPlayer during the last interval of content.

The default interval of content is 2seconds.

#### decodedVideoFramesPerSec

The average number of video frames decoded per second.

#### numDecodingVideoFrames

Number of video frames decoded by NexPlayer during the last interval of content. The default interval of content is 2 seconds.

!> **Deprecated** Use `decodedVideoFramesLastInterval` Instead.

#### numRenderingVideoFrames

Number of video frames rendered and displayed by NexPlayer over the last interval of content.

Even though data for more frames of current content may be decoded during an interval, it may be necessary at times for some frames to be skipped in certain circumstances, and this value provides clearer information about what is actually displayed by NexPlayer.

!> **Deprecated** Use `renderedVideoFramesLastInterval` Instead.

#### renderedVideoFramesLastInterval

Number of video frames rendered and displayed by NexPlayer over the last interval of content.

Even though data for more frames of current content may be decoded during an interval, it may be necessary at times for some frames to be skipped in certain circumstances, and this value provides clearer information about what is actually displayed by the NexPlayer.

#### renderedVideoFramesPerSec

The average number of video frames displayed per second.

#### timeDecodingSingleVideoFrame

The time took to decode a video frame.

#### timeRenderingSingleVideoFrame

The time took to render a video frame.

#### totalAudioFrameBytes

The total size of all the audio frames, in bytes.

#### totalDecodedVideoFrames

The total number of video frames decoded to play a video content.

#### totalDroppedVideoFrames

The total number of video frames skipped while playing a video content.

#### totalRenderedVideoFrames

The total number of video frames displayed during playing a video content.

#### totalVideoFrameBytes

The total size of all the video frames of a video content, inbytes.

#### totalVideoFrames

The total number of video frames to decode.

#### videoFramesLastInterval

The number of video frames available to be decoded during the last interval of content.

### NXStatisticsAPI Class

This class manages the playback statistics of the content.

#### initWithPlayer

Designated initializer.

**Parameters**

| Name  | Description  | 
|---|---|
| player | The NXPlayer instance. |

**Returns**

An instance of NXStatisticsAPI class.

#### bufferInfo

Instance of NXBufferInfo class to access buffer information related methods such asNSUInteger.

**See Also**

NXBufferInfo

#### deviceInfo

The information about the current device streaming a HLS content.

**See Also**

NXDeviceInfo

#### httpStateDelegate

An object that conforms to NXHttpStateDelegate which delivers HTTP state information.

**See Also**

NXHttpStateDelegate


#### RTStreamingInfo

Information about the current HLS content.

**See Also**

NXRTStreamingInfo

### NXHttpStateDelegate Protocol

A delegate method for `NXStatisticsAPI`. Implement this to receive HTTP state information. These methods are optional; implement the methods if you wish to receive the HTTP state information.

#### stateInfoDataReceived

```objc
- (void) nexPlayer: (NXPlayer ∗) nxplayer urlString:(NSString ∗) URLString stateInfoDataReceived:(NXHttpStateInfoDataReceived ∗) dataReceived [optional]
```

This event occurs when NexPlayer is downloading a file which is one of NXHttpStateInfoFileType.

*Parameters*

| Name  | Description  | 
|---|---|
| dataReceived | The detailed dataReceived information (see `NXHttpStateInfoDataReceived`).|

#### stateInfoDownEnd

```objc
- (void) nexPlayer: (NXPlayer ∗) nxplayer urlString:(NSString ∗) URLString stateInfoDownEnd:(NXHttpStateInfo- DownEnd ∗) downEnd [optional]
```

This event occurs when NexPlayer finished downloading a file which is one of NXHttpStateInfoFileType.

*Parameters*

| Name  | Description  | 
|---|---|
| downEnd | The detailed downEnd information (see `NXHttpStateInfoDownEnd`).|


#### stateInfoDownStart

```objc
- (void) nexPlayer: (NXPlayer ∗) nxplayer urlString:(NSString ∗) URLString stateInfoDownStart:(NXHttpStateInfo- DownStart ∗) downStart [optional]
```

This event occurs when NexPlayer started downloading a file which is one of the NXHttpStateInfoFileType.

*Parameters*

| Name  | Description  | 
|---|---|
| downStart | The detailed downStart information (see `NXHttpStateInfoDownStart`).|


#### stateInfoHttpError

```objc
- (void) nexPlayer: (NXPlayer ∗) nxplayer urlString:(NSString ∗) URLString stateInfoHttpError:(NXHttpStateInfo- HttpError ∗) httpError [optional]
```

This event occurs when NexPlayer encountered an error during download.

*Parameters*

| Name  | Description  | 
|---|---|
| httpError | The detailed error information(see NXHttpStateInfoHttpError).|

### NXHttpStateInfoDataReceived Class

#### bytesReceived

The current number of bytes received, as aninteger.

#### totalSize

The total bytes of the content to be downloaded. -1 represents unknown.

### NXHttpStateInfoDownEnd Class

#### bytesReceived

The current number of bytes received, as aninteger.

### NXHttpStateInfoDownStart Class

#### fileType

The file type to be downloaded.

- NXHttpStateInfoFileTypeUnknown = 0, 
- NXHttpStateInfoFileTypeMPD = 1, 
- NXHttpStateInfoFileTypeSegment = 2, 
- NXHttpStateInfoFileTypeInitialSegment = 3,
- NXHttpStateInfoFileTypeKey = 4, 
- NXHttpStateInfoFileTypeSegmentIndex = 5

#### mediaType

The media type of the current content.

- NXHttpStateInfoMediaTypeNone = 0
- NXHttpStateInfoMediaTypeAudio = 1
- NXHttpStateInfoMediaTypeBaseVideo = 2
- NXHttpStateInfoMediaTypeText = 4
- NXHttpStateInfoMediaTypeEnhancedVideo = 8

#### segmentDuration

The duration of the current segment, as an integer.

#### segmentNumber

The current segment number, as an integer.

#### trackBW

The bandwidth of the current track, as an integer.

### NXDeviceInfo Class

This class provides information about the current device.

#### dataConnectionType

The type of current data connection of a device.

#### deviceId

The ID of a device.

#### deviceType

The device type name.

#### ipAddress

The IP address of a device.


#### platformVersion

The current iOS version of a device.


### NXRTStreamingInfo Class

This class manages information about the current streaming content.

#### curNetworkBw

The actual bitrate, in bps, of the read segments. The read bitrate is the average speed at which the streaming segments are read from the network server.

#### curTrackBw

The bitrate, in bps, as specified in the segment profile.

#### initialMpd

Full content of an initial manifest file.

#### initialMpdUrl

The actual URI (after all the redirects) for the request of a manifest file.

#### masterMpd

Full content of a master manifest file.

#### masterMpdUrl

Master manifest URL.

#### numOfBytesRecv

The number of bytes received from the server by the player.

#### numOfRedirect

The total number of redirects. This includes redirects for both the manifest file and the individual segments.

#### numOfSegmentDownRate

The number of the segments with a lower read bitrate than the bitrate specified on the profile. The read bitrate is the average speed at which the streaming segments are read from the network server.

#### numOfSegmentFailToParse

The number of segments failed to receive during the streaming.

#### numOfSegmentFailToRecv

The number of segments failed to receive from the server.

#### numOfSegmentInBuf

The total number of segments in the buffer.

#### numOfSegmentRecv

The number of received segments from the server by the player.

#### numOfSegmentRequest

The number of requested segments from the server by the player.

#### numOfSegmentTimeout

The number of segments that resulting a timeout.

#### numOfTrackSwitchDown

The number of times that a content profile has changed to a profile with a lower bitrate.

#### numOfTrackSwitchUp

The number of times that a content profile has changed to a profile with a higher bitrate.

#### startSegUrl

The description of an initially selected profile.

### NXBufferInfo Class

This class retrieves the specified buffer information.

?> **Note** Do not create instance of this class directly. Instead, use the NXStatisticsAPI::bufferInfo property.
 
**See Also**

- NXStatisticsAPI::bufferInfo

#### bufferedSize

This method gets the buffered size of current media stream.

**Parameters**

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

**Returns**

The buffered size.

#### bufferingState

This method gets the buffering state of current media content.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The buffering state of the current media content.

#### bufferRate

This method gets the buffer rate : (Buffered size)∗100 / (Total buffer size), or how much percentage full the current buffer is.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The buffer rate of current media stream.

#### bufferSize

This method gets the buffer size of current media stream.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The buffer size of current media stream.

#### firstFrameCTS

This method gets the CTS of first frame in the buffer.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The CTS of first frame in the buffer. If there is no frame, return NXBufferInfoValueNotAvailable.

#### initialBufferingSize

This method gets the initial buffering size of current media stream.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The Initial buffering size of current media stream.

#### initialBufferingTime

This method gets the initial buffering time of current media stream.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The initial buffering time of current media stream.

#### lastFrameCTS

This method gets the CTS of last frame in the buffer.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The CTS of last frame in the buffer. If there is no frame, return NXBufferInfoValueNotAvailable.

#### totalDuration

This method gets the total duration of frames in the buffer.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The total duration of all the frames in the buffer, in milliseconds.

#### totalFrameCount

This method gets the total count of frames in the buffer.

*Parameters*

| Name  | Description  | 
|---|---|
| mediaType | The type of current media stream.|

*Returns*  

The total count of all the frames in the buffer.	