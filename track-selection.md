# Track Selection

Certain streaming protocols provide multiple audio and video streams of the same content which are intended to be selected bu the user. NexPlayer provides the `setVideoStream()` API to allow these streams to be selected from the User Interface while content is being played.

The full list of available streams (if any) for particular content can be found in the **NXContentInfo::streams** array. The current selected audio and video can be found in **NXContentInfo::currentVideoStream** and **NXContentInfo::currentAudioStream**, respectively.

There are three possible use cases available:

1. **A variant playlist with alternative audio**: Audio and video are delivered in separate streams or groups of tracks. In this case, video and audio can be selected independently. For example, there could be two different audio tracks (different languages) for a video stream a, which includes multiple tracks to be selected internally by the player by adaptive bitrate streaming. The audio tracks should be selected by the user while the player displays the appropriate video track based on network conditions and the device.

2. **A variant playlist with alternative video**: Each track contains both audio and video, but alternative video streams are available (for example different camera angles or views of the same content). In this case, the same audio is included in each track, and the user chooses which video stream to display. Tracks within a stream are selected internally based on network conditions and the device but the user can change video streams from the UI.

3. **A combination of a variant playlist with alternative video and audio**: This use case is a combination of cases 1 and 2, where the main video stream provides video tracks at different bitrates but INCLUDING the same audio, and separate audio tracks are available for optional language selection. To play the alternative audio tracks, the user selects them from the UI.

The information for getting the streams (included in the content) and the tracks (related to each stream) is presented in the following format:

* NXContentInfo
    * NXMediaStreamInfo
        * NXTrackInfo

**Selecting track using setTargetBandWidth**

Alternatively you can use the `NXPlayerABRController::setTargetBandWidth` API to change the track.

```swift
// Current video stream
let currentVideoStream = player.contentInfo.currentVideoStream

// Random stream (can be video, audio or text)
let randomStream = player.contentInfo.streams.randomElement() as! NXMediaStreamInfo

// Random track from the current video stream
let track = currentVideoStream.tracks.randomElement() as! NXTrackInfo

// Using ABRController we force the change of player target bandwidth to the track BandWidth
let abrController: NXPlayerABRController = NXPlayerABRController(player: player)
abrController.setTargetBandwidth(UInt(track.bandwidth), 
								segmentOption: NexBandwidthSegmentOption.default,
								targetOption: NexBandwidthTargetOption.match)
```

Deeper information about NXPlayerABRController can be found in his respective section.  
The different params you can use in method *NXPlayerABRController::setTargetBandWidth(targetBwBps: UInt, segmentOption: NexBandwidthSegmentOption, targetOption: NexBandwidthTargetOption)* are the following.

* **targetBwBps** - the target bandwidth in bps (bits per second)
* **NexBandwidthSegmentOption** - This option will indicate how to handle buffered content when the track changes:
	* **default**: NexPlayer will decide between Quickmix (changing tracks quickly) and LateMix (playing buffered content and changing tracks more slowly).
	* **quickmix**: NexPlayer will clear the buffer as much as possible and will start to download new track so the user can see a new track faster.
	* **latemix**: NexPlayer will preserve and play the content segments already buffered and will download a new track.
* **NexBandwidthTargetOption**:
	* **default**: Default target option (BELOW).
	* **below**: Select a track with a bandwidth below the target bandwidth.
	* **above**: Select a track with a bandwidth above the target bandwidth.
	* **match**: Select the track that has a bandwidth that matches the target set; otherwise send an error and no new target bandwidth is selected.

## API Reference

### NXPlayer.setVideoStream

```swift 
player.setVideoStream(videoStream: NXMediaStreamInfo!, 
					audioStream: NXMediaStreamInfo!, 
					trackAttributes: [AnyHashable : Any]!)
```

For media with multiple streams, selects the streams that will be presented to the user.
The full list of available streams (if any) can be found in the `NXContentInfo::streams` member in `NXPlayer::contentInfo`.

Each stream listed in the array in content information is either an audio stream or a video stream. One stream of each type may be selected for presentation to the user.

