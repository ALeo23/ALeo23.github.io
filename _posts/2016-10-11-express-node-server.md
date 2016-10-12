---
bg: "aurora.jpg"
layout: post
title:  "Express Development"
crawlertitle: "Express"
summary: "Setting up a simple server with Express"
date:   2016-10-11
categories: posts
tags: ['Using node.js']
author: Alex Leo
---

## Getting Started With Express

Express is a web framework designed to abstract away a lot of the repeated code inside of node.js applications. You can find their documentation [here](https://expressjs.com/en/4x/api.html) and I highly recommend referencing it often while learning to use Express. Express has many built in functions for handling requests and serving responses. Express cleaned up their framework in the 4.x API and did a massive overhaul on the system. Express is now extremely modular and only comes with what a user will need to handle requests as mentioned above. Express comes pretty bare; `express.static` is the only middleware that comes baked in with Express since the 4.x update, so be aware as you read examples online. Any examples referencing 3.x or earlier may contain outdated information.

###### A Note About Middleware

Middleware functions, in the world of Express, are simply plugins that extend Express's functionality. A middleware function has a particular set of parameters it must take to work correctly; req, res, and next are required in middleware functions. Req is the request, res is the response, and next is a callback. The next function will signify the end of the function and allow the next functions to run. A function must either call `next()` or end the request response cycle, or the server will hang. Middleware is loaded using `app.use()`. Express also provides a great guide for writing your own middleware, [it's not as hard as it sounds.](https://expressjs.com/en/guide/writing-middleware.html)

## Using Express

Using Express is both intuitive and rewarding. I've typed up a quick example of a server with some key parts needed to get started handling some GET and POST requests.

[![express1]({{ site.images }}/express1.png)]({{ site.images }}/express1.png)
*On the "Code Less Express!"*


Looking above, we can see that a lot of the request handling is being abstracted away for us. The only external functions that are not listed are the express module itself. Express can chain middleware functions using next to move along until an end or return is reached.

[![express1]({{ site.images }}/express2.png)]({{ site.images }}/express2.png)
*Postman allows you to debug POST requests without having to create forms and event handlers. (See below)*

Generally, you'll want your POST requests to have some sort of inner function that stores data somewhere in the storage method of your choice. These handlers can also take multiple callbacks and chain them together for more complex operations. The additional callbacks passed in will all call `next()` when done running, and the final callback, not usually a named function, in the chain will end the response.

## Going Further

Express is a web framework built on top of node. Like many modules that exist for node, Express extends node's functionality to make working with node less exhausting. Express now comes pretty bare, and only has what you need it to, after you import other middlewares and create your own. Postman is a great app designed to streamline API development and is very quick to pick up and use. Note that when using Express, we don't need to require or use the 'http' module because Express is taking care of the heavy lifting.


## See Also

-[Express](https://expressjs.com/)

-[Authentication with Express](http://www.9bitstudios.com/2013/09/express-js-authentication/)

-[Postman](https://www.getpostman.com/)



