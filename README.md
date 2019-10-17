# FintezaSDK for iOS 

## Installation and initialization

To install Finteza SDK, use CocoaPods or Carthage package manager or download the file archive from GitHub manually.

### Installing via CocoaPods #

To connect Finteza SDK, add the following string to Podfile of your project:

```pod 'FintezaSDK'```

Next, execute the installation command:

```pod install```

When working with CocoaPods, always use the .xcworkspace file instead of .xcodeproj.

### Installing via Carthage

To connect Finteza SDK, add the following string to Cartfile of your project:

```github "finteza/mobile-sdk-ios"```

### Manual installation

Download and unzip the FintezaSDK-X.X.X.framework.zip file[https://github.com/finteza/mobile-sdk-ios/releases]. Next, transfer FintezaSDK.framework to your project in Xcode.

Enable the "Copy items if needed" option during the installation.
![ "Copy items if needed"](https://www.finteza.com/en/integrations/img/ios-sdk-install.png)

## Initializing SDK in the application 

Open the file of your application delegate and import Finteza SDK:

**Objective-C:**

```#import <FintezaSDK/FintezaSDK.h>```

**Swift:**

```import FintezaSDK```

Initialize SDK in the didFinishLaunchingWithOptions method using website ID and address:

**Objective-C:**

```[Finteza initialize:@"{WEBSITE_ID}" site:@"{WEBSITE_URL}" product:@"{PRODUCT}"];```

**Swift:**

```Finteza.initialize("{WEBSITE_ID}", site: "{WEBSITE_URL}", product: "{PRODUCT}")```

Set the website ID as {WEBSITE_ID}. It can be obtained in the website settings (ID field) of the Finteza panel. Next, set the parameters:

| Parameter | Type | Description | 
| ----------- | ----------- | ----------- |
| site | string | Website domain name, for example, "my.site.com". | 
| product | string | Product name to be used as a prefix for labeling events sent to Finteza by your application. | 
 
You may need it to separate events across different platforms in case you have apps for PC, iOS, Android, etc. For example, if you specify the "iOS App" product and send "Registration" event, the final event name in Finteza will be "iOS App Registration".
 
Set 'nil' to avoid using the prefix.
 
You can change the product name later using the setProduct function:
 
**Objective-C:**
 
```[Finteza setProduct:@"{PRODUCT}"];```
 
**Swift:**
 
```Finteza.setProduct("{PRODUCT}")```

## Application launch events

Add the following code to applicationDidBecomeActive:

**bjective-C:**

```[Finteza activate];```

**Swift:**

```Finteza.activate()```

When calling activate, SDK sends "Install Finish" event to Finteza during the first application launch (if the product prefix is set, then "{PRODUCT} Install Finish").

Also, when calling activate, a new working session starts and the "Session Start" event is registered (if the product prefix is set, then "{PRODUCT} Session Start").

The new session begins only if more than three minutes have passed since the previous time the application became inactive.

## Debugging messages 

In order to test working with SDK, you can enable the output of debugging data to the developer's console. Data on events and displayed ads are shown separately.

### Events

**Objective-C:**

```[Finteza addLogging:FintezaLogModeEvents];```

**Swift:**

```Finteza.addLogging(FintezaLogModeEvents)```

### Ads

**Objective-C:**

```[Finteza addLogging:FintezaLogModeBanner];```

**Swift:**

```Finteza.addLogging(FintezaLogModeBanner)```

**Example**

The following debugging message indicates an event sending error due to the absence of the activate method call:

```[event] cannot send event 'Book Load': call the 'activate' method first```

## NEXT

For further settings and examples please proceed to official documentation page https://www.finteza.com/en/integrations/ios-sdk 
