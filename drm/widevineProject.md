## NexPlayer with Widevine project

Here we show a more advance project of NexPlayer with the Widevine DRM integration.

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
