---
bg: "hax.jpg"
layout: post
title:  "Application Security"
crawlertitle: "XSS Tricky"
summary: "Keep the dataz safe"
date:   2016-10-01
categories: posts
tags: ['Cross Site Scripting']
author: Alex Leo
---

## Information Is Important

Computer hackers have been around for a long time now and their business only becomes more lucrative. With the internet and telecommunications continuing to exponenetially grow, the demand for personal information only gets higher. This means that your security needs to be top-notch at all times in order to keep your users, their data, and yourself safe from malicious attacks. There are many oppurtunities for vulnerability while browsing the internet and it is very important to be aware of all of the various ways that you can keep your data safe.

## XSS

XSS is an acronym for cross-site scripting, which is a style of attack where a malicious user injects code into your program unwillingly. This can lead to a myriad of bad events ranging from changing your page layout to stealing all of your client's sensitive user data. Protecting against XSS is important if you want your users to be able to trust that your website is safe. Many different attack vectors, some larger than others, exist that all have different vulnerabilities that need to be protected against. The primary ways to defend against XSS are far too long and involved to cover in one blog post. I highly encourage you to check out the XSS Prevention Cheat Sheet that OWASP has put together [here.](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)

[![security]({{ site.images }}/lock.jpg)]({{ site.images }}/lock.jpg)

###### OWASP

The Open Web Application Security Project is designed to be a worldwide organization that specializes in application security. OWASP's main goal is to allow worldwide distribution of software that can be trusted. They provide information about internet security such as common attack vectors for information, vulnerabilities, and proactive actions you can take. OWASP has a variety of cheat sheets and documentation around ways to protect yourself and design your applications to protect your users.

## Same Origin Policy

Scripts are normally only to be run on the site that originated them. Sounds secure right? This rule is designed to keep users/clients safe from malicious websites. An origin consists of a domain, a sub-domain, protocol, and port; all of these must match to run a script according to the same origin policy. This rule does not protect a server or application from the client. Furthermore, this would even mean that if you wanted to make some changes on your website on a localhost port, any calls to a third party service would fail. This is all part of the browser and is implemented by the developer of the browser. Chrome, for example, allows this service to be disabled by starting the application with the --disable-web-security flag.

###### CORS

Cross Origin Resource Sharing, CORS for short, is accessed when a client makes a request to a server other than its origin. This allows websites across different domains to share data with one another. As you can imagine, this benefit is also a risk, as the data passed between websites can be sensitive. The owner of the server being accessed gets to determine the access rights for CORS on that server.

When a GET request is sent to the server, it will contain a CORS header. The server will then check to see if that client's CORS header matches its Access-Control-Allow-Origin list. If the client has a valid header, the server will fulfill the requests, otherwise the server will send back an unauthorized error. Many servers disable CORS for security purposes, or use some sort of authentication before sending out data.  Authentication is usually verified in the form of user accounts, API keys, and cookies.

A flowchart can be found [here](http://www.html5rocks.com/static/images/cors_server_flowchart.png) that shows the different steps the server will go through when receiving a GET or POST request from an off site client.

###### JSONP

JSONP is Javascript Object Notation with Padding. JSONP can be used to bypass CORS and make cross-domain requests for data. What does it mean when we say "padding" on a JSON object? On the server side, the JSON object just gets wrapped in a callback function before being sent off. If you put the URL inside of a script tag, the browser is going to execute the script tag and download the linked script file, and execute the file once it's been loaded. Script tags are able to pull files from the internet across domains, much like loading jQuery from a CDN. JSONP can be dangerous because the code that is being executed came from another domain. This should only be used with trusted sources.








