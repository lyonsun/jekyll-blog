---
layout: post
title: "Some unexpected issues I encountered while learning build Magento extensions"
date: 2014-10-17 23:01:38 +0800
comments: true
categories: [magento, php]
---

Learning something new is always nice and with a lot of fun. But there also always will be something not clearly stated in books or other materials, which is not fun and sometimes wastes me plenty of time to figure it out, or worsier, drives me crazy. 

Here are some unexpected issues I've faced while reading a book and starting this exciting Magento extension development adventure.

## Issue 1: Cannot login to admin area after successful installation

Well, this is pretty odd. I installed Magento on my Mac Pro under MAMP environment. Everything went perfectly, except one: 

### I can't login to admin area. 

1. There is no error, nothing. Well, there is something: web page actually get refreshed, and url also get updated to something like: [http://localhost:8888/magento/index.php/admin/dashboard/index/key/099e02f9fc33d69ca3fee8f0f5b2b7f6/](http://localhost:8888/magento/index.php/admin/dashboard/index/key/099e02f9fc33d69ca3fee8f0f5b2b7f6/). This url is not always the same, especially the serial at the last. 
2. This issue happens on Google Chrome/Opera/Safari, but not Firefox.
3. If I close this page, and then reopen it and navigate with admin url, I get presented with admin area page. 
4. Safari and Opera will start to work well if I just logout and login again. But Chrome failed to do so. It keeps giving the login page with url similar to the one emphasized above. 

Someone asked this question on SO, but he/she had some other more critial issue on Firefox. However, no absolutely correct answer has been given for this question. 

According to the url that get updated, it apparently says I have been redirected to dashboard page, but due to some reason, Chrome just isn't able to load the view. 

At the time of writing, I still have no idea what went wrong. 

## Issue 2: Not get "Hello World #1." message in sample HappyHour extension

This is odd too... I carefully followed the tutorial on book *Getting Started with Magento Extension Development*. It was quite simple an extension. Actually code is only one line in an action method inside a class: 

    <?php 

    class Foggyline_HappyHour_HelloController extends Mage_Core_Controller_Front_Action
    {
        public function helloWorldAction()
        {
            echo "Hello World #1.";
        }
    }
    
Nothing funcy. But when I navigate to [http://localhost:8888/magento/happyhour/hello/helloWorld](http://localhost:8888/magento/happyhour/hello/helloWorld) as I've been told to, I get 404 response. 

Then when I go to admin area, and navigate to **System > Configuration > Advanced > Advanced**, and save configuration, I see magic **Hello World** message after a refresh on frontend. 

And I also have no idea why things work this way, not that being told on the book.