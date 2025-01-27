# Integrate Felgo with Existing Apps

This guide describes how to integrate Felgo into existing iOS Xcode projects.

*Felgo Native Integration* comes as a public Cocoapods Podspec.

1. Add *Felgo Native Integration* pod as dependency of your existing Xcode project and run `pod install`:

    ```ruby
	pod 'FelgoIOS', :git => 'https://github.com/FelgoSDK/FelgoIOS.git'
    ```

2. Initialize *FelgoIOS* in AppDelegate:

    ```objc
    #import "FelgoIOS.h"

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    
      // Start the Felgo/Qt runtime at app start in background
      [[FelgoIOS sharedInstance] start];
      
      return YES;
    }
    
    - (void)applicationWillTerminate:(UIApplication *)application {
      // Shutdown the Felgo/Qt runtime again
      [[FelgoIOS sharedInstance] quit];
    }
    ```

3. Add `FelgoIOSView` class (a `UIView` subclass) anywhere from within your *View Controller* code or Interface Builder. 

4. Set the `FelgoIOSView`'s '*qmlSource* property to a URL referencing your QML file:

    ```objc
    #import "FelgoIOSView.h"

    - (void)loadQML {
      self.felgoView.qmlSource = [[NSBundle mainBundle] URLForResource:@"Main" withExtension:@"qml"];
    }
    ```

## Example Application

The folder `NativeIntegrationExample` contains a complete iOS example project
making use of FelgoIOS.
You can open by calling `pod install` and then opening the generated `.xcworkspace`.
  