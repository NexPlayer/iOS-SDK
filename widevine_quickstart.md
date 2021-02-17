# NexPlayer SDK Quick Start with Widevine

This tutorial demonstrates how to handle NexPlayer SDK in iOS applications with Widevine. In this tutorial, a sample player will be implemented in **Swift**.

First thing you have to keep in mind before implementing NexPlayer SDK is that most of player methods behave __asynchronously__. There are numerous methods available in _NexPlayerDelegate.h_ which listen to what is happening in NexPlayer. Asynchronous approach is strongly recommended in NexPlayer SDK.

## Create a new project

1. Open Xcode
2. Click “Create a new Xcode project” (or select File > New > Project).
3. Select iOS at the top of the dialog. Then select App
4. Set the name og your app and choose additional options for your project
5. Click Next
6. Choose a location to save your project and click Create

## Import required frameworks

1. Copy NexPlayerSDK.framework to your Xcode project folder
2. Go to Navigation Area in Xcode > XCODE PROJECT FILE(indicated by blue icon) > TARGETS > General > Frameworks, Libraries and Embedded Content, click on (**+**) to add frameworks and libraries to the list
3. To import NexPlayerSDK, click the (**+**) in Frameworks, Libraries and Embedded Content > Add Other... > Add Files... > Select NexPlayerSDK.framework in your Xcode folder. Please ensure that you are using the following Frameworks and Libraries:  
 
 - AVKit  
 - AVFoundation  
 - VideoToolbox  
 - AudioToolbox  
 - CoreAudio  
 - CoreMedia  
 - SystemConfiguration  
 - NexPlayerSDK  

4. Go to Navigation Area in Xcode > XCODE PROJECT FILE(indicated by blue icon) > PROJECT > Build Settings > All | Combined > Search **Other Linker Flags** > Add **-lc++** in **Other Linker Flags** 
5. In order to import the required methods from NexPlayerSDK, we will need to create a Bridging Header, which will export all the Objective-C functions to Swift. Go to Navigation Area in Xcode > XCODE PROJECT FILE(indicated by blue icon) > TARGETS > Build Settings > All | Combined > Search **Objective-C Bridging Header** and set the value to: `<Root folder of your folder>/BridgingHeader.h`

####  BridgingHeader.h
```
#import <NexPlayerSDK/NexPlayerSDK.h>
#import <NexPlayerSDK/NXPlayerABRController.h>
#import <NexPlayerSDK/NXPlayerDelegate.h>
#import <NexPlayerSDK/NXClosedCaption.h>
```

## Setup PlayerView

#### MainViewUI.swift

```swift
import Foundation
  
public class MainViewUI: NSObject{
    lazy var mainPlayerView:UIView = {
        let view = UIView()
        return view
    }()
    
    public func layout(viewController: UIViewController) {
        viewController.view.addSubview(mainPlayerView)

        mainPlayerView.center = viewController.view.center
        
        mainPlayerView.translatesAutoresizingMaskIntoConstraints = false
        mainPlayerView.topAnchor.constraint(equalTo: viewController.view.topAnchor).isActive = true
        mainPlayerView.leftAnchor.constraint(equalTo: viewController.view.leftAnchor).isActive = true
        mainPlayerView.rightAnchor.constraint(equalTo: viewController.view.rightAnchor).isActive = true
        mainPlayerView.bottomAnchor.constraint(equalTo: viewController.view.bottomAnchor).isActive = true
    }
}
```

#### MainViewController.swift

```swift
import UIKit

class MainViewController: UIViewController {    
    
    private let ui = MainViewUI()

    public override func viewDidLoad() {
        super.viewDidLoad()
        ui.layout(viewController: self)
    }
}
```

## Setup NexVideoPlayer and Open Stream

#### NexVideoPlayer.swift