There can be multiple tracks associated with each stream, providing different levels of quality. The player switches among these strings as necessary to provide the best possible quality for the available bandwidth.  
Convenience function for setting audio and video streams.  
This is a convenience function, and is equivalent to calling *setVideoStream:audioStream:textStream:trackAttributes:* with text Stream specified as nil.

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | videoStream | The video stream to select. |
| in | audioStream | The audio stream to select. |
| in | trackAttr | A dictionary specifying the custom attributes by which to select a video track within the stream. |

*Returns*  
NXErrorNone if successful, or another NXError value in case of failure.

**Custom Attributes**

In addition to providing different levels of quality, the tracks associated with a video stream can also provide different types of content (for example, different camera angles). These tracks are labeled with custom attributes.

Custom attributes consist of key/value pairs, and zero or more may be associated with any given track. Each unique combination of custom attributes makes up one attribute set. The list of possible attribute sets available for a given stream can be found in `NXMediaStreamInfo::customAttrSets`.

You may limit the selection of tracks to only those that share a particular set of custom attributes by specifying the set of key/value pairs as an NSDictionary in the track Attr argument.  

> **Note** This is an asynchronous operation that completes in the background. When it is finished, the NXPlayerDelegate::completedAsyncCmdSetMediaStreamWithResult: method of the delegate will be called (and the result argument will indicate success or failure).

**Parameters**

| i/o | Name  | Description  | 
|---|---|---|
| in | videoStream | The video stream to select. This may be any one of the elements of `NXContentInfo::streams` where `NXMediaStreamInfo::type` is NXMediaTypeVideo. Specify nil to leave the video stream unchanged. |
| in | audioStream | The audio stream to select. This may be any one of the elements of `NXContentInfo::streams` where `NXMediaStreamInfo::type` is NXMediaTypeAudio. Specify nil to leave the audio stream unchanged. |
| in | textStream | The text stream to select. This may be any one of the elements of NXContentInfo::streams where NXMediaStreamInfo::type is NXMediaTypeText. Specify nil to leave the text stream unchanged. |
| in | trackAttr | A dictionary specifying the custom attributes by which to select a video track within the stream. Only video tracks that match ALL specified attributes (both name and value) will be used. Names and values must all be given asNSString instances. Specify nil to use the first available combination of custom attributes (the first available attribute set) in the selected video stream. |

*Returns*  
NXErrorNone if successful, or another NXError value in case of failure. Even if the return value indicates success, the operation may still fail later, because it completes asynchronously in the background. To determine actual success or failure, check the result argument of the appropriate delegate callback method.


### NXContentInfo Class

Information about specific multimedia content.  
Information about the currently loaded content is available as an NXContentInfo object via NXPlayer::contentInfo.

#### Methods

- `(NSString∗) + stringFromAudioCodecID:` Convenience method that returns a string representation of an NXCodecID, useful for diagnostic and log output, and for displaying to the user. Use this for audio codec IDs.
- `(NSString∗) + stringFromVideoCodecID:` Convenience method that returns a string representation of an NXCodecID, useful for diagnostic and log output, and for displaying to the user. Use this for video codec IDs.
- `(NSString∗) + stringFromFileFormat:` Convenience method that returns a string representation of an NXFileFormat, useful for diagnostic and log output, and for displaying to the user.
- `(NSString∗) + stringFromCaptionType:` Convenience method that returns a string representation of an NXCodecID, useful for diagnostic and log output, and for displaying to the user. Use this for caption types.  

#### Attributes

* **infoAsMultiLineString**  
	Formats the content information as a multi-line string that can be displayed to the user or logged for diagnostic information.  
The string includes all of the details included in NXContentInfo, as well as details on all of the streams available within.  
The string should be displayed in a fixed-pitch font for best results.

	*Returns*  
The content information is formatted as a string.

* **streamsOfType(NXMediaType)**  
Returns a filtered list of streams containing only streams of a single specific type.

	*Parameters*  
| Name  | Description  | 
|---|---|
| type | The type of stream (NXMediaTypeAudio, NXMediaTypeVideo) to return.|

	*Returns*  
An array of NXMediaStreamInfo objects, containing only the elements of NXContentInfo::streams that match
the specified media type.

