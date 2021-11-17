---

layout: page_v2
title: Prebid Mobile Rendering Modules
description: Prebid Mobile Rendering Modules architecture
sidebarType: 2

---

# Prebid Mobile Rendering (Open Beta)

Prebid Mobile release rendering Open Beta API for display and video media types, without impacting the current core feature set or current interfaces. Rendering in the mobile landscape signifies Prebib Mobile will have full ownership of the WebView, inserting any associated ad markup into a Prebid Mobile controlled WebView. Having full control of the WebView gives Prebid Mobile the ability to offer publishers better control of features such as Open Measurement, MRAID, SKAdNetwork, and more. The same is relevant to the rendering of video (VAST) creatives with an internal video player. 
 
{% capture warning_note %}
The initial release of Open Beta rendering will contain a temporary API structure before being released into general availability. Eventually, the original API and rendering API will be merged in the consistent toolset.  
{% endcapture %}
{% include /alerts/alert_important.html content=warning_note %}

## Benefits

Prebid SDK rendering offers the following benefits:

- **Monetization without an Ad Server**: Publishers who do not have a direct sales force or have no use for an ad server, yet wish to access Prebid's mobile demand stack, publishers can render ads directly without relying on any 3rd party SDKs using Prebid Mobile's render modules.
- **Reduced ad delivery latency**: With the Prebid rendering module, Prebid SDK can render ads immediately when demand is returned from Prebid Server or when receiving the render signal from an ad server. The full render process should vastly reduce ad delivery speeds.
- **Less infrastructure**: The Prebid SDK does not rely on Prebid Server's Cache server, reducing the cost and utility of Prebid Server Cache. 
- **Less discrepancy**: Having full control of the rendering process has the potential to reduce discrepancy with ads instantly available (less http calls, less infrastructure, less setup). Additionally, having control of ad rendering allows the publisher to follow open and transparent industry standards or even potentially custom requirements from buyers. 
- **Framework support**: Full support of SKAdNetworks and similar frameworks 
- **MRAID 3.0 support**
- **Flexible Ad Measurement**: Owning the rendering and Open Measurement process allows publishers to potentially configure any measurement provider in a transparent and open source process. Prebid SDK will eventually be IAB Open Measurement certified and listed on the IAB site once complete.  
- **Community driven**: Being a part of Prebid, there is the ability to add features not readily or easily available either through the Ad Server or other SDKs 

## Potential Features

This set of features are not supported yet but they are intended for implementation in the nearest feature.

- **Multiformat Ad Unit** - with rendering Prebid SDK is able to display any bid format in the given inventory regardless of Primary Ad Server capabilities. 
- **Support of Custom Ad Servers** - potentially the Rendering Module can work with any ad server, so publishers won't be limited with GAM and MoPub on Mobile anymore.
- **Rendering Delegation** - prebid SDK potentially can delegate rendering of the winning bid to the Demand Partner SDK if it is required for special creatives.

## How It Works

Prebid Mobile SDK supports two integration scenarios:

* **Pure In-App Bidding** In this scenario, no Primay Ad Server is used. Prebid Mobile SDK renders the winning bid immediately when it is available.
* **Using a Primary Ad Server** Prebid SDK detects when a Prebid line item wins on the Ad Server and renders the cached bd in the owned Web View or Video View.

In both scenarios, Prebid SDK levarages Prebid Server for demand. Below are the flows for both In-App and Primary Ad Server modes:

### Pure In-App Bidding

![In-App Rendering](/assets/images/prebid-mobile/modules/rendering/Prebid-In-App-Bidding-Overview-Pure-Prebid.png)

1. Prebid Rendering Module sends the bid request to the Prebid Server
1. Prebid Server runs the header bidding auction among preconfigured demand partners
1. Prebid Server responses with the winning bid 
1. Prebid Rendering Module renders the winning bid

### Prebid Rendering Module with Primary Ad Server

![Rendering with Primary Ad Server](/assets/images/prebid-mobile/modules/rendering/In-App-Bidding-Integration.png)

1. Prebid Rendering Module sends the bid request to the Prebid server.
1. Prebid server runs the header bidding auction among preconfigured demand partners.
1. Prebid Server responses with the winning bid that contains targeting keywords.
1. Prebid Rendering Module sets up the targeting keywords of the winning bid to the ad unit configuration of Primary Ad Server SDK.
1. Primary Ad Server SDK sends the ad request to the primary Ad Server
1. Primary Ad Server responds with an ad
1. The meta information about the winning ad is passed to the Prebid Rendering Module
1. Depending on the ad response Prebid Rendering Module renders the winning bid or allows Primary Ad Server SDK to show its own winning ad


## Supported Ad Formats

Prebid Mobile Rendering supports the following ad formats:

* Display Banner
* Display Interstitial
* Video Interstitial
* Rewarded Video
* Outstream Video (for GAM, Pure In-App Bidding)

[//]: # (The support of native will be added later)
[//]: # (* Native Styles Ads)
[//]: # (* Native Ads)

## Integration Scenarios

### Android

To integrate Prebid SDK Rendering, developers are required to peform the following actions:

1. If integrating into an ad server, create line items specific for rendering (line items are uniqe for the Rendering Module and do not cooicide with the standard Prebid SDK line items):
    * [GAM](rendering-gam-line-item-setup.html)
    * [MoPub](rendering-mopub-line-item-setup.html)
1. Build the Prebid SDK project [integrate](android-sdk-integration.html) with the Prebid Rendering Module
1. Integrate app with the Prebid SDK Rendering Module scenario
    * Integrate with [Google Ad Manager (GAM)](android-sdk-integration-gam.html) as a Primary Ad Server
    * Integrate with [MoPub](android-sdk-integration-mopub.html) as a Primary Ad Server
    * [Pure In-App Bidding](android-sdk-integration-pb.html) integration without Primary Ad Server
1. Actualize the [integration and targeting](android-sdk-parameters.html) properties.  

### iOS

To integrate Prebid SDK Rendering, developers are required to peform the following actions:

1. If integrating into an ad server, create line items specific for rendering (line items are uniqe for the Rendering Module and do not cooicide with the standard Prebid SDK line items):
    * [GAM](rendering-gam-line-item-setup.html)
    * [MoPub](rendering-mopub-line-item-setup.html)
1. Build the Prebid SDK project [integrate](ios-sdk-integration.html) with the Prebid Rendering Module
1. Integrate app with the Prebid SDK Rendering Module scenario
    * Integrate with [Google Ad Manager (GAM)](ios-sdk-integration-gam.html) as a Primary Ad Server
    * Integrate with [MoPub](ios-sdk-integration-mopub.html) as a Primary Ad Server
    * [Pure In-App Bidding](ios-sdk-integration-pb.html) integration without Primary Ad Server
1. Actualize the [integration and targeting](ios-sdk-parameters.html) properties.

## Additional refences

- [Deep Links Support](rendering-deeplinkplus.html)
- [Impression Tracking](rendering-impression-tracking.html)

    