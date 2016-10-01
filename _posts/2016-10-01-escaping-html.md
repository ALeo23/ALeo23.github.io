---
bg: "canyon.jpg"
layout: post
title:  "Escaping HMTL"
crawlertitle: "Can you escape the HTML?"
summary: "Escape but don't run!"
date:   2016-10-02
categories: posts
tags: ['Removing dangerous characters']
author: Alex Leo
---


## Converting Values

Malicious users can 'inject' HTML directly into your webpage via XSS(more about that below). When we escape HTML, we replace potentially dangerous characters with their escaped equivalents. A couple examples are highlighted at the end of the section. Escape HTML anywhere that there is a potential for any kind of user input.

For instance, somebody accessed your vulnerable website and entered something like `<script>setInterval(function() {alert("We're no strangers to memes")},0)</script>` into a search bar. This code would then be ran within your HMTL page, entering you into an infinite loop of alerts that allude to [Rick Astley](https://www.youtube.com/watch?v=dQw4w9WgXcQ) jokes. Super malicious. You can prevent this insane act of terror from perversing your webpage by correctly escaping the HTML.

{% highlight js %}
& //escapes to &amp;
< //escapes to &lt;
> //escapes to &gt;
" //escapes to &quot;
' //escapes to &#x27;
` //escapes to &#96;
/ //escapes to &#x2F;
!
@
$
%
(
)
=
+
{
}
[
]
{% endhighlight %}

One way to get these escaped values is the `_.escape` function included in the [underscore.js](http://underscorejs.org/#escape) library. The accompanying `_.unescape` function can be used to convert these strings to their unescaped values. [Regular expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) can also be used to reject or replace strings that (potentially) contain an XSS atack. Note that you are not able to escape all of these using this method. Some of the above symbols can used to escape out of an HTML attribute value that is not quoted and it would be best to escape them. It is also best practice to quote all HMTL attributes for security purposes.

[![escape]({{ site.images }}/keyboard.jpg)]({{ site.images }}/keyboard.jpg)

(You didn't seriously click on that Rick Astley link did you?)


## Unicode

Computers today are very powerful, capable machines, yet they're still complex calculators that operate on numbers. All letter and symbol data that is input into a computer needs to be converted into some sort of number value in order to be interpreted by a computer. This process is referred to as *encoding*; characters are encoded from letters into numbers. As with any other industry or project, a need for some sort of standardization quickly developed. [Unicode](http://unicode.org/standard/WhatIsUnicode.html) came in to save the day by providing a worldwide encoding standard. Unicode is more secure than the past systems, where programs would have to use multiple character encoding systems. This could lead to unexpected code being injected because all systems encode and transfer characters different. Their encoding standard is flexible and can be used across any language, spoken or programming, application, and platform. A healthy by-product of this flexibility is the worldwide availability of many software programs. Unicode eliminates a lot of the frustration involved with communicating with external networks and APIs.

######  UTF-8 / UTF-16 / UTF-32

UTF-8 is the most commonly used type of the Unicode standard. Within Javascript and on the web, this will be the primary type you'll work with. Other platforms such as Java, Windows, and Linux will use either UTF-16 or UTF-32 depending on their needs. UTF-16 and UTF-32 are two more currently implemented types of Unicode. These three versions are all fundamentally similar, but encode characters in different ways. UTF-8 provides up to four 8-bit bytes, UTF-16 holds up to two 16-bit code units and UTF-32 has one 32-bit code unit. No matter what version you are using, it is important to declare your charset using the appropriate HTML attribute within the meta tag. Characters can be transferred from one UTF type to another using algorithms found on the Unicode website. If you're interested, check out their [FAQ](http://unicode.org/faq/utf_bom.html).



## See Also

-[A Game About XSS](https://xss-game.appspot.com/)

-[hack.me An XSS Challenges Website](https://hack.me/t/XSS)

-[OWASP's Vast Security Wiki](https://www.owasp.org/index.php/Main_Page)

-[Templates in Underscore](http://underscorejs.org/#template)

