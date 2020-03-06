---
layout: page
title: About Hassan ElDesouky
categories: []
tags: []
status: publish
type: page
published: true
meta: {}
---

<h1 style="text-align: center; margin-bottom: 40px; margin-top: -50px">Hassan ElDesouky</h1>

<div id="leftCol">
  <img src="/assets/Avatar.jpg" width="290" style="margin-bottom: 10px" />
  <br />
  <p style="text-align: center;"><small style="">Hassan ElDesouky</small></p>
</div>

<div id="rightCol">
  <p>I’m a joiner Computer Science student in a university in Egypt. I knew some concepts about programming in high school but I started doing programming and taking it seriously in college. I’m passionate about Apple technologies such as iOS development and I’m also passionate about sharing my knowledge to help people starting out. I also like to draw and play the guitar.</p>
  
	<p>I started doing competitive programming for almost a year now and participated in several programming competitions like <a href="https://icpc.baylor.edu/regionals/finder/ECPC-2019">ECPC</a>, Google’s Code Jam and Hash Code, and Facebook HackerCup.</p>

	<p>I also started learning iOS development for over a year now, and have been fascinated by how Apple build beautiful and powerful apps and at the same time with really great UI design and an outstanding user experience.</p>

	<p>After I learned some basics of iOS development I started a personal blog on Medium to share what I’ve been doing or learning in the past days. An example of that is that… I use Apple's Voice Memos application a lot and since I started learning iOS development I have always wanted to create an audio recorder with audio visualization but I wasn’t able to find any tutorials on how to build such thing, so I started doing it myself and after I reached an acceptable result I wrote an article about the whole process on Medium.</p>

  <p>Follow what I'm up to on <a href="https://twitter.com/hassanedesouky">Twitter</a> and <a href="https://instagram.com/hassanedesouky">Instagram</a>.</p>
</div>


<div style="width: 100%; float: left; margin-top: 20px; margin-bottom: 20px;">
  <form id="contactform" method="POST" action="https://formspree.io/xgeylegw">
    <p><b>Email Address</b></p>
    <input type="email" name="_replyto" placeholder="Your email address">

    <p><b>Message</b></p>
    <textarea placeholder="Your message" name="message"></textarea>
    <input type="hidden" name="_subject" value="New message from heldesouky.xyz" />
    <br />
    <input type="submit" value="Submit">
  </form>
</div>

<hr />

<style type="text/css">
  .imageCarousel {
    margin-top: 30px;
    height: 310px;
    width: 100%;
    overflow-y: none;
    overflow-x: scroll;
    white-space: nowrap;
  }

  .imageCarousel > a > img {
    height: 300px;
    width: auto;
    max-width: none; /* to override page wide attribute */
    display: inline-block;
  }
  #personalCarousel > a > span {
    /* I didn't spend the time investigating why this is necessary */
    margin-right: 5px;
    height: 300px;
    display: inline-block;
    width: 300px; /* IG pictures should always be square */
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50% 50%;
  }
  #contactform {
    padding-top: 30px;
  }

  #contactform input[type="email"] {
    width: calc(100% - 20px);
    height: 30px;
    font-size: 16px;
    padding: 10px;
    margin-bottom: 10px;
  }
  #contactform textarea {
    width: calc(100% - 30px);
    height: 100px;
    font-size: 16px;
    border: 1px solid #ccc;
    background-color: #fafafa;
    padding: 15px;
    resize: vertical;
  }
  #contactform input[type="submit"] {
    display: inline-block;
    width: 127px;
    height: 42px;
    background-color: #272727;
    color: white;
    font-weight: 600;
    font-style: normal;
    font-size: 14px;
    border: none;
    margin-top: 10px;
    cursor: pointer;
  }
  #leftCol {
    margin-bottom: 40px;
    margin-right: 30px;
    width: 100%;
    text-align: center;
  }
  @media screen and (max-width: 800px) {
    .imageCarousel {
      height: 190px;
    }
    .imageCarousel > a > img {
      height: 180px;
    }
    #personalCarousel > a > span {
      height: 180px;
      width: 180px;
    }
  }
  @media screen and (min-width: 800px) {
    #leftCol {
        width: 40%;
        float: left;
        height: 820px;
      }
    }
  }
  @media screen and (min-width: 800px) {
    #rightCol {
      width: 55%;
      float: right;
    }
  }
  }
</style>
