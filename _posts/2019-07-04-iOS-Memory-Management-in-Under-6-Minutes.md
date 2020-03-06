---
layout: post
title: "iOS Memory Management in Under 6 Minutes"
categories: []
tags:
- objective-c
- iOS
- memory-management
status: publish
type: post
published: true
meta: {}
---

## iOS Memory Management in Under 6 Minutes

Everything you should know about ARC in old good Objective-C.

### iOS Memory Management in Under 6 Minutes

#### What you should know about ARC in old good Objective-C

![](https://cdn-images-1.medium.com/max/2560/1*nkLi2YLBO3xys_dehSXoQw.png)

In the last couple of days, I was searching more on memory management in
iOS. It was a kind of a hard topic for me to understand in Swift.
Therefore, I decided to go a little deeper in old good Objective-C — as
I’m learning it already, to understand memory management more and get an
in-depth understanding of that topic. Like, how was is it before the
ARC? What happened after it? And what is the difference between ARC and
Garbage Collector?… etc.

#### Introduction

When you start working with objects, you will notice an interesting
thing.

Objects are more demanding on memory than primitive types like integers
and floats. This remains true whether these objects are from your own
classes or they are objects you make from classes in any of the Apple
frameworks.

Luckily we don’t have to worry about working manually with memory
addresses and manually allocating or deallocating areas of memory (which
is still true for some languages). Instead in Objective-C, we use
something called reference counting.

[![](https://cdn-images-1.medium.com/max/800/1*4N4u_wPLkqco5f1S1sX5tA.png)](https://www.paypal.me/HassanElDesouky?locale.x=en_US)

#### What does reference counting mean?

When your application starts, an area of memory became available for
your objects. So you create an object and an area of memory is claimed
for that object. Now, the variable that holds the object is a pointer to
that object. A pointer to an area of memory to be exact. What happens
under the hood is that when the object was created it’s been given
what’s called a **retain count** or a **reference count** and it
represents the number of owners for a particular object. Therefore, we
can imagine it to be one, as you see on the image below:

![](https://cdn-images-1.medium.com/max/800/1*B0Qm_tMY5NpfXA8rwyoiDA.jpeg)

The variable that called var is a pointer to a block of memory. So, in
your program, you work with that pointer and call methods on it as long
as you want. But when you arrive at the end of the code block. This
variable is no longer reachable or accessible by any part of the
program. The **retain count** goes again to zero because there’s nothing
pointing to that block of memory now. And when the **retain count** become zero the runtime engine says, here’s a block of memory
that no one cares about. Therefore, it will release this block of memory
and make it available to other objects to use.

#### What might go wrong?

The only issue here can be in situations when you are creating objects
and passing them around from one place to another. So it’s not clear
that the pointer is still in scope or not. And up until 2011 — when
**ARC** (*Automatic Reference Counting*) was added, you had to write
statements on when you were finished using that object.

#### Before ARC

Before ARC was added to Objective-C we would have to do something like
this

```
    MyClass *myObject = [[MyClass alloc] init];[
    myObject myMethod]; // call methods... 
    // doing some stuff with the object
    [myObject release]; // releasing the object
```

We’d write a little bit of code to create an object. It would be
created. We’d call methods of that object. But at some point, we would
have to actually explicitly call a `release` statement. And that would be what was responsible for
taking a retain count down.

This is not a problem with a small number of objects. But when you had
hundreds or thousands of objects being created, manipulated, used as
parameters, passed from object to object… you had to keep track of them
all. If you were passing an object from one area of your program to
another, you might not even be sure if you could release it yet. Or if
some other part of the program would take care of releasing it or might
even release before you were done with it. So you could also write what
was called, retain calls to that object. But you would still need to
match any retain call up with an additional release call.

Basically, before ARC, you had to envision every possible scenario-logic
that your application will go through to make sure that all of your
objects’ lifetime is managed correctly. Not that easy.

#### After ARC

Luckily, when using ARC you are no longer need to use
`release` `autorelease` `retain` calls. But it’s
important to understand the dangers of incorrectly writing this code.

One of the problems you could have is you might release too soon. You’d
create an object, have a pointer to that area of memory, you’d call the
methods, at some point you’d release it. But if you still had a valid
pointer, there’s nothing that would actually stop you writing another
line of code that tried to use it. This would be called a dangling
pointer. The pointer existed, but what it was pointing to was no longer
valid in memory and this could cause a crash.

The flip side of this is you might not release at all, you might create
an object. Start calling methods of that object and then just allow the
pointer to drop out of scope and disappear. But you never released the
object so you just started claiming more and more memory, what was
referred to as a **memory leak**.

So having to write a lot of this code was certainly very prone to errors
and issues. Now you might wonder if we’re using this new ARC feature why
do I even mention the existence of things like release and retain calls.
Because the idea of release and retain calls have not disappeared the
language still does reference counting.

The language hasn’t changed. The difference is you simply don’t need to
write the retain and release and autorelease calls because the compiler
does. ARC is taking the fact that compilers have gotten so good, that
any time you build your project, the compiler, in this case, llvm, which
is what Xcode is using behind the scenes, is able to determine all the
possible paths for your code. And it basically goes through your code
synthesizing the write, retain, release, and autorelease calls that you
would need.

What the compiler’s doing is effectively writing the same code you would
write yourself if you were really, really, really good at writing memory
management code.

ARC doesn’t physically change your source code files, but this is
effectively what the compiler is doing when you compile a project, and
you’re using ARC.

#### **Difference between Garbage Collector and ARC**

ARC is a very different effect than having a garbage collector.
Languages that use garbage collection are often what is referred to as
*non-deterministic*. It means that you can’t tell exactly when objects
are being reclaimed because it's being managed by the runtime by an
external process. ARC allows us to be completely deterministic. The code
controls when these objects are released. It’s just the code to release
them has been written by the compiler, not by you. In fact, not only do
you not write these calls when you’re using ARC, you can’t write these
calls. If you try and do even the simple release call you’re going to
get an error.

#### Conclusion

You need to be aware of the idea of retain or release. It is still
what’s going on under the hood, but, certainly if you haven’t had to do
it be thankful that you don’t have to do this anymore.

I’d love to hear more from you on that topic, and what do you think of
going back to a language like Objective-C in order to understand a topic
like memory management better? Have you ever done that before?

[![](https://cdn-images-1.medium.com/max/800/1*8RA2giRIK2fXze7e57361Q.png)](https://www.paypal.me/HassanElDesouky?locale.x=en_US)

By [Hassan El Desouky](https://medium.com/@hassaneldesouky) on [July 4,
2019](https://medium.com/p/3be777f69b7e).

[Canonical
link](https://medium.com/@hassaneldesouky/ios-memory-management-in-under-6-minutes-3be777f69b7e)