* **audioChannels**  
	The number of audio channels in the current content.  
This is 1 for mono, 2 for stereo. Some formats may support additional channels. If the content doesn’t include audio, this will be zero.

* **audioCodec**  
	The audio codec in use for decoding the content.  
If the content doesn’t include audio, or the audio format is not recognized or not supported, this will be zero.

* **captionType**  
	The types of captions available in the current content.
In the current version, only the types listed above will be recognized and if captions in another format exist, this will be set to `NXTypes::(NXCodecID)NXCodecID_UNKNOWN`.  
Furthermore, if an external subtitle file is included in addition to another format, this member will be set to the external subtitle type (SMI or SRT).  
Since CEA 608 and CEA 708 closed captions cannot be identified until decoding begins, caption Type will also
be set to `NXTypes::(NXCodecID)NXCodecID_UNKNOWN` when they are included in content.

* **currentAudioStream**  
	The currently selected audio stream within the content.  
This applies to content with multiple audio streams. This is one of the streams from the NXContentInfo::streams array.

* **currentTextStream**  
	The currently selected text stream within the content.  
This applies to content with multiple text streams. This is one of the streams from the `NXContentInfo::streams` array.

* **currentVideoStream**  
	The currently selected video stream within the content.  
This applies to content with multiple video streams. This is one of the streams from the `NXContentInfo::streams` array.

* **DRMInfo**  
	Information about DRM protection associated with the content.  
The exact contents of this dictionary depend on the type of DRM, and whether it is being handled by NexPlayer directly. For DRM handled using custom application-provided descramblers, this dictionary will be empty.

* **fileFormat**  
	The format of the file from which the content was loaded, if applicable.  
In cases where there isn’t an applicable file format (such as during some kinds of streaming playback) this will have the value `NXFileFormatNONE`.

	*See Also*  
NXFileFormat for a list of possible values.

* **hasAudio** 
	YES if the content includes audio.  
In some cases, where the content includes audio in a format that NexPlayer doesn’t recognize, this may be NO even for content with audio. If this is YES, the content includes audio, and NexPlayer is capable of playing back that audio.

* **hasVideo**  
	YES if the content includes video.  
In some cases, where the content includes video in a format that NexPlayer doesn’t recognize, this may be NO even for content with video. If this is YES, the content includes video, and NexPlayer is capable of playing back that video.

* **junkContent**  
	YES if the index table is damaged and operations such as seeking may be problematic.  
This allows UI components to alert the user of the problem.

* **metaData**  
	Additional metadata associated with the content.  
The exact contents of this dictionary depend on the content and may change from version to version. ID3 tag values are an example of one kind of metadata that may be associated with the content.

* **pitch**  
	Pitch of the original video frames, in pixels.  
The pitch is the actual pixel width of the video frame, including any hidden margin required by the decoder, and any padding needed to byte-align each row. Since NexPlayer handles the display of the video image automatically on iOS, this value is really only useful for diagnostic purposes.

* **streams**  
	An array of all audio, video, and text streams associated with the content.  
Most content has only one video stream and one audio stream, but some file formats and some streaming formats support multiple streams of the same type (for example, to provide audio tracks in multiple languages).  
In addition, it is possible for some content that this array may be empty, even though there is audio and video associated with the content. In this case, there is no additional information available about the audio or video beyond the basic information in NXContentInfo, and it is not possible to switch to other tracks.  
Each element in this array is an NXMediaStreamInfo object.  
To get a list of only one type of media, call streamsOfType: instead of using this property.

* **totalPlayTime**  
	Total playing time of the media, if applicable.  
For some streaming formats (in particular, live streams) there may not be a duration available. In this case, the total play-time will be `NXDuration_Unknown`.

* **videoCodec**  
	The video codec in use for decoding the content.  
If the content doesn’t include video, or the video format is not recognized or not supported, this will be zero.

* **videoFrameRate**  
	Frame rate of the video, in frames per second. This is the frame rate specified in the content.  
If the device isn’t powerful enough to decode and display the video stream in real-time, the actual number of displayed frames may be lower than this value.  
For the actual number of displayed frames, see *NXPlayer::video PerformanceStats*

