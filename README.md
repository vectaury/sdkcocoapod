# **Vectaury**
## **Prerequisites**
* You need an API key. [You can request an API key here](https://cdn.vectaury.io/static/sdk/index.html).
* From iOS 10, set "NSLocationAlwaysUsageDescription" and "NSLocationWhenInUseUsageDescription" in the Info.plist file.
* From iOS 11, set "NSLocationAlwaysAndWhenInUseUsageDescription" and "NSLocationWhenInUseUsageDescription" in the Info.plist file.
## **Instalation**

### Using CocoaPods (Recommended)
* Add Vectaury dependance to Podfile
* ```pod "Vectaury"```
* In your shell, run
* ```pod install```
* Download the Setting.bundle file : [Setting.bundle](../../ios/Settings.bundle-1.5.zip)
* Add the Settings.bundle file to your project and target the application (if you already have a Settings.bundle file, skip this step and follow [this instruction](#note) )

### Linking the framework directly
* Download the framework
* [Version 1.5](../../ios/Vectaury-ios-1.5.zip)
* Extract the zip and link the binary with the library.
<img src="https://cdn.vectaury.io/sdk/doc/ios/images/lib-ios.png" alt="lib-ios" style="width:100%;">
* Add the path of the framework in your target's build settings "framework search path"
* Add the Vectaury.framework/Settings.bundle file to your project and target the application (if you already have a Settings.bundle file, skip this step and follow [this instruction](#note) )
> Before submitting your app to AppStore, you must exclude the iOS simulator build from the framework

### Note <a class="note"></a>:
if you already have a Settings.bundle in your project, you just need to copy language folder and add in your root.plist file :
``` xml
<dict>
    <key>StringsTable</key>
    <string>Root</string>
    <key>PreferenceSpecifiers</key>
    <array>
        <dict>
            <key>FooterText</key>
            <string>Txt</string>
            <key>Type</key>
            <string>PSGroupSpecifier</string>
            <key>Title</key>
            <string>Privacy</string>
        </dict>
        <dict>
            <key>Type</key>
            <string>PSToggleSwitchSpecifier</string>
            <key>Title</key>
            <string>DataVectaury</string>
            <key>Key</key>
            <string>io.vectaury.userOptInOut</string>
            <key>DefaultValue</key>
            <true/>
        </dict>
    </array>
</dict>
```
## **Integration**
### 1 - Init Vectaury SDK from the AppDelegate.m file
* Import Vectaury
* Init SDK with ```initWithApiKey:withLaunchOptions:withPush: ``` function on :
```
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {}
```
### 2 - Ask for Authorization
Ask the user to share their location data (popup) with the ```+requestAuthorization:``` function.

> Put this line where it makes the most sense for your app user experience. This will trigger a permission request popup. If you already asked thoses permissions elsewhere in your app, you don't need to call it (if you do, it will have no impact).

**Enable Background Mode**
You need to tick the box "Location updates" in the "Capabilities" of your target.
<img src="https://cdn.vectaury.io/sdk/doc/ios/images/background-ios-location.png" alt="background-ios" style="width:100%;">
### 3 - Start Location tracking position
* Start to collect location data with ```+startLocation ```function
### Exemple (Swift 4) :
``` swift
...
import Vectaury
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    ...
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions:     [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
        Vectaury.initWithApiKey("key", withLaunchOptions: launchOptions, withPush: false)
        //Optional : request authorization using vectaury SDK
        Vectaury.requestAuthorization()
        Vectaury.startLocation()
        return true
    }
    ...
}
```
## **Change Logs**
### **SDK 1.5.1 - 12 february 2018**
* Fix wording on opt-in pop-up
### **SDK 1.5 - 02 february 2018**
* New system of location data collecting
* Optimization of batterie use
### **SDK 1.4  - 13 november 2017**
* Setting.bundle : The user can opt-out Vectaury data sharing from the app settings
* New algorithm of location data collecting
* Opt-in banner display option
* Educational popup display option
* Link to settings banner display option
### **SDK 1.3.3 - 23 October 2017**
* Fix Bug on Blue Bar
### **SDK 1.3.2  - 20 October 2017**
* New algorithm of location data collecting