```swift
import Foundation

public class NexVideoPlayer: NSObject {
    lazy var container:UIView = {
        let view = UIView()
        return view
    }()
    
    lazy var playerView:NXPlayerView = {
        let playerView = NXPlayerView()
        playerView.tag = 1
        playerView.autoScaling = NXScale.fitInView
        playerView.autoresizingMask = [UIView.AutoresizingMask.flexibleWidth, UIView.AutoresizingMask.flexibleHeight];
        return playerView
    }()
    
    public var player:NXPlayer { return playerView.player }
    private var abrController:NXPlayerABRController!
    private weak var playerDelegate:NXPlayerDelegate?

    public init(delegate: NXPlayerDelegate) {
        self.playerDelegate = delegate
    }
    
    public func layout(parent: UIView) {
        parent.addSubview(container)
        container.translatesAutoresizingMaskIntoConstraints = false
        container.bounds = parent.bounds
        container.leftAnchor.constraint(equalTo: parent.leftAnchor).isActive = true
        container.rightAnchor.constraint(equalTo: parent.rightAnchor).isActive = true
        container.topAnchor.constraint(equalTo: parent.topAnchor).isActive = true
        container.bottomAnchor.constraint(equalTo: parent.bottomAnchor).isActive = true
        
        container.addSubview(playerView)
        playerView.translatesAutoresizingMaskIntoConstraints = false
        playerView.bounds = parent.bounds
        
        playerView.leftAnchor.constraint(equalTo: container.leftAnchor).isActive = true
        playerView.rightAnchor.constraint(equalTo: container.rightAnchor).isActive = true
        playerView.topAnchor.constraint(equalTo: container.topAnchor).isActive = true
        playerView.bottomAnchor.constraint(equalTo: container.bottomAnchor).isActive = true
 
        player.delegate = playerDelegate
    }
}
```

> Now we are going to implement NXPlayerDelegate, whose methods will be called asynchronously
 
#### MainViewUI.swift

```swift
import Foundation
  
public class MainViewUI: NSObject{

    ...
    
    private var players = [NexVideoPlayer]()
    private var playerContainers = [UIView]()
    
    public func layout(viewController: UIViewController) {
        
		...
        
        let mainPlayer = NexVideoPlayer(delegate: self)
        mainPlayer.layout(parent: mainPlayerView)
        
        mainPlayer.player.open(<Insert your stream here>)
        
        players.append(mainPlayer)
        playerContainers.append(mainPlayerView)
    }
}

extension MainViewUI: NXPlayerDelegate {
    public func nexPlayer(_ nxplayer: NXPlayer!, completedAsyncCmdOpenWithResult result: NXError, playbackType type: NXPlaybackType) {
        if (result == NXError.none) {
            nxplayer.start()
        }
        else {
            print("Failed to open  \(result.hashValue)");
        }
    }
    
    public func nexPlayer(_ nxplayer: NXPlayer!, completedAsyncCmdStopWithResult result: NXError) {
        if (result == NXError.none) {
            nxplayer.close()
        }
        else {
            print("Failed to open  \(result.hashValue)");
        }
    }
}
```

---

## Widevine

Now it is time to set up the Widevine. The first thing that you have to be aware of Widevine frameworks is that there are three types of Widevine Frameworks (develop, simulator, and release). In this tutorial, `widevine_cdm_secured_ios.framework` (develop) will be used to implement Widevine DRM with NexPlayer.

The device should follow these two requirements.

1. iOS version 9.0+
2. arm64 CPU architecture

### Import Widevine Integration

1. Copy `WidevineIntegration.framework` and `widevine_cdm_secured_ios.framework` to your Xcode project folder.

2. Go to Navigation Area in Xcode > XCODE PROJECT FILE(indicated by blue icon) > TARGETS > General > Frameworks, Libraries and Embedded Content, click on (**+**) > Add `WidevineIntegration.framework` and `widevine_cdm_secured_ios.framework` in your Xcode project directory.
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

> **NOTE:** If the `NexPlayerSDK` is not located __under__ both `widevine_cdm_secured_ios` and `WidevineIntegration`, WidevineIntegration is not able to call NexPlayerSDK.

4. Go to Navigation Area in Xcode > XCODE PROJECT FILE (indicated by blue icon) > PROJECT > Build Settings > All | Combined > Search __Allow Non-Modular Includes In Framework Modules__ > `YES`

5. Go to Navigation Area in Xcode > XCODE PROJECT FILE (indicated by blue icon) > PROJECT > Build Settings > All | Combined > Search __Enable Bitcode__ > `NO`

