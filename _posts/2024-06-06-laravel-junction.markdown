---
layout: post
title:  "5 reasons to use Laravel Junction in your next Laravel project"
date:   2024-06-06 15:44:00 +0800
categories: package
---

In this article, I will share 5 reasons why you should consider using the Laravel Junction package in your next or existing Laravel project. Before we go further, let's get to know Laravel Junction. This is an open-source package that was first released in February 2024 by [WEAP](https://github.com/weapnl), one of the development teams I work closely with. I had the opportunity to use this package before it was released to the public as open-source in one of my Laravel projects. Laravel Junction allows us to create REST APIs with extended functionality. Let's dive deeper into why we need to `composer install` this!

![diagram-1-weap-junction-example](/assets/weap-junction-example.png)

1. Boost RESTful API development for CRUD along with action endpoints for custom actions.
```
// routes/api.php
Junction::apiResource('users', 'UserController');
```
With this single line definition in the route file, we already handle all of the REST API endpoints such as create, read, update, and delete (CRUD). These are the common endpoints that allow us to interact with the resource. Additionally, they have included a special endpoint called `action` to trigger any custom actions.

2. Introduce consistent endpoint signatures and simplify endpoint definitions in route files.

3. Extensive support for filters, modifiers, and relations.

4. Built-in support for pagination and validation.

5. Integration with JS Junction for seamless implementation with any JavaScript frontend codebase.

I hope this helps you and your team consider this tool or package, which can significantly boost the development process and allow you to focus more on delivering features that meet business needs.

Have a great day ahead!