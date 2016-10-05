---
bg: "time.jpg"
layout: post
title:  "Optimizing Images"
crawlertitle: "The smaller the better"
summary: "Increase performance; decrease load times"
date:   2016-10-04
categories: posts
tags: ['Rendering Images Faster']
author: Alex Leo
---

## Images as Data

Computer images exist everywhere on the internet. Without them, the world would be a pretty bleak wasteland of text. Pictures display a wide variety of content across the internet, ususally related to the context. Wiki pages use images related to their content, social media profiles have pictures of their users, and games utilize special pictures called [sprites](https://css-tricks.com/css-sprites/) to render characters more efficiently.

[![mountains]({{ site.images }}/mountains.jpg)]({{ site.images }}/mountains.jpg)
A picture is worth 1,000 words, or so they say.

###### Image File Size

As you probably already know, data is stored on a computer in bytes, more often respresented by their larger values: kilobytes, megabytes, and gigabytes. If a picture is worth 1,000 words, how many bytes does it take? Trick question. Picture size is dependent on many factors, but the words you use to describe them in your blog post don't affect the image size. Generally speaking, the more high quality an image is, the larger file size it will have. A main contributor to the quality is the image resolution.

## Compressing Images

Images can be resized and optimized to fit your needs in order to decrease load times. Most times, a small image like the one above does not need to be a 4K resolution ultra HD picture to convey the details you're trying to get across. The best practice is to only use the size that you need for your application.

If the photo is going to be re-sized by your application to be 200px x 200px then it would be a great performance increase to take that load off of your CSS and just do it to the picture itself. To put it simply, making a file smaller, will make it load faster. Today, users demand web apps that are fast and responsive, and simply won't use apps that feel old or dead. So, what's the easiest way to re-size these images?

## ImageOptim

Today, I discovered a new tool that I had to share: ImageOptim. ImageOptim is an application that comes with a slew of great [features](https://imageoptim.com/api) designed to streamline the performance of your deployment. One thing I really like about ImageOptim, is I don't lose image quality when re-sizing the image. My images look exactly the same in production, but load much faster. The comet image on my main blog page now loads ~35kb less than it was before; reducing the amount of data needed to be retrieved from the server before the image can be loaded on screen. ImageOptim will also remove unnecessary metadata, comments, and embedded thumbnails to shrink down on size.

###### Versions of ImageOptim

ImageOptim has a few different options available to access their services. Currently, I'm on the Mac App which installs quick, takes up little space, and is very easy to use with a drag and drop interface. ImageOptim will modify the original files that you drag and drop to re-size; I can recommend backing up any images you plan to manipulate. Drag and drop your files in the GUI to re-size and wait for the program to do its magic. I noticed that this did take some time to process the files provided, so performing the work yourself on your local machine before you publish sounds like the most stable option.

ImageOptim also offers a couple of web services for users who do not wish to modify their local files. Their API is currently in beta and you can sign up to use it on their website. Listed in their documentation, you can also find out how to optimize on the fly. No back-end programming is needed to get this started; you'll just edit your image URLs to point to the ImageOptim server and they'll optimize them before sending to the client. Keep in mind that while this optimizes your images, this also involves another GET request and an outside service, which may actually detract from performance.

## Take Aways

Images are pictures on the internet that are used to display various forms of data. Images are made up of pixels, and the amount of pixels that make up an image is determined by its resolution. A higher resolution means a more detailed image and should only be used when needed. ImageOptim is a powerful and fast tool designed for re-sizing images based on user needs. Re-sizing an image manually, rather than having our code do it for us, causes our code to execute faster due to less required operations. The webpage will also load faster as there is less data being transferred over the wire.

## See Also

-[ImageOptim Mac app](https://imageoptim.com/mac)

-[Shay Howe's Advanced CSS: Performance Organization](http://learn.shayhowe.com/advanced-html-css/performance-organization/)

-[Free High Quality Images For Your Application](https://unsplash.com/)

-[A Guide to Pixels, Resolutions, and DPI](http://www.creativebloq.com/graphic-design/what-is-dpi-image-resolution-71515673)






