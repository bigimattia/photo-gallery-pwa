# ionic-angular-pwa

## Setup

> npm install

## Live reload
Browser:
> ionic serve

Ios:
> ionic cap run ios -l --external

Android:
> ionic cap run android -l --external

## Build

If you’re still running ionic serve in the terminal, cancel it. Complete a fresh build of your Ionic project, fixing any errors that it reports:

> ionic build

> ionic cap add ios
> 
> ionic cap add android

Every time you perform a build (e.g. ionic build) that updates your web directory (default: www), you'll need to copy those changes into your native projects:
> ionic cap copy

Note: After making updates to the native portion of the code (such as adding a new plugin), use the sync command:
> ionic cap sync

## Android deploy

First, run the Capacitor open command, which opens the native Android project in Android Studio:

> ionic cap open android

Similar to iOS, we must enable the correct permissions to use the Camera. Configure these in the AndroidManifest.xml file. Android Studio will likely open this file automatically, but in case it doesn't, locate it under android/app/src/main/.

Scroll to the Permissions section and ensure these entries are included:
> <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
> <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

Save the file. With permissions in place, we are ready to try out the app on a real device! Connect an Android device to your computer. Within Android Studio, click the "Run" button, select the attached Android device, then click OK to build, install, and launch the app on your device.

## iOS deploy

First, run the Capacitor open command, which opens the native iOS project in Xcode:
> ionic cap open ios

In order for some native plugins to work, user permissions must be configured. In our photo gallery app, this includes the Camera plugin: iOS displays a modal dialog automatically after the first time that Camera.getPhoto() is called, prompting the user to allow the app to use the Camera. The permission that drives this is labeled “Privacy - Camera Usage.” To set it, the Info.plist file must be modified [(more details here)](https://capacitorjs.com/docs/ios/configuration?_gl=1*1fv1pgy*_ga*OTIyNjgxMjEwLjE2NzY5ODk1MjU.*_ga_REH9TJF6KF*MTY3ODk1MzE4OC43LjEuMTY3ODk1NDY0NC4wLjAuMA..). To access it, click "Info," then expand "Custom iOS Target Properties."

Each setting in Info.plist has a low-level parameter name and a high-level name. By default, the property list editor shows the high-level names, but it's often useful to switch to showing the raw, low-level names. To do this, right-click anywhere in the property list editor and toggle "Raw Keys/Values."

Add the NSCameraUsageDescription Key and set the Value to something that describes why the app needs to use the camera, such as "To Take Photos." The Value field is displayed to the app user when the permission prompt opens.

Follow the same process to add the other two Keys required of the Camera plugin: NSPhotoLibraryAddUsageDescription and NSPhotoLibraryUsageDescription.

Next, click on App in the Project Navigator on the left-hand side, then within the Signing & Capabilities section, select your Development Team.

With permissions in place and Development Team selected, we are ready to try out the app on a real device! Connect an iOS device to your Mac computer, select it (App -> Matthew’s iPhone for me) then click the "Build" button to build, install, and launch the app on your device:

## Distribution
[Ionic guide](https://ionicframework.com/docs/angular/your-first-app/distribute)