### NXMediaStreamInfo Class

This class provides information about a media stream. For some local formats, and some streaming formats, multiple alternate media streams may be available. For example, audio may be available in multiple languages.  

Media streams are described by `NXMediaStreamInfo` objects. The list of streams available can be found in `NXContentInfo::streams`, and the currently selected audio and video streams can be found in *NXContentInfo::currentVideoStream* and *NXContentInfo::currentAudioStream*, respectively.  

Streams may contain multiple tracking comprising the same media encoded at different quality levels. This allows the player to automatically switch between tracks based on the quality of the network connection and the available bandwidth.  
The full list of tracks available for a stream is in the array `NXMediaStreamInfo::tracks`; the current track that has been automatically selected by the player is in *NXMediaStreamInfo::currentTrack*.  
Some streaming formats support variations on the content (not merely the encoding). Tracks that contain different content are marked with custom attributes to distinguish them from tracks that are merely variations in quality.  

The available methods of this class are the following:

#### Methods

* **infoAsMultiLineString**

	Formats the media stream information as a multi-line string that can be displayed to the user or logged for diagnostic information.  
The string includes all of the details included in NXMediaStreamInfo and it should be displayed in a fixed-pitch font for best results.

	- *Returns*  
The media stream information formatted as a string.

#### Attributes

* **customAttrSetIDs**

	Numeric IDs for each supported combination of custom attributes as an array of NSNumber objects.  
These are internal identifiers and their use is discouraged except for debugging and diagnostic purposes.

* **inStreamID**

	This is the INSTREAM-ID TAG of the media stream. It is an arbitrary value set by the author and is intended for user display (to allow users to select among different alternative streams).

* **internalId**

	An internal numeric ID that uniquely identifies a stream.  
This can be used to determine if two different `NXMediaStreamInfo` objects refer to the same stream:

	```swift
	if( streamA.internalId == streamB.internalId ) {
		// mediaStreamA and mediaStreamB refer to the same stream
}
	```

	However, since a given `NXContentInfo` object can only refer to one set of `NXMediaStreamInfo` objects (one per stream), it is generally safe to simply test for identity:

	```swift
	if( player.contentInfo.streams[i] == player.contentInfo.currentAudioStream ) {
		// The object at index i is the current audio stream
}
	```

	The actual integer value that appears here is arbitrary and may be any 32-bit value. The method for assigning the internal ID may change in future versions.

* **language**

	The language of the stream.  
Some stream formats may not include language information. The exact format of the language string depends on the format of the content and the options chosen by the author of the stream.

* **name**

	The name of the stream.  
Not all streaming formats include stream names, so it is possible for the stream name to be empty.

* **representCodecType**

	The type of codec available in the stream.  
It will be set to `NXTypes::(NXCodecID)NXCodecID_UNKNOWN` until the stream is downloaded. If this is for CEA 608/708 captions embedded in the content, it will be represented as `NXTypes::(NXCodecID)NXCodecID_TEXT_CC_CEA`

### NXTrackInfo Class

Information about a track in a media stream.  
For any given stream, the list of available tracks is in NXMediaStreamInfo::tracks.

Any given stream may have multiple tracks containing the same content encoded at different quality levels to support different network conditions.

* **codecID**  
	This indicates the codec used for the given track.  

!> Do not trust this value in HLS, DASH, and MS Smooth Streaming mode, as invalid values are sometimes provided.

* **internalId**  

	An internal numeric ID that uniquely identifies a stream.  
This can be used to determine if two different `NXMediaStreamInfo` objects refer to the same stream:

	```swift
	if( streamA.internalId == streamB.internalId ) {
		// mediaStreamA and mediaStreamB refer to the same stream
}
	```

	However, since a given `NXContentInfo` object can only refer to one set of `NXMediaStreamInfo` objects (one per stream), it is generally safe to simply test for identity:

	```swift
	if( player.contentInfo.streams[i] == player.contentInfo.currentAudioStream ) {
		// The object at index i is the current audio stream
}
	```

	The actual integer value that appears here is arbitrary and may be any 32-bit value. 

