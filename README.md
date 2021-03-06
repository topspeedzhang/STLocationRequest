<p align="center">
<img width=300 src="./Preview/STLocationRequest_AppIcon.jpg" alt="STLocationRequestAppIcon" title="STLocationRequestAppIcon">
</p>
# STLocationRequest

[![Swift 2.2](https://img.shields.io/badge/Swift-2.2-orange.svg?style=flat)](https://developer.apple.com/swift/)
[![Version](https://img.shields.io/cocoapods/v/STLocationRequest.svg?style=flat)](http://cocoapods.org/pods/STLocationRequest)
[![License](https://img.shields.io/cocoapods/l/STLocationRequest.svg?style=flat)](http://cocoapods.org/pods/STLocationRequest)
[![Platform](https://img.shields.io/cocoapods/p/STLocationRequest.svg?style=flat)](http://cocoapods.org/pods/STLocationRequest)
[![codebeat badge](https://codebeat.co/badges/ce1c3749-fca8-4c3b-ae28-6210fd0e129a)](https://codebeat.co/projects/github-com-sventiigi-stlocationrequest)

STLocationRequest is a simple and elegant way to request the user location at the very first time written in Swift. It shows a beautiful 3D 360 degree Flyover-MapView over 21 citys or landmarks.

<p align="center">
<img src="./Preview/STLocationRequest.gif" alt="STLocationRequest" title="STLocationRequest">

</p>

## Installation

STLocationRequest is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'STLocationRequest'
```

## Usage

To present the `STLocationRequest`-Controller 

```swift
import STLocationRequest

class ViewController : UIViewController, STLocationRequestDelegate {

    func presentLocationRequest(){
        let locationRequest = STLocationRequest()
        locationRequest.titleText = "We need your location for some awesome features"
        locationRequest.allowButtonTitle = "Alright"
        locationRequest.notNowButtonTitle = "Not now"
        locationRequest.authorizeType = .RequestWhenInUseAuthorization
        locationRequest.delegate = self
        locationRequest.presentLocationRequestController(onViewController: self)
    }
    
}

```

## Customizing

To perfectly match the design to your app, simply playaround with the parameters `mapViewAlphaValue` and `backgroundColor` to get your very own design.

```swift
/// The alpha value for the MapView
locationRequest.mapViewAlphaValue = 0.7

/// The backgroundcolor for the view of the STLocationRequestController
locationRequest.backgroundColor = UIColor.orangeColor()
```

<p align="center">
<img width=200 src="./Preview/STLocationRequest_Purple.jpg" alt="STLocationRequest" title="STLocationRequest">
<img width=200 src="./Preview/STLocationRequest_Green.jpg" alt="STLocationRequest" title="STLocationRequest">
<img width=200 src="./Preview/STLocationRequest_Orange.jpg" alt="STLocationRequest" title="STLocationRequest">
<img width=200 src="./Preview/STLocationRequest_Red.jpg" alt="STLocationRequest" title="STLocationRequest">
</p>

Furthermore you can change the behavior of the `STLocationRequest`-Controller by changing these attributes on your purpose.

```swift
// Defines if the pulse Effect which will displayed under the location symbol should be
// enabled or disabled. Default Value: true
locationRequest.pulseEffectEnabled = true

// The color for the pulse effect behind the location symbol. Default value: white
locationRequest.pulseEffectColor = UIColor.whiteColor()

// Set the location symbol icon which will be displayed in the middle of the STLocationRequest-Controller.
// The devault value is FALocationArrow. You can browse at http://fontawesome.io/icons/ or 
// https://github.com/Vaberer/Font-Awesome-Swift for other icons but be aware to use a icon 
// which is in the context of a location request.
locationRequest.locationSymbolIcon = FAType.FALocationArrow

// The color of the location symbol which will be presented in the middle of 
// the location request screen. Default value: white
locationRequest.locationSymbolColor = UIColor.whiteColor()

// Defines if the location symbol which will be presented in the middle of
// the location request screen is hidden. Default value: false
locationRequest.locationSymbolHidden = false

// Set the in the interval for switching the shown places in seconds. Default value is 15 seconds
locationRequest.timeTillPlaceSwitchesInSeconds = 15.0
```

## Delegate

You can apply to the `STLocationRequestDelegate` to get notified if the user has authorized or denied the location services, tapped the _Not-Now_ Button or if the `STLocationRequestController` did presented or did disappear.

```swift

func locationRequestControllerDidChange(event: STLocationRequestEvent) {
    switch event {
        case .LocationRequestAuthorized:
            break
        case .LocationRequestDenied:
            break
        case .NotNowButtonTapped:
            break
        case .LocationRequestDidPresented:
            break
        case .LocationRequestDidDisappear:
            break
    }
}

```

## Info.plist

Also don't forget to add the usage description key to your `Info.plist` for you selected authorization type.

STLocationAuthorizeType.**RequestWhenInUseAuthorization**
```swift
<key>NSLocationWhenInUseUsageDescription</key>
<string>PUT IN YOUR LOCATION EXPLANATION TEXT</string>
```

STLocationAuthorizeType.**RequestAlwaysAuthorization**
```swift
<key>NSLocationAlwaysUsageDescription</key>
<string>PUT IN YOUR LOCATION EXPLANATION TEXT</string>
```

This text will be shown in the default iOS location request dialog, which will show up when the user tapped the allow button.

<p align="center">
<img src="./Preview/iOSLocationRequestDialog.png" alt="iOSRequestDialog" title="iOSRequestDialog" width=300>

</p>

For more details check out the example application.

## iOS Simulator

Please mind that the 3D Flyover-View will only work on a real iOS device (not in the Simulator) with at least iOS 9.0 installed. A Screenshot taken from an **iOS Simulator** running `STLocationRequest`-Controller.

<p align="center">
<img src="./Preview/iOSSimulatorBehavior.jpg" alt="iOSSimulatorBehavior" title="iOSSimulatorBehavior" width=300>

</p>

## Objective-C

To present the `STLocationRequest`-Controller in an `Objective-C` project you can go like this.

```objective-c
#import "ViewController.h"
@import STLocationRequest;

@interface ViewController () <STLocationRequestDelegate>
@end

@implementation ViewController

-(void)presentLocationRequest{
    STLocationRequest *locationRequest = [STLocationRequest new];
    locationRequest.titleText = @"We need your location for some awesome features";
    locationRequest.allowButtonTitle = @"Alright";
    locationRequest.notNowButtonTitle = @"Not now";
    locationRequest.mapViewAlphaValue = 0.9;
    locationRequest.backgroundColor = [UIColor lightGrayColor];
    locationRequest.authorizeType = STLocationAuthorizeTypeRequestWhenInUseAuthorization;
    locationRequest.delegate = self;
    [locationRequest presentLocationRequestControllerOnViewController:self];
}

-(void)locationRequestControllerDidChange:(enum STLocationRequestEvent)event{
    switch (event) {
        case STLocationRequestEventLocationRequestAuthorized:
            break;
        case STLocationRequestEventLocationRequestDenied:
            break;
        case STLocationRequestEventNotNowButtonTapped:
            break;
        case STLocationRequestEventLocationRequestDidPresented:
            break;
        case STLocationRequestEventLocationRequestDidDisappear:
            break;
    }
}

```

## Author

Sven Tiigi (http://sven.tiigi.de)

## License

```
STLocationRequest
Copyright (c) 2015 Sven Tiigi <sven@tiigi.de>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```
