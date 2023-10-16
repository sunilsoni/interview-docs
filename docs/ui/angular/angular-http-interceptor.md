---
layout: default
title: Angular http Interceptor
parent: Angular
resource: true
grand_parent: UI Design
permalink: /docs/ui/angular/interceptor/
desc: "Angular http Interceptor interview questions and answers."
categories: [Angular http Interceptor]
---

# Angular http Interceptor
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---
## What is Angular Http Interceptor?

* An Angular HTTP interceptor is a powerful feature that allows you to intercept and modify HTTP requests and responses. It is a way to centralize the handling of certain aspects of an HTTP request, such as adding headers, handling errors, or modifying the request and response.

* An HTTP interceptor is a service that implements the HttpInterceptor interface, which defines a single method intercept(req: HttpRequest<any>, next: HttpHandler) : Observable<HttpEvent<any>>. This method is called for each HTTP request, and it receives the current request and a next object, which is used to execute the next interceptor or the final request.

Here is an **example** of how to **create** an HTTP interceptor that adds a custom header to all requests:

```log
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable()
export class AuthInterceptor implements HttpInterceptor {

intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
// Clone the request and add the new header
const authReq = req.clone({ headers: req.headers.set('Authorization', 'Bearer YOUR_TOKEN') });

    // Pass the cloned request to the next handle
    return next.handle(authReq);
}
}
```

You then need to register the interceptor in your **app.module.ts** file by adding it to the providers array and the `HTTP_INTERCEPTORS` multi-provider.

```log
import { AuthInterceptor } from './auth.interceptor';

@NgModule({
...
providers: [
{ provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi: true }
],
...
})
```

* HTTP interceptors can be used for a variety of tasks, such as adding headers, handling errors, logging, caching, or modifying the request and response.

* It's worth mentioning that you can also create multiple interceptors, each one with a specific task, and chain them together to handle multiple aspects of an HTTP request.

In summary, an Angular HTTP interceptor is a powerful feature that allows you to intercept and modify HTTP requests and responses, it allows you to centralize the handling of certain aspects of an HTTP request and enables you to handle multiple aspects of an HTTP request by chaining multiple interceptors.

### How to Add interceptor to providers?

In Angular, you can add interceptors to your application's providers by first importing the HTTP_INTERCEPTORS token and the interceptor class. Then, in your application's module, you can add the interceptor class to the providers array, along with the HTTP_INTERCEPTORS token.

Here is an example:

1. Import the necessary modules in your interceptor file:

```log
 import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
```

2. Create the interceptor class and implement the HttpInterceptor interface:

```log
@Injectable()
export class MyInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    // Add your interceptor logic here
  }
}
```

3. In your **app.module.ts**, import the HTTP_INTERCEPTORS token and the interceptor class:

```log
import { HTTP_INTERCEPTORS } from '@angular/common/http';
import { MyInterceptor } from './interceptors/my-interceptor';
```

4. Add the interceptor class to the providers array, along with the HTTP_INTERCEPTORS token:

```log
@NgModule({
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: MyInterceptor,
      multi: true
    }
  ]
})
export class AppModule { }

```

**Note:** The multi: true is added so that multiple interceptors can be added.

### Any interceptor we want to create needs to implement the HttpInterceptor interface.

* This means that our new class should have a method called intercept with parameters HttpRequest and HttpHandler. The use of interceptors transforms outgoing requests and incoming responses, but we cannot tamper with the original request - it has to be immutable. To make changes, we need to clone the original request.

* As we clone the original request, we can set any header we want. In our case, it's very simple - we want to add an Authorization header with an auth scheme of Bearer after the JSON Web Token in local storage, which we get from the AuthService by calling the getToken method.

---















