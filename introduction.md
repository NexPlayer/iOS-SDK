# NexPlayer SDK for iOS Documentation
*Last updated December 2, 2020*

### 1.1 Legal Notices

**Disclaimer for Intellectual property**

This product is designed for general purpose, and accordingly the customer is responsible for all or any of intellectual property licenses required for actual application. NexPlayer Corp. does not provide any indemnification for any intellectual properties owned by third party.

**Copyright**

Copyright for all documents, drawings and programs related with this specification are owned by NexPlayer
Corp. All or any part of the specification shall not be reproduced nor distributed without prior written approval by NexPlayer Corp. Content and configuration of all or any part of the specification shall not be modified nor distributed without prior written approval by NexPlayer Corp.

© Copyright 2010-2020 NexPlayer Corp. All rights reserved.

### 1.2 Abstract

This document describes NexPlayer SDK for iOS version 5.40 and how to use the API functions of NexPlayer SDK v5.40.x

> **Note** The current API is based on Objective-C. For the best development experience, and to access the newer NexPlayer features, new applications should use the Objective-C API. Developers are strongly encouraged to migrate existing applications to the new API as well.

NexPlayer SDK adds support for modifying HTTP requests sent to servers (`NXPlayerDelegate::nexPlayer:onModifyHttpRequest:`) 

In addition to recently added support for caption rendering attributes like text modes, rendering options and other rending settings, for retrieving playback statistics (`NXStatsInfo`) like decoded and rendered frame rates and support for user-selected caption styles (currently only for CEA 608 and WebVTT) and for custom ID metadata tags in addition to basic support for CEA 708 closed captions, WebVTT text tracks, and 3GPP/TTML timed text, a new method, getSeekableRange, to check the range in content where seeking is possible as well as support for SmoothStreaming LiveBackOff and LiveBackOffset, support for handling manifests and playlists, and descrambling modules for Piff PlayReady and Progressive Download content, as well as other new features. NexPlayer continues to support features from earlier versions such as CEA 608 closed captions, Apple’s HTTP Live Streaming (HLS), MS Smooth Streaming, an interface for descrambling DRM content, and progressive download. The precise feature set available depends on the SDK edition.

The developers of iOS Applications benefit from NexPlayer SDK, which allows developers to easily build custommedia players, without needing to worry about how content is transported. In addition, NexPlayer SDK is reliable and robust, and has proven compatibility with international standards, without sacrificing performance.
