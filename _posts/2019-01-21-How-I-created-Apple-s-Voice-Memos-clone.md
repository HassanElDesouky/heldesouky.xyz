---
layout: post
title: "How I created Apple’s Voice Memos clone"
categories: []
tags:
- apple
- tutorial
- iOS
status: publish
type: post
published: true
meta: {}
---

## How I created Apple’s Voice Memos clone

Learn how to create a voice recording app, that has audio visualization as well as a record button just like Apple’s Voice Memos app.

* * * * *

### How I created Apple’s Voice Memos clone

![](https://cdn-images-1.medium.com/max/2560/1*gZVacMLXnPfxHQAJfvFDCA.png)

Several months ago, I really wanted to create a voice recorder with an audio visualizer like Apple’s Voice Memos app. As a beginner, I googled a lot but I couldn’t find anything that worked or did what I really wanted. Therefore I decided to go for it and try to build it myself.

Follow my learning path and see how to create a voice recording app, that has audio visualization as well as a record button just like Apple’s Voice Memos app.

### The basic setup.

Of course, I’m going to start by creating a new project. Call it on your own taste, I’m going to call mine VoiceMemosClone. Make sure the app is working and you get this satisfying white screen. Now everything looks great, but before we go any farther let’s break the original Voice Memos app into smaller pieces.

Personally, I find it very difficult to start building/ coding something without preparing first, also I find it very intimidating. Therefore, I like cracking everything into smaller pieces and solve every small task alone.

So if you look at Apple’s Voice Memos app, you’ll find several key features: 
**1. The draggable bottom view.
2. The animation of the recording/ stop button.
3. The audio visualizer while recording.
4. Actual recording.**

Now, let’s build them together!

[![](https://cdn-images-1.medium.com/max/800/1*4N4u_wPLkqco5f1S1sX5tA.png)](https://www.paypal.me/HassanElDesouky?locale.x=en_US)

### Prepare the basic User Interface.

In *Main.storyboard* in the *ViewController*, embed in a *NavigationController*, check *PrefersLargeTitles*, and give it “Voice Memos” as a title.

### **1. The Card View.**

First, add two containerViews to the View Controller. One of them is a RecordingsViewController and the other one is that RecorderViewController. Create a new UIViewController Classes from the File -\> New menu, choose UI Cocoa Touch Class file.

Change the background color of the RecorderViewController to *ViewFlipsideBackgroundColor*, change the size property to Freeform. And In the Size Inspector make the hight 150. Add also a UIView and make it the same size as the ViewController and give it a black color with 45% alpha. In RecordingsViewController add to it a tableView and add also a UIView just like you did in RecorderViewController, and in both UIViews check the Hidden property. Finally, connect the outlets of the UIViews you just created.

![](https://cdn-images-1.medium.com/max/1200/1*zjXh_TKUCrzwhEiHP3_kEQ.jpeg)

I like following [Sean Allen](https://twitter.com/seanallen_dev) approach of building the UI, it’s called “Skeletal Storyboards”. If you don’t know what I’m talking about check out his video [here](https://youtu.be/hIQMQmzitfU). Therefore let’s jump in the RecorderViewController.

In the RecorderViewController we will be doing almost everything. But first, if you took a look at what we are trying to build and analyze it, you will find the following.

![](https://cdn-images-1.medium.com/max/800/1*AXoneKtO_N7M4mC0s3kT_w.jpeg)

So, let’s start with the handle view. In *RecordViewController.swift*add a new *property (*call it*handleView)*and a private method (call it *setupHandleView). Also, s*etup the layout constrains and don’t forget to call *setupHandleView()* in *viewDidLoad*().

<script src="https://gist.github.com/HassanElDesouky/63c6d03a2349e3ac8143ed253aa7ef6f.js"></script>

You will get an error saying *“Argument labels ‘(r:, g:, b:)’ do not match any available overloads”.*That’s because I’ve made an extension file for the UIColor. So, create a new Swift file, call it Extensions and add the following code in it. Some of the code below we will be using it in the future. Everything should work fine now.

<script src="https://gist.github.com/HassanElDesouky/3aded6f035a2de79a8fda8f9f360d53b.js"></script>

### 2. The Record Button.

![](https://cdn-images-1.medium.com/max/600/1*9DKIrRFVSwtxknaPLXL_dQ.gif)

I wanted to create a recording button just like the app and I did a search and found out a great article [here](http://markalldritt.com/?p=1193). In this article Mark Alldritt go through how he created the button animation. I really recommended you to read it. Anyways, just copy the *RecordButton.swift* and the *RecordButtonKit.swift* files alongside with copying the StartRecording and the StopRecording sound files.

To make it work you will have to install the [PRTween pod](https://cocoapods.org/pods/PRTween). So, create a pod file in your project directory and install it. The pod is in Objective-C. Therefore, we will have to create an Objective-C Bridge file.

To create the Objective-C Bridge file: from File -\> New -\> File, choose Header File, it’s really important what you will name your header file so **pay attention** here “nameOfYourProject*-Bridging-Header.h”.

*I will name mine* **VoiceMemosClone-Bridging-Header.h**

add it to your project folder. Finally, choose your app target and go to Build Settings, make sure All is selected on top, find Objective-C Bridging Header and give it the path of your header file.

![](https://cdn-images-1.medium.com/max/800/1*bbKcRHT7adBpBtcgiQVclw.jpeg)

Open the header file that you just created, delete everything from it, and just type this following line of code.

```
#import <PRTween/PRTween-umbrella.h>
```

Now, in your *RecorderViewController.swift* file add the button, its constraints, and add your *handleRecording* function. As always don’t forget to call it in your viewDidLoad method.

<script src="https://gist.github.com/HassanElDesouky/bbef3ec2584f061023ff7776c263bb39.js"></script>

Now we need to show a couple of things when you click on the recordButton; the audioView and the timeLabel. So, add a label and a uiview(for now) to the recorderViewController. When we tap on the button we need some animation on the card view, here is what I did.

<script src="https://gist.github.com/HassanElDesouky/80646bf1b2dd19d76456dc66286ef95e.js"></script>

### 3. AudioVisualizerView

Create a UIView class and the following to it, to create the audio visualizer.

<script src="https://gist.github.com/HassanElDesouky/38a6d07b4a039b0bb3259ce28257b230.js"></script>

Now, in *RecorderViewController.swift* change the audioView to:

```
var audioView = AudioVisualizerView()
```

Now you just need to set up the recorder and actually record!

### The final result.

![](https://cdn-images-1.medium.com/max/800/1*OKYCiP3V0sZgeCcRZ6UdCA.gif)

I’m really happy with the final result… however, there are a few enhancements that maybe you could make it to this project, like: 
1. Adding a deleting functionality.
2. Add auto layout, because it’s now only working on iPhone X or XS.
3. Make the cardView (Recorder) draggable.**

### Conclusion.

Ultimately I’m really happy with what I was able to achieve. Not only is it functional, but I had a lot of fun doing it!

I’d love to hear about any experiences you may have about a similar project. I’d also like to see what you may do differently to achieve a better result.

I’m now looking forward to the next blog, what should I try to build next?

If you aren’t a designer you can also buy some great [iOS App Templates](https://www.iosapptemplates.com/) and if you are more interested in [React Native App Templates](https://www.instamobile.io/) you can buy them from here they have a really great collection.

### The full project is on GitHub.

Feel free to use it!

[**HassanElDesouky/VoiceMemosClone**](https://github.com/HassanElDesouky/VoiceMemosClone "https://github.com/HassanElDesouky/VoiceMemosClone")[](https://github.com/HassanElDesouky/VoiceMemosClone)

### Resources.

I couldn't have ever gotten to this results without these guys great work. So, please check them out.

1. The record button by Mark Alldritt, GitHub repo [here](https://github.com/alldritt/RecordButton).
2. Simple Recorder by Sergey Yuryev, GitHub repo [here](https://github.com/snyuryev/SimpleRecorder).
3. How to record audio by Paul Hudson, tutorial link [here](https://www.hackingwithswift.com/example-code/media/how-to-record-audio-using-avaudiorecorder).

Shoutout to:
[**Mohammed Elnaggar**](https://twitter.com/MoElnaggar14)
[**Mohammed Ennabah**](https://twitter.com/M_Ennabah)
[**Lisa Dziuba**](https://twitter.com/LisaDziuba)

[![](https://cdn-images-1.medium.com/max/800/1*8RA2giRIK2fXze7e57361Q.png)](https://www.paypal.me/HassanElDesouky?locale.x=en_US)

By [Hassan El Desouky](https://medium.com/@hassaneldesouky) on [January 21, 2019](https://medium.com/p/b6cd6d65f580).

[Canonical link](https://medium.com/@hassaneldesouky/how-i-created-apples-voice-memos-clone-b6cd6d65f580)
