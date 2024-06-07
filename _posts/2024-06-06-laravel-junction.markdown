---
layout: post
title:  "5 reasons to use Laravel Junction in your next Laravel project"
date:   2024-06-06 15:44:00 +0800
categories: package
---

In this article, I will share 5 reasons why you should consider using this package in your next or existing Laravel project. Before we go further, let's get to know that. [Laravel Junction](https://github.com/weapnl/laravel-junction) is an open-source package that was first released in February 2024 by [WEAP](https://github.com/weapnl), one of the development teams I work closely with. I had the opportunity to use this package before it was released to the public as open-source in one of our Laravel projects. Laravel Junction allows us to create REST APIs with extended functionality.

![diagram-1-weap-junction-example](/assets/weap-junction-example.png)

Now, let's dive deeper into why we need to `composer install` this package and start using it!

### 1. Boost RESTful API development for CRUD along with action endpoints for custom actions
```
// routes/api.php
Junction::apiResource('users', 'UserController');
```
With this single line definition of `apiResource` in the route file, we already handle all of the REST API endpoints such as create, read, update, and delete (CRUD). These are the common endpoints that allow us to interact with the resource. Additionally, they have also included a special endpoint called `action` to trigger any custom actions.

```
// UserController.php
public function actionSendNotification(): void
{
    // send notification
}
```

To trigger the action method, you can submit a PUT request with this payload:
- URL: http://localhost/user
- Method: PUT
- Payload: `{ action: "sendNotification" }`

By passing the `sendNotification` value to the `action` in the request payload, we can trigger the custom action that we have defined in the controller.

### 2. Introduce consistent endpoint signatures and simplify endpoint definitions in route files
With a single line, `Junction::apiResource('users', 'UserController');`, declared in the route file, we can always ensure that the signatures of the endpoints are consistent. This will also make our route file cleaner and prevent it from being cluttered with inconsistent endpoint names.

### 3. Extensive support for filters, modifiers, and relations
The support for these features helps us cater to complex use cases that require more than CRUD functions. For example, consider a datatable where we want to filter with a limited number of results and order by the ascending name column. To do this, we can call the request as follows:
```
http://localhost/user?limit=10&orders[][column]=name,orders[][direction]=asc
```
There are more keys supported for filters and modifiers, which you can refer to in the [README](https://github.com/weapnl/laravel-junction?tab=readme-ov-file#filters) in the package repository.

### 4. Built-in support for pagination and validation
The package provides pagination mechanisms along with simple pagination, which will not return the total amount if you need to handle large database tables.

### 5. Integration with [JS Junction](https://github.com/weapnl/js-junction) 
This allows us to easily consume APIs built with Laravel Junction for seamless implementation with any JavaScript frontend codebase.

I hope this helps you and your team consider this tool or package, which can significantly boost the development process and allow you to focus more on delivering features that meet business needs.

Have a great day ahead!