> **NOTE:** We need to implement Widevine in BridgingHeader

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

`WidevineIntegration.start()` should be set just before `open()`

#### MainViewUI.swift

```swift
public class MainViewUI: NSObject{
    ...
    
    private var widevine = WidevineIntegration()
    
    public func layout(viewController: UIViewController) {
        ...
        
        let mainPlayer = NexVideoPlayer(delegate: self)
        mainPlayer.layout(parent: mainPlayerView, index: 0)
        
        widevine = WidevineIntegration.init(nxPlayer: mainPlayer.player, clientInfo: ClientInfo())
        widevine.nexWVdelegate = self
        widevine.licenseServerUrl = (<Insert the license here>)
        widevine.start()

        mainPlayer.player.open(<Insert your stream here>)
        
        ...
    }
}

extension MainViewUI: NXPlayerDelegate {
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

extension MainViewUI: NexWidevineDelegate {
    
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


### NexPlayer with Widevine project

#### MainViewUI.swift

```swift
import Foundation

public class MainViewUI: NSObject{
    lazy var mainPlayerView:UIView = {
        let view = UIView()
        return view
    }()
    
    lazy var activityIndicator:UIActivityIndicatorView = {
        let activityIndicator = UIActivityIndicatorView()
        activityIndicator.startAnimating()
        activityIndicator.hidesWhenStopped = true
        activityIndicator.style = .white
        return activityIndicator
    }()
    
    private var players = [NexVideoPlayer]()
    private var playerContainers = [UIView]()
    
    private var widevine = WidevineIntegration()
    
    public func layout(viewController: UIViewController) {
        viewController.view.addSubview(mainPlayerView)
        viewController.view.addSubview(activityIndicator)

        activityIndicator.center = viewController.view.center
        mainPlayerView.center = viewController.view.center
        
        mainPlayerView.translatesAutoresizingMaskIntoConstraints = false
        mainPlayerView.topAnchor.constraint(equalTo: viewController.view.topAnchor).isActive = true
        mainPlayerView.leftAnchor.constraint(equalTo: viewController.view.leftAnchor).isActive = true
        mainPlayerView.rightAnchor.constraint(equalTo: viewController.view.rightAnchor).isActive = true
        mainPlayerView.bottomAnchor.constraint(equalTo: viewController.view.bottomAnchor).isActive = true
        
        mainPlayerView.addGestureRecognizer(UITapGestureRecognizer(target: self, action: #selector(handleTap)))
        mainPlayerView.isUserInteractionEnabled = true
        
        let mainPlayer = NexVideoPlayer(delegate: self)
        mainPlayer.layout(parent: mainPlayerView)
        
        widevine = WidevineIntegration.init(nxPlayer: mainPlayer.player, clientInfo: ClientInfo())
        widevine.nexWVdelegate = self
        widevine.licenseServerUrl = "https://proxy.staging.widevine.com/proxy"
        widevine.start()

        mainPlayer.player.open("https://storage.googleapis.com/wvmedia/cenc/h264/tears/tears.mpd")
        
        players.append(mainPlayer)
        playerContainers.append(mainPlayerView)
    }
    
    public func getVideoPlayer() -> NexVideoPlayer{
        return players[0]
    }
    
    @objc func handleTap() {
        let player = players[0]
        if(player != nil && player.isPaused()){
            player.resume()
        }else{
            player.pause()
        }
    }
}

extension MainViewUI: NXPlayerDelegate {
    public func nexPlayer(_ nxplayer: NXPlayer!, completedAsyncCmdOpenWithResult result: NXError, playbackType type: NXPlaybackType) {
        if (result == NXError.none) {
            activityIndicator.stopAnimating()
            nxplayer.start()
        }
        else {
            print("Failed to open  \(result.hashValue)");
        }
    }
    
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

extension MainViewUI: NexWidevineDelegate {
    
    public func process(afterLicenseServer receivedData: Data!) -> Data! {
        return receivedData
    }
    
    public func onLicenseRequest(_ receivedData: Data!) -> Data! {
        return nil
    }
}
```  

#### MainViewController.swift

```swift
import UIKit

class MainViewController: UIViewController {    
    
    private let ui = MainViewUI()
    
    lazy var buttonBack:UIButton = {
        let button = UIButton()
        button.setImage(UIImage(named: "back"), for: .normal)
        return button
    }()
    
    public override func viewDidLoad() {
        super.viewDidLoad()
        ui.layout(viewController: self)
        
        view.addSubview(buttonBack)
        buttonBack.translatesAutoresizingMaskIntoConstraints = false
        
        if #available(iOS 11.0, *) {
            buttonBack.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 20).isActive = true
            buttonBack.leftAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leftAnchor, constant: 20).isActive = true
        } else {
            buttonBack.topAnchor.constraint(equalTo: view.topAnchor, constant: 20).isActive = true
            buttonBack.leftAnchor.constraint(equalTo: view.leftAnchor, constant: 20).isActive = true
        }
        buttonBack.heightAnchor.constraint(equalToConstant: 40).isActive = true
        buttonBack.widthAnchor.constraint(equalToConstant: 40).isActive = true
        buttonBack.contentEdgeInsets = UIEdgeInsets(top: 10,left: 10,bottom: 10,right: 10)
        buttonBack.backgroundColor = UIColor.darkGray.withAlphaComponent(0.8)
        buttonBack.layer.cornerRadius = 10
        buttonBack.addTarget(self, action: #selector(backTapped(_:)), for: .touchUpInside)
    }
    
    public override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
    }
    
