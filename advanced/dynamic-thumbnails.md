# Dynamic Thumbnails

## What is a video thumbnail?

A video thumbnail is as simple as it's just a preview, a single frame, of the video about to be started. Moreover, during the playback of a media content, the concept of thumbnail is still existing, which is called dynamic thumbnail.

## What are dynamic thumbnails?

As mentioned above, a thumbnail is a simple preview of the content that is about to be watched. Dynamic thumbnail allows the user to *explore* what's coming next within the playback of the content that is being played. In other words, dynamic thumbnails allow the user to get a preview of the upcoming video frames.

In order to understand deeply what's a dynamic thumbnail, we need to identify among 3 different frame types:

- **I-Frames**: These are the key frames, since are containing the full image information.
- **P-Frames**: These are considered as prediction frames, only containing the changes from the previous frame.
- **B-Frames**: These type of frames get the differences between the frame preceding and the one following to determine the content.

Since, the I-frame keeps all the image information, the dynamic thumbnail will work with these kind of frames.

## How to enable dynamic thumbnails?

NexPlayer provides different APIs to implement the dynamic thumbnail feature.

In order the set this feature up, the following steps need to be made:

- Enable the dynamic thumbnail feature:

	```swift
	player.enableDynamicThumbnail()
	```

- When open command has been completed, the `contentInfo` can be used to get the total playtime of the content. By dividing the total media duration by the number of thumbnails set to be created, we can obtain the interval time. This value will be used to set each thumbnail content accordingly, regarding the whole media duration.

	```swift
	let intervalTime = player.contentInfo.totalPlayTime / numOfThumbnails
	```

- With the value gotten above, the next step is to call `setOptionDynamicThumbnail` which will set the thumbnail options:

	```swift
	player.setOptionDynamicThumbnailwithOption(NexDynamicThumbnailOption.interval, andParam1: interval, andParam2: 0)
	```

	| Name  | Description  | 
	|---|---|
	| option | The option property to set thumbnail data.|
	| param1 | The number of thumbnails to split the content.|
	| param2 | Possible option to handle Dynamic Thumbnail information (set to 0).|

- If the previous steps have worked correctly, NexPlayer will use the `NXDynamicThumbnailDelegate`   to send thumbnail data to the UI

	```swift
	class YourClass: NXDynamicThumbnailDelegate {
		public func onDynamicThumbnailData(_ player: NXPlayer!, width: Int, height: Int, cts: Int, thumbImage: UIImage!) {
		    //Update UI
		}
	}
	```

	| Name  | Description  | 
	|---|---|
	| mp | The NexPlayer object generating the event.|
	| width | The width of the thumbnail image.|
	| height | The height of the thumbnail image.|
	| cts | The current timestamp of the thumbnail image.|
	| bitmap | RGB buffer pointer(RGB565) of the thumbnail image.|

- `onDynamicThumbnailRecvEnd` method informs that the all thumbnails has been received.

	```swift
	class YourClass: NXDynamicThumbnailDelegate {
		public func onDynamicThumbnailRecvEnd(_ player: NXPlayer!) {
		    //Update UI
		}
	}
	```
		
	| Name  | Description  | 
	|---|---|
	| mp | The NexPlayer object generating the event.|

- When closing the played content, the `disableDynamicThumbnail` method should be called before `NexPlayer.close`:

	```swift
	player.disableDynamicThumbnail()
	player.close()
	```

- If a video track is changed while content is playing, these methods should be called in the following order:
    1. `disableDynamicThumbnail`
    2. `enableDynamicThumbnail` to enable Dynamic Thumbnails for the new content.
    3. `setOptionDynamicThumbnailwithOption` to set the appropriate interval for the new thumbnails.


Full implementation might look like below:    
    
```swift
class YourClass: NXDynamicThumbnailDelegate {
	func setup() {
		let intervalTime = = player.contentInfo.totalPlayTime / numOfThumbnails;
		player.setOptionDynamicThumbnailwithOption(NexDynamicThumbnailOption.interval, andParam1: interval, andParam2: 0)
		player.dynamicThumbnailDelegate = self
	}
	
	func onDynamicThumbnailData(_ player: NXPlayer!, width: Int, height: Int, cts: Int, thumbImage: UIImage!) {
	    //Update UI
	}
	
	func onDynamicThumbnailRecvEnd(_ player: NXPlayer!) {
	    //Update UI
	}
	
	func stop() {
		player.disableDynamicThumbnail()
		player.close()
	}
}
```

## Things to consider

- Dynamic thumbnail feature uses both the H.264 and H.265 NexPlayer SW libraries.