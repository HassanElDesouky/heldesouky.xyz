---
layout: post
title: "How I Created Apple’s Shortcuts Icon System"
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

## How I Created Apple’s Shortcuts Icon System

A step-by-step guide on implementing Apple’s Shortcuts Icons
Customization system.

In this tutorial, I will share a step-by-step guide on implementing
Apple’s Shortcuts Icons Customization system.

### How I Created Apple’s Shortcuts Icon System 

#### A step-by-step guide on implementing Apple’s Shortcuts Icons Customization system.

![](https://cdn-images-1.medium.com/max/2560/1*LUayqJvpi3FJX8-sCHVkbA.gif)

#### Introduction 
In this tutorial, I will share with you how I created the icon-creating
system that I see in a lot of apps and I really liked what Apple did in
their Shortcuts app. I have been wondering how do they create such a
thing… how you can customize an icon for a list and not just choose an
already finished icon.

![](https://cdn-images-1.medium.com/max/800/1*KFiCOH0TlpHWvvhg0Amjgg.gif)

Creating Icons

Of course, what I did is that I googled a lot but I didn’t go anywhere.
Therefore, I decided to make my own!

> Note: I know that my approach is far away from perfect and, of course,
> I can improve it a lot better. So, please if you know a better
> approach share it with me.

#### In this article, we will go through:

-   The starter project
-   Describing my approach
-   Adding CoreDataCreating a CoreData Manager model
-   Rely on the CoreData model
-   Implement CreateListController
-   Implement ListIconController
-   Updating the main ViewController
-   The final result and a Conclusion
-   Resources

* * * * *

### The Starter Project 

Previously I tried to create custom collectionView like Apple’s
Shortcuts app. Then I wrote an article about it and you can read it
[here](https://blog.prototypr.io/create-custom-collectionview-like-apples-shortcuts-app-in-code-29b1272347e).

Pull the repo from GitHub and let’s start.

[**HassanElDesouky/ShortcutsCollectionView**](https://github.com/HassanElDesouky/ShortcutsCollectionView)

Run the project in Xcode and you will be starting with something like
this.

![](https://cdn-images-1.medium.com/max/800/1*_3PpBUQPNN0mC4Kd8LRgkQ.png)

### My approach
In order to achieve what I was looking for I manly relyed on
Notification Pattern to pass through the selected icons and colors.

From passing through the icons and background colors I concatenated a
view from that info and then rendered the UIView to a UIImage.

I also used CoreData to store all of the information about the List.

[![](https://cdn-images-1.medium.com/max/800/1*4N4u_wPLkqco5f1S1sX5tA.png)](https://www.paypal.me/HassanElDesouky?locale.x=en_US)

### CoreData 
I was learning CoreData so I choose to use it as the database for my app
as it’s really easy to use and to add in your existing projects.

From **File** choose **New File** *or* by using the keyboard **⌘+N**, then
choose **Data Model** under the **Core Data** tab. Name it **Model** and
click *Create*.

Add a new **Entity** let’s call it List then I’ll add a few attributes:

-   `name` of type **String**
-   `firstColor` of type **Binary Data**
-   `secondColor`of type **Binary Data**
-   `imageData`of type **Binary Data** and in the attributes inspector check on **Allows External Storage**

![](https://cdn-images-1.medium.com/max/1200/1*uXi0W9DgNmKsnRnZiRoN8Q.jpeg)

> The CoreData model with the List entity and its attributes

### CoreData Manager

To make things easy I’ll make a CoreDataManager struct to deal with
CoreData easier.

From **File** choose **New File** *or* by using the keyboard **⌘+N**, then
choose **Swift File**. Name it **CoreDataManager** and click *Create*.

<script src="https://gist.github.com/HassanElDesouky/7a138b96dfbaaf3ec21bb298c1ff9ddf.js"></script>

By the help of this model, I can get the `context `of the CoreData, get all of the lists.

### Rely on CoreData

We will need to make some changes in order to fully rely on CoreData. Go
to **ViewController.swift** and add a new *Property:*

```
var lists = [List]()
```

In *collectionView:numberOfItemsInSection:* method change return
statement from `3` to
`lists.count`

Then, go to **MainCollectionViewCell.swift** and add a list *Property*,
remove the gradients methods so the *setup method* will match the
following.

<script src="https://gist.github.com/HassanElDesouky/2e9d014b081c110241bb032788382af2.js"></script>

Go back to **ViewController.swift** and in *collectionView:cellForItemAt:* method update it; to just pass the list.

<script src="https://gist.github.com/HassanElDesouky/859c810f5a10e99e53b3b476a6c2c24a.js"></script>

Now after we defined the data source for our lists, let’s move to actually create a new list.

### Create a List

I will create a new Storyboard. So again from **File** choose **New File** *or* by using the keyboard **⌘+N**, then choose **Storyboard** I will name it **CreateList** then click *create.*

Add a TableViewController with the following attributes **static cells** and **grouped** then in the first and the only section make them
**2 rows**. In the first row add a **TextField** and in the second row
and a **Label** and an **ImageView,** and change its *accessory* to **Disclosure Indicator.**

Add a **NavigationItem** and both a **LeftBarButton** and a **RightBarButton.**

![](https://cdn-images-1.medium.com/max/800/1*wVmFgCjfSpyGGuoyb4p0wA.jpeg)

Create a new **Swift File** let’s call it **CreateListController** and make it inherits from `UITableViewController` Then go again to the storyboard and set the custom class and the **Storyboard ID** to **CreateListController.**

For testing purposes, go to **ViewController.swift** and in **addNewList** method push our new controller. You will see that the new controller is pushed but of course, nothing is working yet.

Create a `protocol` call it CreateListControllerDelegate.

<script src="https://gist.github.com/HassanElDesouky/c22070444769ed371d0a0ea487a38f37.js"></script>

Create outlets for the bar button item, text field, and icon image view.
Also, create actions for both bar button items, and create the delegate
property.

<script src="https://gist.github.com/HassanElDesouky/f38c051f1c5d67116d44bb5b4e51f57d.js"></script>

Connect the delegate in **addNewList** method inside of **ViewController.swift** file.

<script src="https://gist.github.com/HassanElDesouky/a7130407237547a47b2a89c77abacb82.js"></script>

Connecting the delegate and pushing the CreateList view controller

Then handle empty fields like if the text field is empty the done bar
button should be disabled.

<script src="https://gist.github.com/HassanElDesouky/8de1de200c0f3b99313ecefab4d7666b.js"></script>

Then, of course, to save all of the changes you would have to implement
creating a new list and storing it in CoreData.

<script src="https://gist.github.com/HassanElDesouky/98c9c67979dc74a077119c92150db121.js"></script>

#### Create icon controller

If you took a look at the original Shortcuts app in the icon creating
screen. You will see that.

![](https://cdn-images-1.medium.com/max/800/1*tsXMsLcn4O8tch7hQfbCsA.jpeg)

**IconView**: you will construct the icon and see your result in that
view.
**SegmentedControl**: you will use the segmented control to switch
between the views in the container view.
**ContainerView**: in this view, you will select your desired color,
glyph, or choose an image.

Therefore, I created a similar screen in the **CreateList.storyboard**.

![](https://cdn-images-1.medium.com/max/1200/1*osc3DrjFacLoMQRfujSf6w.jpeg)

Create four new Swift files name them **ListIconController**, **IconColorController**, **IconGlyphController**, and **IconOtherController**.

#### **In**IconOtherController

You will need to handle selecting a photo and passing the photo using
**Notifications** to the **ListIconController.**

<script src="https://gist.github.com/HassanElDesouky/e12539517dc5f53b5e731ed6437fbee3.js"></script>

#### In **IconColorController** 

You will show a collection view and in that collection view you will
show your colors and when choosing a color you will also pass it using
**Notifications**.

<script src="https://gist.github.com/HassanElDesouky/7a9ceaed0d0e957e724f847664293f20.js"></script>

Also, don’t forget to create a **collectionViewCell**.

<script src="https://gist.github.com/HassanElDesouky/5237beb600f334bdc3a82f441c699034.js"></script>

#### In **IconGlyphController**

First, you will need to add the images to your project. I downloaded a
free pack from [FlatIcon](http://flaticon.com) and then dragged them and
added them to the project folder.

Following the same pattern as of selecting an icon and selecting a
background color. In choosing a glyph for your list you will be passing
it by **Notifications**.

<script src="https://gist.github.com/HassanElDesouky/3cf6b3835495c5ed19c309746feebd8a.js"></script>

#### **In ListIconController**

You will need to unwrap the information coming from the notification
observers.

<script src="https://gist.github.com/HassanElDesouky/1d202b490f4796dc63e8a3ed991c788d.js"></script>

You will need to handle changing views based on the segmented
controller.

<script src="https://gist.github.com/HassanElDesouky/aa258f4a48cb6666e9368df3a0bf8a14.js"></script>

And, of course, saving the data to CoreData and rendering the UIView to
an image. And maybe check if there’s an already saved image you will
load it instead of a new one.

<script src="https://gist.github.com/HassanElDesouky/c4aa54e363f3da508a190bdfe5ea1fd7.js"></script>

Also, you will need to create an icon view that will have a gradient
background.

<script src="https://gist.github.com/HassanElDesouky/bda06c338e472151439223410c2c7fa3.js"></script>

Update your Extension file to match the following:

<script src="https://gist.github.com/HassanElDesouky/c40f6102ca5f77c83ea9d3957a26e0a5.js"></script>

> If you are interested in knowing how I saved UIColor with CoreData. I
> used an approach similar to what I used in my previous article — [Save UIColor With UserDefaults in Swift 5](https://heldesouky.xyz/blog/Save-UIColor-With-UserDefaults-in-Swift-5).

### Main **ViewController**

Finally, go to **ViewController.swift** and you will need to update a
couple of things.

In both **viewDidLoad** and **viewWillAppear** methods, you will need to
add the following line in order to fetch the list objects from
*CoreData*.

```
self.lists = CoreDataManager.shared.fetchLists()
```

You will also need to confirm to the **CreateListControllerDelegate** and
implement the `didAddList()` function.

<script src="https://gist.github.com/HassanElDesouky/6895d9028f28f6855ddd9700c64a5b19.js"></script>

### The final result and a Conclusion

Finally, after a lot of work — for me at least. I managed to achieve my
goal of making an icon creating system. It really comes very handily in
a lot of application and it gives the user great user experience.

![](https://cdn-images-1.medium.com/max/800/1*H_eN7rlHYNvQvfuLZNUurQ.gif)

The end result

I’m really happy with my end result maybe there was an easier way of
doing the same task. So if you have any feedback please add a comment
below. I do really appreciate it.

Also, remember If you aren’t a designer you can also buy some great [iOS App Templates](https://www.iosapptemplates.com/) and if you are more
interested in [React Native App Templates](https://www.instamobile.io/)
you can buy them from here they have a really great collection.

#### Improvements

There’s a big room for improvements like for example improving or
refining the code or adding new features like:

-   Editing a list
-   Deleting a list

Therefore, please feel free to pull the repo from GitHub and add when
you are finished adding features to the project submit a PR. PRs are
very welcome.

#### GitHub Project

[**HassanElDesouky/AppleShortcuts**](https://github.com/HassanElDesouky/AppleShortcuts)

And special thanks to [Mohammed ElNaggar](https://twitter.com/MoElnaggar14) for helping out!

* * * * *

I think this article will help a lot of people. Therefore, I’m making it
free. But please if you can tip me I will be so grateful. I’m saving to
get an Apple Developer paid account so I can start uploading apps to the
AppStore and tackle with early betas and a lot of paid only technologies
like CloudKit.

[![](https://cdn-images-1.medium.com/max/800/1*8RA2giRIK2fXze7e57361Q.png)](https://www.paypal.me/HassanElDesouky?locale.x=en_US)

By [Hassan El Desouky](https://medium.com/@hassaneldesouky) on [August
28, 2019](https://medium.com/p/826eabd44886).

[Canonical
link](https://medium.com/@hassaneldesouky/apples-shortcuts-826eabd44886)