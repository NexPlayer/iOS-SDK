# DRM Integration

This tutorial demonstrates how to handle NexPlayer SDK in iOS applications with Widevine. First of all, for the following of this tutorial, we have to implement a sample player following the [Setup Guide](/basic/setup-guide.md) in **Swift**.

## Widevine DRM

Now it is time to set up the Widevine. The first thing that you have to be aware of Widevine frameworks is that there are three types of Widevine Frameworks (develop, simulator, and release). In this tutorial, `widevine_cdm_secured_ios.framework` (develop) will be used to implement Widevine DRM with NexPlayer.

### Import Widevine Integration

1. Copy `WidevineIntegration.framework` and `widevine_cdm_secured_ios.framework` to your Xcode project folder.

2. Go to Navigation Area in Xcode > XCODE PROJECT FILE(indicated by blue icon) > TARGETS > General > Frameworks, Libraries and Embedded Content, click on (**+**) > Add files > Add `WidevineIntegration.framework` and `widevine_cdm_secured_ios.framework` in your Xcode project directory.
3. Go to Navigation Area in Xcode > XCODE PROJECT FILE(indicated by blue icon) > TARGETS > Build Phases > Link Binary With Libraries. Check the order of frameworks. **Order is extremely important** like below:
 
 - AVKit
 - AVFoundation
 - VideoToolbox
 - AudioToolbox
 - CoreAudio
 - CoreMedia
 - SystemConfiguration
 - **widevine_ cdm_ secured_ ios**
 - **WidevineIntegration**
 - **NexPlayerSDK**

> **IMPORTANT NOTE:** If the `NexPlayerSDK` is not located __under__ both `widevine_cdm_secured_ios` and `WidevineIntegration`, WidevineIntegration is not able to call NexPlayerSDK.

4. Go to Navigation Area in Xcode > XCODE PROJECT FILE (indicated by blue icon) > PROJECT > Build Settings > All | Combined > Search __Allow Non-Modular Includes In Framework Modules__ > `YES`

5. Go to Navigation Area in Xcode > XCODE PROJECT FILE (indicated by blue icon) > PROJECT > Build Settings > All | Combined > Search __Enable Bitcode__ > `NO`

6. We need to implement Widevine in BridgingHeader

####  BridgingHeader.h

```
#import <NexPlayerSDK/NexPlayerSDK.h>
#import <NexPlayerSDK/NXPlayerABRController.h>
#import <NexPlayerSDK/NXPlayerDelegate.h>
#import <NexPlayerSDK/NXClosedCaption.h>

#import <WidevineIntegration/WidevineIntegration.h>
#import <WidevineIntegration/NexWidevineDelegate.h>
```

### Setup Widevine

Now we will setup widevine in the simple "PlayerController" class we made in the set-up guide.  
`WidevineIntegration.start()` should be set just before `open()`

#### PlayerController.swift

```swift
public class PlayerController: UIViewController {
    ...
    
    private var widevine = WidevineIntegration()
    
    override func viewDidLoad() {
        ...
        
	    let playerView = NXPlayerView()
	    playerView.autoScaling = .fitInView
	    playerView.captionRenderController.captionHidden = true
	    playerView.autoresizingMask = [.flexibleWidth, .flexibleHeight]

        let mainPlayer = playerView.player
        self.view.addSubview(playerView)
        //mainPlayer.delegate = self
	    playerView.player.delegate = self
        
        widevine = WidevineIntegration.init(nxPlayer: mainPlayer, 
                                            clientInfo: ClientInfo())
        widevine.nexWVdelegate = self
        widevine.licenseServerUrl = (<Insert the license here>)
        widevine.start()

        mainPlayer.player.open(<Insert your stream here>)
        
        ...
    }
}

extension PlayerController: NXPlayerDelegate {
    ...
    
    public func nexPlayer(_ nxplayer: NXPlayer!, completedAsyncCmdStopWithResult result: NXError) {
        if (result == NXError.none) {
            
            //widevine should stop before closing the player
            widevine.stop()
            
            nxplayer.close()
        }
        else {
            print("Failed to open  \(result.hashValue)");
        }
    }
}

extension PlayerController: NexWidevineDelegate {
    
    public func process(afterLicenseServer receivedData: Data!) -> Data! {
        return receivedData
    }
    
    public func onLicenseRequest(_ receivedData: Data!) -> Data! {
        return nil
    }
}
```

Client information is needed to initialize Widevine object. Before start API of WidevineIntegration is called, the license server URL should be set.
 
Keep in mind that start API of WidevineIntegration should be called before open API of NexPlayerSDK, and stop API of WidevineIntegration should be called before close API of NexPlayerSDK.

## HTTP Headers

HTTP headers let the client and the server pass additional information with an HTTP request or response. They are compound by 2 params:

- Key: String
- Value: String

Widevine also supports the addition of this HTTP headers.  
To add them we just need to call the following method of widevine:

```swift
widevine.addHeaderField(withKey: header.key, value: header.value)
```

This must be called before `WidevineIntegration.start()`. In case we have several headers we can add them by continuously calling ``addHeaderField`` with the different values.