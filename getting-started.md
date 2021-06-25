# Getting Started with NexPlayer iOS SDK

## Setting up a New Xcode Project using the NexPlayer SDK

1. Create a new application.
2. Drag **NexPlayerSDK.framework** into the Frameworks group in Xcode.
3. You may choose to reference a shared location or copy the framework into your project.
4. Right-click on the Frameworks group in Xcode and choose **Add-** > **Existing Framework** , and add each of the
    follow frameworks, required by the NexPlayerSDK:
	- AudioToolbox.framework
	- OpenGLES.framework
	- Foundation.framework
	- QuartzCore.framework
	- SystemConfiguration.framework
	- CoreVideo.framework
	- CoreMedia.framework
	- AVFoundation.framework
	- VideoToolbox.framework

For a quick start to your first application, create a `UIViewController` subclass (we’ll call it, for this example, `PlayerController`) and simply add the following code in the `viewDidLoad` method:

```objc
- (void)viewDidLoad {
	self.view.backgroundColor = [UIColor blackColor];
	
	m_playerView = [[NXPlayerView alloc] initWithFrame:self.view.bounds];
	[m_playerView setAutoresizingMask:
	UIViewAutoresizingFlexibleWidth |
	UIViewAutoresizingFlexibleHeight];
	[self.view addSubview:m_playerView];
	
	m_playerView.player.delegate = self;
	[m_playerView.player open:@"http://your.media.com/index.m3u8"
							mode:NXOpenModeLocalBundle
							subtitles:nil
							transport:NXTransportTypeTCP
							autoPlay:YES];
}
```

Make sure you edit the header file to indicate that this implements the NXPlayerDelegate protocol:

```objc
@interface PlayerController : UIViewController <NXPlayerDelegate> {
	NXPlayerView*m_playerView;
}
```

And then create an instance of your PlayerController when your application starts, and add its view to your window:

```objc
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*) launchOptions {
       playerController = [[PlayerController alloc] init];
       [self.window addSubview:playerController.view];
       [self.window makeKeyAndVisible];
       return YES;
}
```

That’s all; just make sure your HLS media URL, "http://your.media.com/index.m3u8" for example, is available on the network and this simple program will load and play that content.

> **Warning** Bitcode is not supported yet. To disable Bitcode, the build option Enable Bitcode in the Build Settings of the target of your App should be set to No.

## Handling Events

NexPlayer generates various events to notify the application of changes in the player’s status in real time. This allows the application to update the user interface in an appropriate manner, detect the end of the content, and respond to errors.

Events are handled through the NXPlayerDelegate protocol. You should create an object which conforms to this protocol and assign it to the delegate property of your NXPlayer instance.

See NXPlayerDelegate for more information on handling events.

## Support for Subtitles and Closed Captions

In addition to support for standard subtitle formats, this version of the SDK also fully supports CEA 608 closed captions according to the specifications. These closed captions can be fully handled and displayed by the SDK or, as these captions include a variety of attributes and display modes, they may be implemented differently in a specific application if desired by using the NXCEA608Caption API to pass updated caption information to be displayed by the final application.

Basic support (rendering of text) for CEA 708 closed captions, WebVTT text tracks, and 3GPP/TTML timed text is also currently supported.

Please see `NXCEA608Caption` and `NXCEA608CaptionView` for more information on how to implement CEA 608 closed captions as well as `NXPlayer::selectedCEA608Channel:` for selecting or disabling CEA 608 closed captions.

## Support for Server-side Time Shift in Live Content

This version of the NexPlayer SDK introduces support for server-side time-shifting playback in live content. While content is viewed live, a certain amount of time in the past or future may also be available to be played, depending on the server for the given content. By checking the member `isSeekable` in `NXPlayer::contentInfo` to determine if seeking is allowed, NexPlayer then uses the properties `seekBase` and `seekableLength` to determine the range within the content where seek can be performed and thus within which playback may be time-shifted.

The method `NXPlayer::getSeekableRange` can also be called to determine the range in content where seeking is
possible.

Please also see `nexPlayer:seekableStateChangedTo:seekBase:seekableLength: (NXPlayerDelegate-p)`, `NXPlayer::getSeekableRange`, and `seekTo: (NXPlayer)` as well as the sample code for more information.

## iOS Versions and Multitasking

The NexPlayer SDK links to certain functions available to detect when the application is suspended or sent to the background. In this case, video display is suppressed (attempting to access OpenGL to draw frames while in the background will cause iOS to kill the application).

NexPlayer is weak-linked to the required functions, so it still runs on older iOS versions without multi-tasking, by simply not calling those functions.

NexPlayer uses Audio Queues and Audio Units to play back audio on iOS. Normally, iOS automatically suspends these when the application is sent to the background. This automatically causes video playback to stop as well, since it is timed to the audio. That means if you want your audio and video to suspend while your app is in the background, you don’t need to do anything special; the default behavior will work.

If you want audio to continue playing, you will need to prevent the app from completely suspending by using the appropriate iOS API functions. The exact technique is beyond the scope of this document, but can be found in the iOS documentation from Apple.

## DRM Descrambling

NexPlayer supports DRM descrambling by allowing the application to assign one or more descramblers to members of NXPlayer.

A descrambler can be the same as the NXPlayerDelegate, or can be a dedicated descrambling object.

There is an ObjectiveC protocol for each type of descrambler, and a descrambler object must conform to the appropriate protocol. For the most part, a descrambling protocol consists only of a single descrambling method.

The descrambling method receives pointers to input and output buffers; it descrambles the data in the input buffer and places the descrambled data in the output buffer.

> **Warning** In many cases, the input and output buffer pointers point to the same location. Your code should be able to handle cases where they point to the same location, and cases when they are different. For example a typical no-op descrambling method that just outputs what it is given as input might be written as follows:

```objc
@interface MyDRMDescrambler : NSObject <NXDRMDescrambler> {
}
@end

@implementation MyDRMDescrambler

- (int) descrambleDRMForPlayer:(NXPlayer*)player
			dataType:(NXDRMDataType)type
			inputBuffer:(unsigned char*)pInputBuffer
			inputBufferSize:(unsigned int)uiInputBufferSize
			outputBuffer:(unsigned char*)pOutputBuffer
			outputBufferSize:(unsigned int*)puiOutputBufferSize
{
    NSLog(@"[%@]: pInputBuffer=0x%X uiInputBufferSize=%d", [self class], (unsigned int)pInputBuffer, uiInputBufferSize);

	if( pInputBuffer != pOutputBuffer )
		memcpy( pOutputBuffer, pInputBuffer, uiInputBufferSize );

	puiOutputBufferSize = uiInputBufferSize;
	return 0;
}
@end
```

Different types of descramblers allow access to data at different points in the decoding process. The exact point at which the descrambling must occur differs between the different DRM schemes. In addition, some descramblers have additional methods or additional method parameters that are necessary for a given type of DRM. See the individual protocol descriptions for more information.

## Remote File I/O

NexPlayer also provides a remote file I/O interface that allows an application to provide custom open, close, read and write implementations. This allows an application to retrieve the file data from another source, or to perform DRM descrambling on the data as it is read. See `NXRemoteFileIOInterface` for details
