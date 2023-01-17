---
layout: default
title: Services
parent: Angular
resource: true
desc: "Angular Services interview questions and answers."
categories: [Angular Services]
---

# Angular Services
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


# Angular Services

Angular services are singleton objects which get instantiated only once during the lifetime of an application. It contains method that maintain data throughout the life of an application, i.e. data does not get refreshed and is available all the time. The main objective of a service is to organize and share business logic, models, or data and functions with different components of an Angular application.

**Benefits**

An Angular service is a stateless object and provides some very useful functions. These functions can be invoked from any component of Angular, like Controllers, Directives, etc. This helps in dividing the web application into small, different logical units which can be reused.

```typescript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';

@Injectable({ // The Injectable decorator is required for dependency injection to work
    // providedIn option registers the service with a specific NgModule
    providedIn: 'root',  // This declares the service with the root app (AppModule)
})
export class RepoService {
    constructor(private http: Http) { }

    fetchAll() {
       return this.http.get('https://api.github.com/repositories');
    }
}
```

The above service uses Http service as a dependency.

### Angular Service vs Interceptor

* In Angular, a **service** is a `class` that is used to **encapsulate business logic, share data, and handle cross-component communication**. `Services` are typically used to handle tasks that are not directly related to the view, such as interacting with a backend API, handling browser storage, or logging events. `Services` are typically stateless and are injected into components or other services using Angular's dependency injection system.

* An **interceptor**, on the other hand, is a `class` that is used to **intercept and modify HTTP requests and responses**. `Interceptors` are typically used to add headers, handle authentication, or handle errors. An `interceptor` is typically used to modify the request before it is sent and also handle the response after it is received.

* In summary, `services` are a way to encapsulate and share business logic, data and cross-component communication, whereas `interceptors` are used to intercept and modify HTTP requests and responses, and are typically used to add headers, handle authentication, or handle errors. Both `services` and `interceptors` are used in Angular to separate concerns and make the code more maintainable.

















For more information:

[Introduction to services and dependency injection](https://angular.io/guide/architecture-services)