---
layout: post
title: "Create custom collectionView like Apple’s Shortcuts app in Code"
categories: []
tags:
- apple
- iOS
- tutorial
status: publish
type: post
published: true
meta: {}
---

## Create custom collectionView like Apple’s Shortcuts app in Code

CollectionViews are in almost any of iOS applications and to make your application stands out you should create a good design…

* * * * *

### Create custom collectionView like Apple’s Shortcuts app in Code.

![](https://cdn-images-1.medium.com/max/1200/1*EsxEv5SyOOHSa_fTeEGVYg.png)

CollectionViews are critical to have in almost any of your iOS applications and to make your application stands out you should create a good design. Apple’s Shortcuts app *Library screen* really shows off a great user interface design and still very simplistic and authentic.

* * * * *

**Let’s start** with creating a new project; I will name it ShortcutsCollectionView. Make sure that you have chosen Swift as your Language, save it somewhere on your mac and let’s start coding!

We are making it entirely in code, and we won’t be using the storyboard. So, **First** delete the **Main.storyboard** file and then remove it again from the **Deployment Info** in your target. You should have something looking like this:

![](https://cdn-images-1.medium.com/max/800/1*WmmLTN9FUJ4g1RULK_iNpQ.jpeg)

* * * * *

The second thing that we would have to do is to set up the window. So, in your *AppDelegate.swift* file you add those couple of lines of code to your *didFinishLaunchingWithOptions* method.

* * * * *

Now, if you run the app it will show you a black screen, and that’s amazing! 
So let’s build our collectionView.

I will create the collectionViewCell class first, so let’s create it! **Start** with creating a new Swift file, name it *MainCollectionViewCell.swift*, import **UIKit** instead of Foundation and make a class and call it **MainCollectionViewCell** and of course make it conform to the UICollectionViewCell class. override your *init* method and add *required init*method. Then we will create our UI elements, we need an **edit button**, an **icon image** and a **title** for the cell. Then we will create a setupCell method to help organize our code better, a cellRandomBackgroundColors method, gradientBackgroundColor method, roundCorner method, and a setCellShadow method.

### Random gradient background.

Now, let’s talk about how I created the randomly generated background gradients.
**First,** I took a screenshot from Apple’s Shortcuts app to help me pick the colors that I’ll be working with since I’m aiming for creating a somewhat identical UI.

![](https://cdn-images-1.medium.com/max/800/1*TRpe05Cu5CUPNdgX0JaeWg.jpeg)

**Next,** I created a function that doesn't take any parameters and returns a UIColor array.
**Then,** I created a UIColor array for every two colors since that those two colors will be used to create the gradient.
**Next,** I created a *HashTable* or a *Dictionary* that will have a *key* of type integer and *values* of type UIColor array.
**Finally,** I returned a random element value from that dictionary.

#### **Now our file should look like this:**

<script src="https://gist.github.com/HassanElDesouky/8c9d30af4d05b1142f07db079a2ed9c1.js"></script>

> Note: I have created an extension file to help me with the autoLayout and to set the gradient background color.


Now let’s move to our *ViewController.swift* file. Make it conform to UICollectionViewController and UICollectionViewDelegateFlowLayout. Now if you run your app it will crash, we will solve all of the issues later. But now let’s set up our collectionView and navigationBarController.
In the collectionViewLayout method you need to make the screen fits only two cells. **So it will be something like this:**

```
func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
   return CGSize(width: (view.frame.width / 2) - 20, height: 110)}
```

Now if you run the app it’ll ***crash***, so let’s fix that bug.
**Open** the *AppDelegate.swift* file and change the method that we wrote earlier to this… because now the ViewController is a collectionView.

* * * * *

### Final results:

If you run the app now, **voilà! 
**It has three cells that have different background gradient colors almost like Apple’s Shortcuts App.

If you aren’t a designer you can also buy some great [iOS App Templates](https://www.iosapptemplates.com/) and if you are more interested in [React Native App Templates](https://www.instamobile.io/) you can buy them from here they have a really great collection.

![](https://cdn-images-1.medium.com/max/800/1*MRnUJ_OcfqNBeqgSXQkzjg.png)

* * * * *

### Challenge:

Now every time you run the app, the colors will change. What if you want to save the colors, so it will be generated once and not every time you open the app. **What will you do?**

### The full project on GitHub

Here’s a link to the full project on my GitHub account if you wanted to play with the code yourself.

[**HassanElDesouky/ShortcutsCollectionView**](https://github.com/HassanElDesouky/ShortcutsCollectionView "https://github.com/HassanElDesouky/ShortcutsCollectionView")[](https://github.com/HassanElDesouky/ShortcutsCollectionView)

### Finally:

I hope you liked my first tutorial, and if you do please don’t forget giving it a clap, and I really would appreciate it if anyone has any advice for me to make my next article better.

> Happy coding!

* * * * *

By [Hassan El Desouky](https://medium.com/@hassaneldesouky) on [December 13, 2018](https://medium.com/p/29b1272347e).

[Canonical link](https://medium.com/@hassaneldesouky/create-custom-collectionview-like-apples-shortcuts-app-in-code-29b1272347e)