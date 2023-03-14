## RoktWebViewSDK Android

**This project is no longer maintained**
--

The RoktWebView SDK for Android is a custom WebView that opens links in an external browser instead of in the same WebView.


| Environment | Build |
| ----------- | :----- |
| release | [![Build status](https://badge.buildkite.com/ead4486004439bfee871822ed4408d6c1f2f684f08a851ca5d.svg)](https://buildkite.com/rokt/android-webviewsdk)

## Requirements

Download [Android Studio](https://developer.android.com/studio). Project is configured to run on Android API 18 or above and compiled against API 29.

## Project structure

This project consists of 2 modules: [**roktwebviewsdk**](roktwebviewsdk) library module and [**app**](app) application module.
**roktwebviewsdk**: the library module containing all the sdk functionality and contains all the unit tests. It can be exported as .aar archive and imported into another project as a [Gradle](https://gradle.org/) dependency  
**app**: example application for demonstrating the usages of roktwebviewsdk in partner applications. All the UI tests are in this package.

## How to build example project locally?

1. Open Android Studio
2. Open project by selecting project folder
3. Wait for Gradle to sync dependencies
4. Click on green run button and select the device (physical or emulator) to run on

## How to run UI tests locally?

Connect a device or emulator and run in terminal when in main project folder: `./gradlew assemble app:assembleAndroidTest`
or run each test from Android Studio using a run button next to each one. Tests can be found in: `app/src/androidTest/java/com/rokt/roktwebviewsample/`

Note: Make sure you disable animations on the emulator before running UI Tests and make sure you have selected the mock build variant.
You can disable animations by running these commands:
   ```
adb shell settings put global window_animation_scale 0.0
adb shell settings put global transition_animation_scale 0.0
adb shell settings put global animator_duration_scale 0.0
   ```

## How to run Unit tests locally?
Open Terminal and go to root of the project and execute: `./gradlew roktwebviewsdk:testDebugUnitTest`

or Local Unit test cases can also be executed using fastlane
```
   bundle install
   bundle exec fastlane test
   ```

## SDK Dependencies

All the dependencies for sdk are listed in roktwebviewsdk/build.gradle. To add/update the dependencies modify the config.gradle first and then
update in build.gradle.

## CI/CD System

The CI system used is **Buildkite**  https://buildkite.com/rokt/android-sdk-build
Buildkite pipelines are defined in the `.buildkite` directory. There are two seperate lanes that are executed based on branch names.
Branches with **release-** prefix are considered production branches, the publish step will release to the production maven respository.
All other branches are considered alpha branches, so it will publish to maven with with **-alpha** postfix.
It uses **docker** container for executing the build steps using the **Fastlane** build tool. The steps are configured in the `fastlane/Fastfile`

## Demo

![Demo](/assets/demo.gif)

## Publishing
We publish our library to Jitpack which requires us to have code in github. To create a release, in Github click on create a new release.
Releases will determine the version of our library. Click on Choose a tag and enter your initial version of the library and click Enter. 
Also, enter the title of release and a description of the library. Finally, click on Publish release to publish.

### How to publish locally
Use below gradle commands to publish the library to ($HOME/.m2/repository)
```
./gradlew assemble 
./gradlew publishProductionPublicationToMavenLocal
```

## Usage

Setting up the RoktWebView SDK is the same process as including a standard WebView described in the [Android Docs](https://developer.android.com/guide/webapps/webview).

### Step 1: Add the Rokt Placement plugin
1. Open the build.gradle file for your app module.
2. Add the RoktWebViewSDK library to the dependencies section.
```
dependencies {
    implementation 'com.rokt:roktwebviewsdk:1.0.0'
}
```

### Step 2: Add the RoktWebView to your layout

Add the RoktWebView to your layout. For example: 
```
<?xml version="1.0" encoding="utf-8"?>
   <com.rokt.roktwebviewsdk.RoktWebView
       android:id="@+id/webView"
       android:layout_width="match_parent"
       android:layout_height="match_parent"/>

```

Or to add it programmatically in your onCreate(), use similar logic to the following: 

**Kotlin**
```
val myWebView = RoktWebView(activityContext)
setContentView(myWebView)
```

**Java**
```
WebView myWebView = new RoktWebView(activityContext);
setContentView(myWebView);
```
### Step 3: Load a web page
To load a web page in the RoktWebView, use loadUrl(). For example:

**Kotlin**
```
val myWebView: RoktWebView = findViewById(R.id.webview)
myWebView.loadUrl("https://www.rokt.com")
```

**Java**
```
WebView myWebView = (RoktWebView) findViewById(R.id.webview);
myWebView.loadUrl("https://www.rokt.com");
```

### License
Please see [LICENSE](/LICENSE.md)