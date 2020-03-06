---
layout: post
title: "Save UIColor With UserDefaults in Swift 5"
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


## Save UIColor With UserDefaults in Swift 5

I wanted to save UIColor into UserDefaults so I googled it and I
couldn’t find any updated resource to Swift 5. Therefore, I came up
with…

### Save UIColor With UserDefaults in Swift 5

![](https://cdn-images-1.medium.com/max/800/1*tQaKld0tddpG8xR6ERbMsA.png)

I wanted to save `UIColor` into `UserDefaults` so I googled it and couldn’t find any updated resource for [Swift](https://developer.apple.com/swift/) 5. Therefore, I came up with my own solution. Hopefully, it’s helpful.

There’s no straight way to save `UIColor` with `UserDefaults` so we will have to manipulate the type a bit.

We are going to convert `UIColor` to
`Data `and save it as
`any?`. To convert the type of
`UIColor`, we will need to use a special
method called `NSKeyedArchiver`.

> "`NSKeyedArchiver`, a concrete
> subclass of `NSCoder`,
> provides a way to encode objects (and scalar values) into an
> architecture-independent format that can be stored in a file. When you
> archive a set of objects, the class information and instance variables
> for each object are written to the archive. The companion class
> `NSKeyedUnarchiver` decodes
> the data in an archive and creates a set of objects equivalent to the
> original set.”* — Apple*

Therefore, let’s make an extension to the `UserDefaults`.

We’ve converted `UIColor` to
`Data` and then saved it as
`Any?`. Then, we used the unarchiver to
unarchive `data `and return the
`UIColor`.

Also, If you aren’t a designer you can also buy some great [iOS App
Templates](https://www.iosapptemplates.com/) and if you are more
interested in [React Native App Templates](https://www.instamobile.io/)
you can buy them from here they have a really great collection.

* * * * *

### Resources 

-   [How to save and load objects with NSKeyedArchiver and
    NSKeyedUnarchiver](https://www.hackingwithswift.com/example-code/system/how-to-save-and-load-objects-with-nskeyedarchiver-and-nskeyedunarchiver)
-   [Store UIColor with UserDefaults in Swift
    3](https://www.sitepoint.com/store-uicolor-with-userdefaults-in-swift-3/)
-   [iOS App Templates](https://www.iosapptemplates.com/)
-   [React Native App Templates](https://www.instamobile.io/)

By [Hassan El Desouky](https://medium.com/@hassaneldesouky) on [July 22,
2019](https://medium.com/p/951ef1aa88e8).

[Canonical
link](https://medium.com/@hassaneldesouky/save-uicolor-with-userdefaults-in-swift-5-951ef1aa88e8)

Exported from [Medium](https://medium.com) on February 29, 2020.
