## RoktWebViewSDK Android

The RoktWebView SDK for Android is is custom WebView that extends [android.webkit.WebView](https://developer.android.com/reference/kotlin/android/webkit/WebView). This WebView adds a JS interface once its initalised, allowing calls to RoktWebViewSDK.open(url) to open in an external browser.

The RoktWebView SDK for Android does 3 things. 
1. Appends RoktWebViewSDK to the user agent string 
2. Enables Javascript
3. Adds the RoktWebView Javascript Interface for capturing RoktWebViewSDK.open() methods


## Demo

![Demo](/assets/demo.gif)


## Instructions

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