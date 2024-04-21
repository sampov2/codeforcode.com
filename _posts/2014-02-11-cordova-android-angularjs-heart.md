---
title: "Cordova + Android + AngularJS = ♡"
date: "2014-02-11"
tags: 
  - "android-angularjs-cordova-chromium"
background: "/images/droid.jpg"
layout: post
---

I recently [released an Android application](/2014/02/11/radio-helsinki-player) for listening to my [favorite radio channel](http://www.radiohelsinki.fi) in Helsinki. Writing a mobile app was a long time coming. This is a story of my flip flop.

![Image by Markus Reinhardt](https://images.squarespace-cdn.com/content/v1/52375b95e4b030ffaec4c1f9/1392153094998-OMPH53YUP2CSA14AQE4R/5696426981_9dde938241_o.jpg){: width="100%" }
Image by [Markus Reinhardt](http://www.flickr.com/photos/tuxxilla/5696426981/)

For quite a while, mobile development had interested me, but I had not yet taken the plunge. I did however have a clear picture of how good quality mobile apps should be created: by using native SDKs. [Phonegap](http://phonegap.com/) / [Cordova](http://cordova.apache.org/) were clever hacks, but hacks nevertheless. For mobile applications, UX and integration with platform services & ecosystem are vital. And these are where compromises must be made if not doing native development. And these compromises are bad, I thought.

As the time was ripe for me to actually get off my behind and start teaching myself how to do this, I did whatever any developer would do to start: I downloaded the [Android SDK](http://developer.android.com/sdk/) and looked through a few tutorials. I had heard some nice things about the IDE. It has good integration with the Android emulator and you can easily test layouts on a wide variety of device profiles. I'm also no stranger to strongly typed object oriented languages and very fluent in Java. Considering my bias towards native development, this was going to be a match made in heaven.

Immediately after opening the IDE with a sample project, it hit me. I've always strongly disliked writing UIs. It is tedious and mind numbing, not to mention the anguish of debugging layout issues across different platforms and screen sizes. Looking at the sample application layout, browsing through the different components and attributes for the panes and buttons it dawned on me that this is indeed not HTML but a different animal with different rules and different mechanics.

## Back to the future

Back in 2012 I was introduced to [NodeJS](http://nodejs.org/) and [AngularJS](http://angularjs.org/). These two, especially as a combination, made me take JavaScript seriously both as a language and as a development platform. And not only as a language for the client side, but that's a whole different topic. The NodeJS ecosystem contains wonderful tools to make web development more tolerable. I cannot stress enough how essential it is to write CSS with a proper markup language instead of raw CSS. AngularJS gave web development a proper form and scaffolding it had been missing. Front end code became structured, testable, and reliable over night. I finally found a development model that I enjoyed working with on the front end, not to mention it allowing me to be fantastically productive. I later heard someone say that Java developers familiar with [Spring](http://spring.io/) feel right at home with AngularJS. There is truth to that.

Fast forwarding to the topic on hand. The shock I felt looking at the alien layouting system of the Android SDK was only amplified by my previous triumph over the web. After a spell of wandering around the menus aimlessly, I shut down the IDE and felt like I was at a crossroads. Do I really want to put all that effort into building the skill set necessary for native android development? I'm not building games, doing 3D graphics, or writing HDR camera apps. I do not need to have access to low level resources or push processing power to a device's limits. And these skills would only apply to Android.

## The shift

Not long after hitting this crossroads, I found a very interesting chromium project: [mobile-chrome-apps](https://github.com/MobileChromeApps/mobile-chrome-apps). This is essentially a toolchain and workflow that combines Cordova with Android and iOS SDKs. The promise of this tool is that you can have a mobile application in Google Play or App Store in a matter of hours (App Store approval takes much longer, but you get the gist).

As these experimental tools were made available, I had the idea for the Radio Helsinki Player brewing in my mind. This app was going to be dead simple and going through the process of learning all the ropes of the native SDK did not seem worth the trouble for this app.

I decided to give the _clever_ _hack_ a go.

```
$ . ~/nvm/nvm.sh
$ npm install -g cca
$ cca create radiohelsinki-player
cca v0.0.3
## Checking that tools are installed
Android SDK detected.
## Creating Your Application
...
$ cd radiohelsinki-player
$ cca run android --device
```

Everything worked without a hitch and the template application I had just created started up on my Nexus 5. The development environment was quick to operate and robust. I was back in familiar territory. I had tools to run the application for development using a browser, the SDK emulator, or a real device. The tools could also create APK's for distribution. The stage was set.

## Under the hood

The Radio Helsinki Player is a single screen application written using AngularJS. It has a button to play or pause the stream and the shout box, which is essentially a chat between listeners and the DJs. But at the time I'm writing this post, the shout box is only read only in the app.

Even though the application is very simple, I got to test how Cordova plugins are handled in this toolchain. I used the Cordova AudioHandler plugin for playing back audio. Installation was a breeze:

```
$ cca plugin add org.apache.cordova.core.audiohandler
```

All JS libraries (AngularJS, lo-dash) and assets (icons, images, fonts) are included in the application so nothing extra needs to be retrieved over the network at startup.

Building the final application was very straightforward. Once I had set up a key to sign the application, the key needs to be configured in platforms/android/ant.properties:

```
key.store=/where/ever/is/the/keystore.jks
key.alias=alias
key.store.password=XXXX
key.alias.password=YYYY

```

Then to build the application:

```
$ cca build android --release
```

The APK will be created in the directory platforms/android/ant-build/ . Post the APK in Google Play and you're done!

## Final thoughts

I'm not saying that this toolchain or Cordova in general should be used for all Android development. There is definitely a place for both. My lesson in this was that I was underestimating how important working with familiar techniques for productivity is. You might be able to create a better app, faster, even if the app would generally be thought of as better suited for native development. 

### Positives

- Incredibly fast workflow, from 0 to Google Play in hours. It took me about 4 hours to write the first release of Radio Helsinki Player.
- You get to use AngularJS, it's awesome.
- [Remote debugging an Android device](https://developers.google.com/chrome-developer-tools/docs/remote-debugging) is seamless despite having Cordova in the mix.

### Negatives

- mobile-chrome-apps creates a lot of scaffolding! It's difficult if not impossible for a developer to know what all these files are and what to include in version control. Some files are pure scaffolding, others are build residuals, and some are actually your code!
- Relating the the previous one, 'cca clean' would be great!
- When developing in a desktop browser, 'cca serve \[port\]' needs to have an option to watch for changed files.

All in all, I'm a happy convert!
