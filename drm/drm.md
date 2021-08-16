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

## NexPlayer with Widevine project

Now lets see a more advance project of NexPlayer with the Widevine DRM integration.

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
    public func nexPlayer(_ nxplayer: NXPlayer!, completedAsyncCmdOpenWithResult result: NXError, playbackType Type: NXPlaybackType) {
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
