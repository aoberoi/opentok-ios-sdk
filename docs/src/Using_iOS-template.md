Using the OpenTok iOS SDK
=========================

The OpenTok iOS SDK lets you connect to OpenTok sessions, and publish and subscribe to OpenTok audio-video streams.

Developer and client requirements
---------------------------------

* The OpenTok iOS SDK requires XCode 4.2 or later. XCode 4.2 requires Mac OS 10.6.8 or later.

* You need to test OpenTok apps on an iOS device running iOS 5. The OpenTok iOS SDK supports iPhone 3GS and higher, iPod touch 3rd generation and higher, and all iPad versions. 

* The OpenTok iOS SDK supports Wi-Fi only.

* To test OpenTok apps on an iOS device, you will need to register as an Apple iOS developer at
[http://developer.apple.com/programs/register/](http://developer.apple.com/programs/register/).

* Download the latest version of the OpenTok iOS SDK from [GitHub](https://github.com/opentok/opentok-ios-sdk).

Setting up your development environment
---------------------------------------

Included in the OpenTok iOS SDK download file is the OpenTokHello sample app. This app publishes to a demo session, and subscribes to its own stream (or any other stream in the session). Included in the sample app directory is the OpenTok iOS library and other files you will need to develop your own apps.

* **libOpentok.a** -- The OpenTok iOS library. Note that to use the library you must also include the opentok.bundle file and the headers included in in the Frameworks directory of the sample app.

* The **opentok.bundle** file -- This file includes required assets. Include it with your project.

* **Frameworks directory** -- The OpenTok iOS library uses linked frameworks and dynamic libraries provided by iOS. We cannot pre-link them in the libOpentok.a static library, so your project must link them. Expand the "Frameworks" directory of the sample application in XCode project browser. Drag and drop the contents of this directory into your own iOS project.

* **Adding the -ObjC flag** -- Our static library uses Objective-C categories. Your application will crash if you do not load the entire symbol table of the library at linking time. You can read more about this issue [here](http://developer.apple.com/library/mac/#qa/qa1490/_index.html).

	Add -ObjC to the "Other Linker Flags" property of your build target.

* A **docs** directory -- This includes the reference documentation for the OpenTok iOS SDK. Install it into XCode to add documentation and auto-completion of your code.

You can connect to the same OpenTok session that the OpenTokHello sample app uses by going to http://www.tokbox.com/opentok/api/tools/js/tutorials/helloworld.html. You can generate a new session ID at this URL:

http://staging.tokbox.com/hl/session/create

You can also create a web page that connects to the same session as the OpenTokHello sample app. Be sure to load the OpenTok JavaScript library (TB.js) from the following location:

	<script src="http://staging.tokbox.com/v0.91/js/TB.min.js" ></script>

Known issues
------------

* Some features available in the OpenTok SDK for other platforms (such as JavaScript) are not supported in the OpenTok iOS SDK. These unsupported features include peer-to-peer streaming and archiving.

* The OpenTok iOS SDK supports iOS 5 only.

* Our graphics rendering pipeline causes this error to be logged when debugging: "CGContextDrawImage: invalid context 0x0." This should not affect the performance of your app. If you experience video quality issues, please let us know.

For other issues, check the RELEASE_NOTES.txt file in the libOpentok directory.

Using the sample apps
---------------------

* The [OpenTokHello](OpenTokHello.html) sample app shows the most basic functionality of the OpenTok iOS SDK: connecting to sessions, publishing streams,
and subscribing to streams.
* The [OpenTokBasic](OpenTokBasic.html) sample app uses more of the OpenTok iOS SDK than the OpenTokHello sample app does.

Creating your own app using the OpenTok iOS SDK
-----------------------------------------------

Here are the basic steps in creating your own app:

1. In XCode, create a new project. The simplest application is a Single-View application.

2. Open the project navigator in Xcode.

2. Drag the Opentok.framework directory from the Mac OS finder to the Frameworks directory for in XCode.

3. The OpenTok framework requires a few other frameworks and libraries to be added to your project. The easiest way to add them is
to copy them from the OpenTokHello sample app.

	Open the OpenTokHello sample app in XCode. Drag all of the additional frameworks from the frameworks folder (in the project navigator)
	of the OpenTokHello project into the frameworks folder of your project.
	
	The additional frameworks and libraries include the following: AudioToolbox.framework, AVFoundation.framework, CFNetwork.framework,
	CoreAudio.framework, CoreMedia.framework, CoreVideo.framework, libz.dylib, libstdc++.dylib, MobileCoreServices.framework,
	OpenGLES.framework, QuartzCore.framework, Security.framework, SystemConfiguration.framework.

6. In the project manager, select your project and click the Build Settings tab. At the top of the Build Settings tab, click All (to reveal all build settings). Under the Linking section, click to the right of Other Linker Flags, and add `-ObjC`.

Next steps:

1. In the ViewController.h file, add the following line (after `import <UIKit/UIKit.h>`):

		#import <Opentok/Opentok.h>

2. Assuming that your ViewController will implement the OTSessionDelegate, OTPublisherDelegate, and OTSubscriberDelegate protocols,
edit the `@interface` declaration in the ViewController.h file to the following:

		@interface ViewController : UIViewController <OTSessionDelegate, OTSubscriberDelegate, OTPublisherDelegate>

3. You will need to implement the required method in each protocol that you add (OTSessionDelegate, OTSubscriberDelegate, OTPublisherDelegate).

4. Add code to initialize and connect to an OpenTok session. And add code to publish and subscribe to streams.
See the code in the OpenTokHello application.


Switching from staging to production
------------------------------------

When you are ready to distribute your app (or to test a production version of your app), switch from using the OpenTok staging media server to the
OpenTok production media server (see [Testing and production](http://www.tokbox.com/opentok/api/tools/js/documentation/overview/production.html)).
You can specify that your application connects to the OpenTok production server when you call `[OTSession initWithSessionId:delegate:environment:]`.


Connect with TokBox and with other OpenTok developers
-----------------------------------------------------

Your comments and questions are welcome. Come join the conversation at the [OpenTok iOS SDK forum](http://www.tokbox.com/forums/ios).