    public override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
    }
    
    @objc func backTapped(_ button: UIButton) {
        ui.getVideoPlayer().player.close()
        self.dismiss(animated: true, completion: nil)
    }
}
```

#### NexVideoPlayer.swift

```swift
import Foundation

public class NexVideoPlayer: NSObject {
    lazy var container:UIView = {
        let view = UIView()
        return view
    }()
    
    lazy var playerView:NXPlayerView = {
        let playerView = NXPlayerView()
        playerView.tag = 1
        playerView.autoScaling = NXScale.fitInView
        playerView.autoresizingMask = [UIView.AutoresizingMask.flexibleWidth, UIView.AutoresizingMask.flexibleHeight];
        return playerView
    }()
    
    public var player:NXPlayer { return playerView.player }
    private var abrController:NXPlayerABRController!
    private weak var playerDelegate:NXPlayerDelegate?

    public init(delegate: NXPlayerDelegate) {
        self.playerDelegate = delegate
    }
    
    public func layout(parent: UIView) {
        parent.addSubview(container)
        container.translatesAutoresizingMaskIntoConstraints = false
        container.bounds = parent.bounds
        container.leftAnchor.constraint(equalTo: parent.leftAnchor).isActive = true
        container.rightAnchor.constraint(equalTo: parent.rightAnchor).isActive = true
        container.topAnchor.constraint(equalTo: parent.topAnchor).isActive = true
        container.bottomAnchor.constraint(equalTo: parent.bottomAnchor).isActive = true
        
        container.addSubview(playerView)
        playerView.translatesAutoresizingMaskIntoConstraints = false
        playerView.bounds = parent.bounds
        
        playerView.leftAnchor.constraint(equalTo: container.leftAnchor).isActive = true
        playerView.rightAnchor.constraint(equalTo: container.rightAnchor).isActive = true
        playerView.topAnchor.constraint(equalTo: container.topAnchor).isActive = true
        playerView.bottomAnchor.constraint(equalTo: container.bottomAnchor).isActive = true
 
        player.delegate = playerDelegate
        abrController = NXPlayerABRController(player: player)
    }
    
    public func isPaused() -> Bool {
        return player.state == NXPlayerState.pause
    }
}
```

#### BridgingHeader.h

```
#import <NexPlayerSDK/NexPlayerSDK.h>
#import <NexPlayerSDK/NXPlayerABRController.h>
#import <NexPlayerSDK/NXPlayerDelegate.h>
#import <NexPlayerSDK/NXClosedCaption.h>
#import <WidevineIntegration/WidevineIntegration.h>
#import <WidevineIntegration/NexWidevineDelegate.h>
```