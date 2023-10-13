---
title: AngularOld
has_children: true
nav_order: 2
permalink: docs/angular
resource: true
desc: "Angular interview questions and answers."
categories: [Angular]
---

# Angular
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


---

## Steps you follow to increase application performance in angular.

- Use lazy loading: Lazy loading helps to reduce the size of the initial bundle and increases the performance of your application by loading only the necessary components and modules on demand.

- Use production mode: Running your application in production mode helps to improve performance by disabling development checks and setting various environment variables to production-ready values.

- Use AOT (Ahead-of-Time) Compilation: AOT compilation compiles the Angular components and templates at build time instead of runtime, reducing the startup time of your application.

- Use Change Detection Strategy: Change detection is the process of checking for changes in the Angular components. By using OnPush change detection strategy, you can limit the number of change detection checks and improve the performance of your application.

- Use modern JavaScript features: Use modern JavaScript features such as async/await, destructuring, and spread operators to write cleaner, more performant code.

- Use optimization tools: Use optimization tools such as ngcc, Angular CLI's production builds, and Ahead-of-Time (AOT) compilation to reduce the size of the bundle, improve the startup time, and improve overall performance.

- Minimize the number of DOM manipulations: Minimizing the number of DOM manipulations will help reduce the time it takes for the browser to render the changes and improve the performance of your application.

- Use caching: Use caching techniques such as in-memory caching and HTTP caching to reduce the amount of data that needs to be transferred over the network and improve the performance of your application.

- Use server-side rendering: Server-side rendering allows the browser to display the initial view of your application faster, improving the time-to-first-paint and overall user experience.

- Use Angular animations wisely: Angular animations can add visual appeal to your application, but can also have a negative impact on performance if not used wisely. Minimize the number of animations and optimize them for performance by using transform and opacity instead of width and height, for example.

- Monitor performance regularly: Regularly monitor your application's performance using tools such as the Chrome DevTools performance panel and the Angular Augury tool to identify and resolve performance bottlenecks.

- Follow best practices for Angular development: Adhering to best practices for Angular development, such as using observables instead of promises, keeping components simple, and avoiding excessive use of nested components, can help improve the overall performance of your application.

- Use efficient data structures: Using efficient data structures, such as HashMaps, Tries, and Binary Search Trees, can help improve the performance of your application by reducing the time it takes to search and manipulate data.

- Minimize the number of HTTP requests: Minimizing the number of HTTP requests can improve the performance of your application by reducing the amount of data that needs to be transferred over the network. Consider using batch requests or caching to minimize the number of HTTP requests.

- Use efficient algorithms: Use efficient algorithms to solve problems in your application, such as using binary search instead of linear search, or using a breadth-first search instead of a depth-first search.

- Use memoization: Memoization is a technique that caches the results of function calls so that they can be reused in the future, reducing the number of redundant computations and improving performance.

- Use a content delivery network (CDN): Using a CDN can help improve the performance of your application by caching static assets, such as images and scripts, on multiple servers around the world, reducing the latency for users accessing your application from different locations.

- Use efficient data binding: Efficient data binding can help improve the performance of your application by reducing the number of bindings and avoiding unnecessary updates to the DOM. Consider using one-way data binding or using a Pure pipe to reduce the number of bindings.

- Minimize the use of third-party libraries: While third-party libraries can provide additional functionality, they can also have a negative impact on performance if they are not optimized or used excessively. Minimize the use of third-party libraries and consider alternative solutions, such as writing your own code, to improve performance.

- Regularly update Angular: Regularly updating Angular can help improve performance by taking advantage of the latest features and optimizations, as well as fixing any known performance issues. Stay up-to-date with the latest version of Angular and its related libraries to ensure optimal performance.


---

## Single-page application(SPA) vs. multiple-page application(MPA)


### Single-Page Application

A single-page application is an app that works inside a browser and does not require page reloading during use. You are using this type of applications every day. These are, for instance: Gmail, Google Maps, Facebook or GitHub.

####  Pros of the Single-Page Application

- SPA is fast, as most resources (HTML+CSS+Scripts) are only loaded once throughout the lifespan of application. Only data is transmitted back and forth.
- The development is simplified and streamlined. There is no need to write code to render pages on the server. It is much easier to get started because you can usually kick off development from a file file://URI, without using any server at all.
- SPAs are easy to debug with Chrome, as you can monitor network operations, investigate page elements and data associated with it.
- It’s easier to make a mobile application because the developer can reuse the same backend code for web application and native mobile application.
- SPA can cache any local storage effectively. An application sends only one request, store all data, then it can use this data and works even offline.

####   Cons of the Single-Page Application

- It is very tricky and not an easy task to make SEO optimization of a Single-Page Application. Its content is loaded by AJAX (Asynchronous JavaScript and XML) — a method of exchanging data and updating in the application without refreshing the page.
- It is slow to download because heavy client frameworks are required to be loaded to the client.
- It requires JavaScript to be present and enabled. If any user disables JavaScript in his or her browser, it won’t be possible to present application and its actions in a correct way.
- Compared to the “traditional” application, SPA is less secure. Due to Cross-Site Scripting (XSS), it enables attackers to inject client-side scripts into web application by other users.
- Memory leak in JavaScript can even cause powerful system to slow down

### Multiple-Page application(MPA)


Multiple-page applications work in a `traditional` way. Every change eg. display the data or submit data back to server requests rendering a new page from the server in the browser. These applications are large, bigger than SPAs because they need to be. Due to the amount of content, these applications have many levels of UI. 

Luckily, it’s not a problem anymore. Thanks to AJAX, 
we don’t have to worry that big and complex applications have to transfer a lot of data between server and browser. That solution improves and it allows to refresh only particular parts of the application. On the other hand, it adds more complexity and it is more difficult to develop than a single-page application.


#### Pros of the Multiple-Page Application

- It’s the perfect approach for users who need a visual map of where to go in the application. Solid, few level menu navigation is an essential part of traditional Multi-Page Application.
- Very good and easy for proper SEO management. It gives better chances to rank for different keywords since an application can be optimized for one keyword per page.

#### Cons of the multiple-page application

- There is no option to use the same backend with mobile applications.
- Frontend and backend development are tightly coupled.
- The development becomes quite complex. The developer needs to use frameworks for either client and server side. This results in the longer time of application development.


---

## AngularJS vs Angular

Angular is a completely revived component-based framework in which an application is a tree of individual
components.


| AngularJS                                         | Angular                                             |
|---------------------------------------------------|-----------------------------------------------------|
|JavaScript-based framework for creating SPA.       |Complete re-write of AngularJS version.       |
|Still supported but no longer will be developed.   |It is updated version regularly released because of Semantic Versioning.|
|The architecture of AngularJS is based on MVC.     |The architecture of Angular 2 is component based|
|AngularJS was not developed with a mobile base in mind.|Angular 2 is a mobile-oriented framework.|
|AngularJS code can write by using only ES5, ES6, and Dart.|We can use ES5, ES6, Typescript to write an Angular 2 code.|
|Factory, service, provider, value and constant are used for services|The class is the only method to define services in Angular2|
|Run on only client-side                             |Runs on client-side & server-side|
|ng-app and angular bootstrap function are used to initialize | bootstrapmodule() function is used to initialize|

### AngularJS

#### Advantages

* It has great MVC data binding that makes app development fast.
* Using HTML as a declarative language makes it very intuitive.
* It is a comprehensive solution for rapid front-end development since it does not need any other frameworks or plugins.
* AngularJS apps can run on every significant program and advanced cells including iOS and Android-based phones and tablets.
* Two-way data binding
* Directives
* Dependency injection

#### Disadvantages

* It is big and complicated due to the multiple ways of doing the same thing.
* Implementations scale poorly.
* If a user of an AngularJS application disables JavaScript, nothing but the basic page is visible.
* There is a lagging UI if there are more than 200 watchers.


### Angular


#### Advantages

* Component-based architecture that provides a higher quality of code
* Reusability: Components of similar nature are well encapsulated, in other words, self-sufficient. Developers can reuse them across different parts of an application.
* Unit-test friendly: The independent nature of components simplifies unit tests, quality assurance procedures aimed at verifying the performance of the smallest parts of the application, units.
* Maintainability: Components that are easily decoupled from each other can be easily replaced with better implementations.


#### Disadvantages

* Angular is verbose and complex
* Steep learning curve
* Migrating legacy systems from AngularJS to Angular requires time

### Why Angular

Angular is a development platform, built on TypeScript. As a platform, Angular includes:

* A component-based framework for building scalable web applications
* A collection of well-integrated libraries that cover a wide variety of features, including routing, forms management,
  client-server communication, and more
* A suite of developer tools to help you develop, build, test, and update your code

With Angular, you're taking advantage of a platform that can scale from single-developer projects to enterprise-level
applications. Angular is designed to make updating as easy as possible, so you can take advantage of the latest
developments with a minimum of effort.


---

## Components

Components are a logical piece of code for Angular application. A Component consists −

- **Template** This is used to render the view for the application. This contains the HTML that needs to be rendered in
  the application. This part also includes the binding and directives.
- **Class** This is like a class defined in any language such as C. This contains properties and methods. This has the
  code which is used to support the view. It is defined in TypeScript.
- **Metadata** This has the extra data defined for the Angular class. It is defined with a decorator.

Components are the building blocks that compose an application. A component includes a TypeScript class with a
@Component() decorator, an HTML template, and styles. The [@Component()](https://angular.io/api/core/Component)
decorator specifies the Angular-specific information:

- A CSS selector that defines how the component is used in a template. HTML elements in your template that match this
  selector become instances of the component.
- An HTML template that instructs Angular how to render the component.
- An optional set of CSS styles that define the appearance of the template's HTML elements.

The following is a minimal Angular component.

```typescript
import {Component} from '@angular/core';

@Component({
  selector: 'hello-world',
  template: `
<h2>Hello World</h2>
<p>This is my first component!</p>
`,
})
export class HelloWorldComponent {
// The code in this class drives the component's behavior.
}
```

To use this component, you write the  in a template:

```typescript
<hello-world > </hello-world>
```

When Angular renders this component, the resulting DOM looks like this:


```typescript
<hello-world >
<h2>Hello
World < /h2>
< p > This
is
my
first
component! < /p>
< /hello-world>
```

Angular's component model offers strong encapsulation and an intuitive application structure. Components also make your
application easier to unit test and can improve the overall readability of your code.



---

## Templates

Every component has an HTML template that declares how that component renders. You define this template either inline or
by file path.

Angular extends HTML with additional syntax that lets you insert dynamic values from your component. Angular
automatically updates the rendered DOM when your component’s state changes. One application of this feature is inserting
dynamic text, as shown in the following example.

```typescript
<p>{
{
  message
}
}
</p>
```

The value for message comes from the component class:

```typescript
import {Component} from '@angular/core';

@Component({
  selector: 'hello-world-interpolation',
  templateUrl: './hello-world-interpolation.component.html'
})
export class HelloWorldInterpolationComponent {
  message = 'Hello, World!';
}
```

When the application loads the component and its template, the user sees:

```typescript
<p>Hello, World! < /p>
```

Notice the use of double curly braces--they instruct Angular to interpolate the contents within them.

Angular also supports property bindings, to help you set values for properties and attributes of HTML elements and pass
values to your application's presentation logic.

```typescript
<p [id] = "sayHelloId" [style.color] = "fontColor" > You
can
set
my
color in the
component! < /p>
```

Notice the use of the square brackets--that syntax indicates that you're binding the property or attribute to a value in
the component class.

You can also declare event listeners to listen for and respond to user actions such as keystrokes, mouse movements,
clicks, and touches. You declare an event listener by specifying the event name in parentheses:

```typescript
<button (click) = "sayMessage()" [disabled] = "canClick" > Trigger
alert
message < /button>
```

The preceding example calls a method, which is defined in the component class:

```typescript
sayMessage()
{
  alert(this.message);
}
```

hello-world-bindings.component.ts

```typescript
import {Component} from '@angular/core';

@Component({
  selector: 'hello-world-bindings',
  templateUrl: './hello-world-bindings.component.html'
})
export class HelloWorldBindingsComponent {
  fontColor = 'blue';
  sayHelloId = 1;
  canClick = false;
  message = 'Hello, World';

  sayMessage() {
    alert(this.message);
  }
}
```

hello-world-bindings.component.html

```html

<button (click)="sayMessage()" [disabled]="canClick">Trigger alert message</button>
<p [id]="sayHelloId" [style.color]="fontColor">You can set my color in the component!</p>

```

You can add additional functionality to your templates through the use of directives. The most popular directives in
Angular are <B>*ngIf</B> and <B>*ngFor</B>. You can use directives to perform a variety of tasks, such as dynamically
modifying the DOM structure. And you can also create your own custom directives to create great user experiences.

The code is an example of the *ngIf directive.

hello-world-ngif.component.ts

```typescript

import {Component} from '@angular/core';

@Component({
  selector: 'hello-world-ngif',
  templateUrl: './hello-world-ngif.component.html'
})
export class HelloWorldNgIfComponent {
  message = 'I\'m read only!';
  canEdit = false;

  onEditClick() {
    this.canEdit = !this.canEdit;
    if (this.canEdit) {
      this.message = 'You can edit me!';
    } else {
      this.message = 'I\'m read only!';
    }
  }
}

```

hello-world-ngif.component.html

```html

<h2>Hello World: ngIf!</h2>
<button (click)="onEditClick()">Make text editable!</button>
<div *ngIf="canEdit; else noEdit">
  <p>You can edit the following paragraph.</p>
</div>
<ng-template #noEdit>
  <p>The following paragraph is read only. Try clicking the button!</p>
</ng-template>
<p [contentEditable]="canEdit">{{ message }}</p>

```

Angular's declarative templates allow you to cleanly separate your application's logic from its
presentation.  [Templates](https://angular.io/guide/template-syntax) are based on standard HTML, so they're easy to
build, maintain, and update.



---

## Dependency injection


Dependency Injection (DI) allows a class receive dependencies from another class. Most of the time in Angular, dependency injection is done by injecting a service class into a component or module class.

```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class PopcornService {

  constructor() {
    console.log("Popcorn has been injected!");
  }

  cookPopcorn(qty) {
    console.log(qty, "bags of popcorn cooked!");
  }
}
```
*AppComponent.ts*
```typescript
import { Component } from '@angular/core';
import { PopcornService } from './popcorn.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  providers: [PopcornService]
})
export class AppComponent {
  constructor(private popcorn: PopcornService) {}

  cookIt(qty) {
    this.popcorn.cookPopcorn(qty);
  }
}
```


Dependency injection allows you to declare the dependencies of your TypeScript classes without taking care of their
instantiation. Instead, Angular handles the instantiation for you. This design pattern allows you to write more testable
and flexible code. Even though understanding dependency injection is not critical to start using Angular, we strongly
recommend it as a best practice and many aspects of Angular take advantage of it to some degree.

To illustrate how dependency injection works, consider the following example. The first file, logger.service.ts, defines
a Logger class. This class contains a writeCount function that logs a number to the console.

logger.service.ts

```typescript
import {Injectable} from '@angular/core';

@Injectable({providedIn: 'root'})
export class Logger {
  writeCount(count: number) {
    console.warn(count);
  }
}
```

Next, the hello-world-di.component.ts file defines an Angular component. This component contains a button that uses the
writeCount function of the Logger class. To access that function, the Logger service is injected into the HelloWorldDI
class by adding private logger: Logger to the constructor.

hello-world-di.component.ts

```typescript
import {Component} from '@angular/core';
import {Logger} from '../logger.service';

@Component({
  selector: 'hello-world-di',
  templateUrl: './hello-world-di.component.html'
})
export class HelloWorldDependencyInjectionComponent {
  count = 0;

  constructor(private logger: Logger) {
  }

  onLogMe() {
    this.logger.writeCount(this.count);
    this.count++;
  }
}
```

For more information  [Dependency injection ](https://angular.io/guide/dependency-injection)


---

## What is routing

- A website is made up of a multitude of pages These pages are written with HTML(HyperText Markup Language) language.
- Hypertext is the technology that will link a page to other pages via hyperlinks.
- Routing is the mechanism for navigating from one page to another on a website.

For example, if you type these two urls in your browser.

```html
https://en.wikipedia.org/wiki/Braveheart
https://en.wikipedia.org/wiki/Dances_with_Wolves
```

Depending on the movie name indicated in the url, the Wikipedia web application will determine the processing to be
performed. This treatment will display the web page corresponding to the requested movie (here  `Braveheart`
or `Dances_with_Wolves` ).

This is called Routing.

### Angular Routing and Navigation 

- The `Angular Router enables navigation from one view (component)` to the another/next as users perform tasks, views (
  component)
- Routing simply means navigating between different view (component)
- **RouterModule**
  - RouterModule helps to `create routes`, which allows us to move from one part of the application to another part or
    from one view to another
  - A separate NgModule/Angular Module that provides the necessary service providers and directives for navigating
    through application views
- **Router**
  - The Angular Router is an `optional service that presents a particular component view` for a given URL, it is not
    part of the Angular core
  - The Angular Router enables navigation from one view to the another as users perform application tasks/actions
- **router-outlet**
  - The directive `(<router-outlet>)` that marks where the router displays a view (a container to hold different
    views/components loaded as users perform application tasks/actions)
- **routerLink**
  - The attribute/directive for binding a clickable HTML element to a route which denotes link/view name to load/show
    in `(<router-outlet>)`




---

## Angular Module


In Angular, a module is a mechanism to group components, directives, pipes and services that are related, in such a way that can be combined with other modules to create an application.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';

@NgModule ({
    imports:      [ BrowserModule ],
    declarations: [ AppComponent ],
    bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

The NgModule decorator has three options
* The imports option is used to import other dependent modules. The BrowserModule is required by default for any web based angular application
* The declarations option is used to define components in the respective module
* The bootstrap option tells Angular which Component to bootstrap in the application



---

## What is Interpolation?

Interpolation is a special syntax that Angular converts into property binding. It is a convenient alternative to property binding. It is represented by double curly braces(`{{ }}`). The text between the braces is often the name of a component property. Angular replaces that name with the string value of the corresponding component property.

```html
<h3>
  {{title}}
  <img src="{{url}}" style="height:30px">
</h3>
```

In the example , Angular evaluates the title and url properties and fills in the blanks, first displaying a bold application title and then a URL.


---

## Bootstrapping Module

Every application has at least one Angular module, the root module that you bootstrap to launch the application is called as bootstrapping module. It is commonly known as AppModule. The default structure of AppModule generated by AngularCLI would be as follows,

```typescript
/* JavaScript imports */
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from './app.component';

/* the AppModule class with the @NgModule decorator */
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```


---

## JIT vs AOT compilation


Angular has 2 types of build dev build or prod build

### Just-in-Time (JIT)

Just-in-Time (JIT) is a type of compilation that compiles app in the browser at runtime. JIT compilation is the default when you run the ng build (build only) or ng serve (build and serve locally) CLI commands. i.e, the below commands used for JIT compilation,

```javascript
ng build
ng serve
```

### Ahead-of-Time (AOT)
Ahead-of-Time (AOT) is a type of compilation that compiles app at build time. For AOT compilation, include the `--aot` option with the ng build or ng serve command as below,

```javascript
ng build --aot
ng serve --aot
```

```
ng build or ng build --dev   -  this is for development build
ng build --prod              -  this is for production build
```

|Dev Build	                                |Production build                           |
|-------------------------------------------|-------------------------------------------|
|Source maps(.js.map files) are generated	  |Source maps not generated                  |
|Dev Build is not minified and uglified	    |Production Build is minified and uglified  |
|Dev build is not tree shaked	              |Production build is tree shaked            |
|No AOT compilation	                        |AOT compilation takes place                |


* **minification** - process of removing excess whitespace, comments and optinal tokens like curly braces and semi colons
* **uglification** - process of transforming code to use short variable and function names
* **tree shaking** -  is the process of removing any code that we are not actually using in our application from the final bundle

*Note: The ng build command with the --prod meta-flag (`ng build --prod`) compiles with AOT by default.*


### Advantages of AOT

1. **Faster rendering** The browser downloads a pre-compiled version of the application. So it can render the application immediately without compiling the app.
2. **Fewer asynchronous requests** It inlines external HTML templates and CSS style sheets within the application javascript which eliminates separate ajax requests.
3. **Smaller Angular framework download size** Does not require downloading the Angular compiler. Hence it dramatically reduces the application payload.
4. **Detect template errors earlier** Detects and reports template binding errors during the build step itself
5. **Better security** It compiles HTML templates and components into JavaScript.  So there wont be any injection attacks.


### What are the ways to control AOT compilation?

You can control your app compilation in two ways
1. By providing template compiler options in the `tsconfig.json` file
2. By configuring Angular metadata with decorators

---

## How to optimize loading large data in angular?

**Load Time Performance**

1. **AOT**: The Angular Ahead-of-Time (AOT) compiler converts your Angular HTML and TypeScript code into efficient JavaScript code during the build phase before the browser downloads and runs that code. Compiling your application during the build process provides a faster rendering in the browser.
2. **Tree-shaking**: This is the process of removing unused code resulting in smaller build size. In **angular-cli**, Tree-Shaking is enabled by default.
3. **Uglify**: It is the process where the code size is reduced using various code transformations like mangling, removal of white spaces, removal of comments etc. For webpack use uglify plugin and with angular-cli specify the "prod" flag to perform the uglification process.
4. **Lazy loading**: Lazy loading is the mechanism where instead of loading complete app, we load only the modules which are required at the moment thereby reducing the initial load time.
5. **Ivy Render Engine**: It results in much smaller bundle size than the current engine with improved debugging experience.
6. **RxJS**: RxJS makes the whole library more tree-shakable thereby reducing the final bundle size. However, it has some breaking changes like operators chaining is not possible instead, pipe() function (helps in better tree shaking) is introduced to add operators.
7. **Service worker cache**: A service worker is a script that runs in the web browser and manages caching for an application.
8. **defer attribute**: Mentioning defer attribute to script tag will defer the loading of the scripts (sychronous) until the document is not parsed thus making site interactive quicker.
9. **async attribute**: async delays the loading of scripts until the document is not parsed but without respecting the order of loading of the scripts.
10. **ChangeDetectionStrategy.OnPush**: `ChangeDetectionStrategy.OnPush` tells Angular that the component only depends on his Inputs ( aka pure ) and needs to be checked in only the following cases:  
    i). The `Input` reference changes.  
    ii). An event occurred from the component or one of his children.  
    iii). You run change detection explicitly by calling `detectChanges()/tick()/markForCheck()`

Example

```typescript
@Component({
  selector: 'my-select',
  template: `
    ...
  `,
  changeDetection: ChangeDetectionStrategy.OnPush
})
```

11. **TrackBy**: If we provide a trackBy function, Angular can track which items have been added or removed according to the unique identifier and only create or destroy the things that have changed.

Example:

```typescript
@Component({
  selector: 'my-app',
  template: `
    <ul>
      <li *ngFor="let item of collection;trackBy: trackByFn">{{item.id}}</li>
    </ul>
    <button (click)="getItems()">Refresh items</button>
  `,
})
export class App {

  constructor() {
    this.collection = [{id: 1}, {id: 2}, {id: 3}];
  }
  getItems() {
    this.collection = this.getItemsFromServer();
  }
  getItemsFromServer() {
    return [{id: 1}, {id: 2}, {id: 3}, {id: 4}];
  }
  trackByFn(index, item) {
    return index; // or item.id
  }
}
```




---

## How an Angular application gets started or loaded?


The **main.ts** file, that is the first code which gets executed. The job of main.ts is to bootstrap the application. It loads everything and controls the startup of the application.

**main.ts**

```typescript
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

Most importantly here is the line where bootstraps start our angular app by passing app module to the method. AppModule refers to the app.module.ts file.

**app.module.ts**

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, ErrorHandler } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule
  ],
  providers: [ ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

When angular starts, it bootstrap array in `@NgModule`. It basically there is a list of all components which should be known to Angular at the point of time it analyzes **index.html** file.

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Angular 8</title>
    <base href="/" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="icon" type="image/x-icon" href="favicon.ico" />
  </head>
  <body>
    <app-root>Loading...</app-root>
  </body>
</html>
```


---
## when to use angular vs react ?

The choice between using Angular or React depends on the specific needs of the project.

* **Angular** is a full-featured framework, providing a strong set of built-in features and tools for building large, complex web applications. It uses a component-based architecture, and provides features such as dependency injection, a powerful template language, and a built-in set of directives for creating reusable UI components.

* **React**, on the other hand, is a JavaScript library for building user interfaces. It focuses on the declarative approach to building components, making them easy to reason about and debug. React's virtual DOM allows for efficient updates and rendering, making it well suited for building high-performance, responsive user interfaces.

* If you are building a large, complex web application that requires a lot of built-in features, Angular may be a better choice. If you are building a smaller, simpler application or integrating with an existing codebase, React may be a better choice.

* Ultimately, the decision comes down to the specific needs of your project, as well as the preferences and experience of your development team.

### Difference between in Angular and React

Angular and React are both popular JavaScript frameworks/libraries used for building web applications, but they have some key differences:

* **Architecture:** Angular is a full-featured framework, providing a strong set of built-in features and tools for building large, complex web applications. It uses a component-based architecture and follows the Model-View-Controller (MVC) pattern. React, on the other hand, is a JavaScript library for building user interfaces and follows the component-based architecture.

* **Language:** Angular uses TypeScript, a typed superset of JavaScript, while React uses JavaScript.

* **Data Binding:** Angular uses two-way data binding, where changes in the model are reflected in the view and vice versa. React uses one-way data binding, where the component's state is passed down to its children via props.

* **DOM manipulation:** Angular uses a real DOM, where changes to the view result in direct manipulation of the DOM. React uses a virtual DOM, which optimizes updates and renders by only making changes to the parts of the DOM that have actually changed.

* **Learning Curve:** Angular has a steeper learning curve than React, as it provides a lot of built-in features and tools that need to be understood before building an application. React is more focused and has a simpler learning curve.

* **Community:** React has a larger community and more third-party libraries available, but Angular is backed by Google and has a strong corporate support.

* **Use Cases:** Angular is well-suited for building large, complex web applications that require a lot of built-in features and tools. React is well-suited for building smaller, simpler applications or integrating with an existing codebase.

In summary, both Angular and React have their own unique set of features and use cases, and the choice between them will depend on the specific needs of your project and the preferences of your development team.

Another difference between Angular and React is the way they handle forms. Angular provides a powerful template-driven approach to forms, where you can create form controls and validation directly in the template. React, on the other hand, uses a more explicit approach to forms, where you need to create the form controls and validation logic in JavaScript.

* Additionally, **Angular** has a more opinionated structure and file organization, with a specific folder structure and conventions for organizing your code. **React**, on the other hand, is more flexible and allows you to structure your code in a way that makes sense for your application.

* In terms of performance, **React** generally has better performance as it utilizes Virtual DOM and better updates/renders management, However, **Angular** has improved its performance in the latest versions and it also offers Ahead of Time (AOT) compilation and lazy loading features that help to improve the performance.

* Finally, **Angular** is best for large enterprise applications, while **React** is best for building smaller, simpler applications or integrating with an existing codebase. But it's not limited to that, *both Angular and React can be used to build large-scale applications depending on the developer's experience and the resources available*.

---

## What is Observable angular?

* In Angular, an Observable is a powerful way to handle asynchronous data streams. It is a part of the RxJS (Reactive Extensions for JavaScript) library, which is included with Angular.

* An Observable is a stream of events that can emit multiple values over time. It is similar to a Promise, but it can emit multiple values instead of just one. Observables can be used with the async pipe in templates, or with the subscribe() method in component classes.

Here is an example of how to use an Observable in a component class:

```log
import { Component } from '@angular/core';
import { Observable } from 'rxjs';

@Component({
  selector: 'app-root',
  template: `
    <h1>{{ data | async }}</h1>
  `
})
export class AppComponent {
  data: Observable<string>;

  constructor() {
    this.data = new Observable((observer) => {
      setTimeout(() => {
        observer.next('Hello');
      }, 1000);
      setTimeout(() => {
        observer.next('World');
      }, 2000);
    });
  }
}

```

* In this example, the component class creates an observable that emits "Hello" after 1 second and "World" after 2 seconds. The async pipe in the template subscribes to the observable and updates the view with the latest emitted value.

* You can also use the subscribe() method to subscribe to an Observable and handle the emitted values.

```log
this.data.subscribe(
  (value) => console.log(value),
  (error) => console.error(error),
  () => console.log('complete')
);

```
* The subscribe method take 3 callbacks, first one is for value, second one is for error and third one is for complete.

* You can use various RxJs operator like `map`, `filter`, `debounceTime`, `switchMap` etc to manipulate the data coming from an Observable.

---

## BehaviorSubject

* In addition to the `next()` and `subscribe()` methods, BehaviorSubject also has a `getValue()` method that can be used to retrieve the current value of the subject, and a `asObservable()` method that can be used to get an observable that can be subscribed to but can't be updated.

* It's important to note that BehaviorSubject must be initialized with an initial value. If a new subscriber subscribes to the BehaviorSubject before a value has been emitted, they will receive the initial value.

*An example of using a BehaviorSubject to share data between components:

**In a service:**
```log
import { BehaviorSubject } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private data = new BehaviorSubject<string>('initial value');
  currentData = this.data.asObservable();

  updateData(value: string) {
    this.data.next(value);
  }
}

```
**In a component:**
```log
import { DataService } from './data.service';

export class ComponentA {
  constructor(private dataService: DataService) {
    this.dataService.currentData.subscribe(data => {
      console.log(data);
    });
  }

  updateData() {
    this.dataService.updateData('new value');
  }
}

```

Here in this **example**, the `data` BehaviorSubject is used to share data between the `DataService` and `ComponentA`. The `ComponentA` subscribes to the `currentData` observable, which is the `data` BehaviorSubject wrapped in an observable, and updates the value of the data BehaviorSubject using the `updateData()` method.

* **Another advantage** of using `BehaviorSubject` is, it can be used to hold the current state of an application, for example, the currently logged-in user or the current theme. This can be used in a guard to check whether a user is logged in or not before allowing access to a certain route, or to apply styles to the application based on the current theme.

* It's also important to note that if you are using BehaviorSubject for holding state, it's recommended to use it only in a singleton service, so that all the components are using the same instance of the subject. And it's also a good practice to unsubscribe from the subject when the component is destroyed to avoid memory leaks.

* In summary, BehaviorSubject is a powerful tool for sharing and holding state in an Angular application. It can be used to share data between components, hold the current state of an application, and provides a way to get the last emitted value to new subscribers. It's important to use it carefully and unsubscribe from it when the component is destroyed to avoid memory leaks.

### Code Example
```log
import { Component, OnInit, HostBinding } from '@angular/core';
import { BsService } from './bs.service'
import {
  style, animate, transition, state, trigger, keyframes, query, stagger, group,
  animateChild
} from '@angular/animations';

@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ],
  animations: [
      trigger('signal', [
      state('red', style({backgroundColor: 'red'})),
      state('blue', style({'background-color': 'blue'})),
      state('go', style({'background-color': 'green'})),
      transition('* <=> *', [
        animate('.6s ease-in-out')
      ]),
    ])
  ]

})
export class AppComponent implements OnInit  {
  name = this.bs.name;

  constructor(
    private bs: BsService
  ) {}
     ngOnInit(){
   }
}
```
---

## Angular Authentication: Using Route Guards

Route guards in Angular are used to protect routes, so that only authenticated users can access them. They are implemented as classes that implement the CanActivate interface, and they can be added to a route's configuration to control access to it.

A simple example of a route guard that checks whether a user is logged in or not:

```log
import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';
import { AuthService } from './auth.service';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}

  canActivate(): boolean {
    if (!this.authService.isLoggedIn()) {
      this.router.navigate(['/login']);
      return false;
    }
    return true;
  }
}

```

This guard checks whether the user is logged in by calling the `isLoggedIn()` method of the AuthService. If the user is not logged in, the guard redirects them to the login page and returns false, otherwise it returns true, allowing access to the protected route.

To use this guard, you need to add it to the route's configuration.

```log
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'admin', component: AdminComponent, canActivate: [AuthGuard] },
  { path: 'login', component: LoginComponent },
];

```

* In this example, the `admin` route is protected by the `AuthGuard`, and only authenticated users can access it.

* You can also use other types of route guards like `CanActivateChild` to protect child routes, `CanDeactivate` to prevent a user from navigating away from a route, and `CanLoad` to prevent a lazy-loaded module from being loaded.

In summary, Route guards in Angular are a powerful feature that allows you to protect routes and control access to them based on the user's authentication status. They are implemented as classes that implement the `CanActivate` interface, and they can be added to a route's configuration to control access to it.

* `Another way to use route guards` is by using them in combination with an Http interceptor. An Http interceptor is a class that implements the HttpInterceptor interface, which allows you to modify or add functionality to outgoing HTTP requests. You can use an Http interceptor to add an authorization token to the headers of every request, and check the response from the server to see if the user's session is still valid. If the user's session is no longer valid, you can use the route guard to redirect the user to the login page.

* In this case, your route guard will not have to check the user's authentication status, it can simply return true or false based on the value returned by the Http interceptor.
```log
import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';
import { AuthService } from './auth.service';

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}

  canActivate(): boolean {
    if (!this.authService.isAuthorized()) {
      this.router.navigate(['/login']);
      return false;
    }
    return true;
  }
}
 
```
* In this example, the isAuthorized() method of the AuthService is used to check if the user is authorized by checking the value returned by the Http interceptor.

* It's important to note that, when using Http interceptors with route guards, you should handle errors in the interceptor and not in the guard, to avoid duplicating code and make it more maintainable.

In summary, Route guards are a powerful feature in Angular that allows you to protect routes and control access to them. They can be used in combination with Http interceptors to add or check authentication tokens, allowing you to handle authentication and authorization in a centralized and maintainable way.

---

## What is bootstrap module in angular?

The Bootstrap module in Angular is a module that allows you to use Bootstrap CSS framework in your Angular application. Bootstrap is a popular CSS framework that provides a set of pre-defined CSS classes and JavaScript components that can be used to quickly create responsive and visually appealing websites.

In Angular, the Bootstrap module can be imported and used in a few different ways:

* You can use the Angular CLI to install the ng-bootstrap package, which is a set of Angular directives for Bootstrap components. This package allows you to use Bootstrap components in your Angular application without having to include the Bootstrap CSS and JavaScript files in your project.

* You can also import the Bootstrap CSS and JavaScript files in your Angular application manually. You can do this by adding the Bootstrap CSS file to the styles array in the angular.json file, and the Bootstrap JavaScript file to the scripts array in the angular.json file.

* Finally, you can use a pre-built Angular template that already includes Bootstrap. There are many Angular templates available that include Bootstrap, such as the Angular Material, PrimeNG and many more.

* Once you've imported the Bootstrap module, you can use Bootstrap classes and components in your Angular application. Bootstrap classes can be added to HTML elements to style them, and Bootstrap components can be used to create navigation bars, modals, forms, and more.

In summary, The Bootstrap module in Angular is a way to use Bootstrap CSS framework in your Angular application. It can be installed using Angular CLI or imported manually, and it allows you to use Bootstrap classes and components in your Angular application.

---


## Angular js Scope

* In AngularJS (also known as Angular 1), a scope is an object that refers to the model of the application. It is the glue between the controller and the view. Scopes are used to pass data between the controller and the view and to provide a context for expressions that are evaluated in the view.

* Scopes are hierarchical in nature, which means that each scope can have a parent scope, and this parent-child relationship creates a scope hierarchy. This hierarchy is used to look up properties, so that if a property is not found on the current scope, the parent scope is searched, and so on, until the property is found or the $rootScope is reached.

* A controller can create a new scope by injecting the $scope service and then attaching properties and functions to it. These properties and functions can then be accessed in the view.

* **For example:**
```log
app.controller('MyController', function($scope) {
  $scope.name = 'John Doe';
  $scope.sayHello = function() {
    alert('Hello ' + $scope.name);
  };
});
 
```
* In the above example, the controller creates a new scope and attaches a name property and a sayHello function to it. These properties and functions can then be accessed in the view:

```log
<div ng-controller="MyController">
  <p>{{ name }}</p>
  <button ng-click="sayHello()">Say Hello</button>
</div>

```
* Here, the view binds to the name property to display its value and binds to the sayHello function to execute it when the button is clicked.

* In AngularJS, scopes also provide a mechanism for handling events, such as button clicks, and for registering watchers, which can be used to update the view when the model changes.

In summary, In AngularJS, a scope is an object that refers to the model of the application, it acts as a glue between the controller and the view, it is used to pass data between the controller and the view and to provide a context for expressions that are evaluated in the view. Scopes are hierarchical in nature, and a controller can create a new scope by injecting the $scope service and then attaching properties and functions to it, which can then be accessed in the view.

---
## What is  angular disadvantages ?

Angular is a powerful and widely-used framework for building web applications, but like any technology, it has its own set of disadvantages. Some of the most notable disadvantages of Angular include:

1. **Steep Learning Curve:** Angular has a relatively steep learning curve, especially for developers who are new to the framework. Angular uses a lot of advanced concepts and technologies, such as dependency injection, directives, and observables, which can be difficult to understand and master.

2. **Complexity:** Angular's architecture and design can be quite complex, especially for large and complex applications. This can make it difficult to understand the overall structure and organization of the application, and can make it challenging to debug and troubleshoot issues.

3. **Performance:** Angular can have performance issues, especially when working with large and complex applications. This is due to the framework's use of two-way data binding and change detection, which can cause the application to slow down and become unresponsive.

4. **Size:** Angular has a large file size, which can make it take longer to load and can slow down the performance of the application, especially on low-end devices or with slow internet connection.

5. **Limited Flexibility:** Angular follows a specific pattern and structure, which can be limiting for developers who want to experiment with different approaches or use different libraries.

6. **Limited Mobile Support:** Angular is primarily geared towards building web applications, and its mobile support is limited. While it's possible to build mobile apps with Angular, it's not as well suited for mobile development as other frameworks like React Native.

In summary, Angular is a powerful and widely-used framework for building web applications, but it has its own set of disadvantages, such as a steep learning curve, complexity, performance issues, large file size, limited flexibility and limited mobile support.

---

## Angular Bootstrap Responsive Grid

1. The Angular Bootstrap responsive grid is a way to create a responsive layout in an Angular application using the Bootstrap CSS framework. Bootstrap includes a responsive grid system that allows you to create a flexible and responsive layout for different screen sizes.

2. The grid system in Bootstrap is based on a 12-column layout, where each row is divided into 12 equal-width columns. You can use the `.col-*` classes to specify the number of columns that a particular element should span. For example, if you want an element to span 6 columns, you can use the class `.col-6`.

3. In addition to the `.col-*` classes, Bootstrap also includes classes for different screen sizes, such as `.col-sm-*`, `.col-md-*`, `.col-lg-*`, and `.col-xl-*`. These classes allow you to specify the number of columns that an element should span for different screen sizes.

4. For example, you can use the class .col-sm-6 to specify that an element should span 6 columns on small screens and `.col-md-4` to specify that it should span 4 columns on medium screens.

Here's an example of how you can use the Bootstrap responsive grid in an Angular application:
```log
<div class="container">
  <div class="row">
    <div class="col-sm-6 col-md-4">
      <div class="card">
        <div class="card-body">
          <h5 class="card-title">Card Title</h5>
          <p class="card-text">Card content</p>
        </div>
      </div
```

---

## Angular 12 scope types

* In Angular (version 2 and above), the concept of scope is not used, Instead, Angular uses a different way to handle data binding, change detection, and component hierarchy which is called Zones.

* In Angular, components and directives have access to their own change detection and data binding, and the framework uses a unidirectional data flow, where data is passed down from a parent component to its children through inputs and events. Components can also communicate with each other by using a shared service or by emitting events.

* The change detection system in Angular is based on the concept of zones, which are responsible for running change detection checks on all the components of an application. When something changes in the application, the change detection system runs a check on all the components and updates the view accordingly.

In summary, Angular (version 2 and above) does not use the concept of scopes, Instead, it uses Zones and unidirectional data flow. Components and directives have access to their own change detection and data binding, and they can communicate with each other through shared services or events. The change detection system in Angular is based on Zones which are responsible for running change detection checks on all the components of an application.

### Angular 12 features

Angular 12 is the latest version of Angular and it brings several new features and improvements over previous versions. Some of the most notable features in Angular 12 include:

1. **Faster Builds:** Angular 12 includes a new feature called the "differential loading by default", which allows the browser to download the version of the JavaScript that it supports, resulting in faster build times and better performance.

2. **Dynamic imports for lazy-loaded modules:** Angular 12 allows you to use dynamic imports for lazy-loaded modules, which can result in faster load times and better performance.

3. **Improved Ivy:** Angular 12 includes further improvements to Ivy, Angular's new renderer, which aims to improve the performance and size of Angular applications.

4. **Faster testing:** Angular 12 includes a new testing harness that can run tests faster and more efficiently.

5. **Improved type-checking:** Angular 12 includes a new feature called "strict mode" that can help you catch potential type errors in your code.

6. **Improved Logging:** Angular 12 includes improved logging to help you better understand the performance of your application and to help identify and fix issues.

7. **Improved Internationalization (i18n):** Angular 12 includes improved support for internationalization, which makes it easier to create applications that can be localized for different languages and cultures.

8. **Deprecation of "scope" in the context of the core framework:** Angular 12 deprecates the use of the term "scope" in the context of the core framework. The core framework no longer uses the concept of scope, and the term is replaced by more specific terms such as "component" and "directive".

In summary, Angular 12 is the latest version of Angular and it brings several new features and improvements over previous versions, such as faster builds, dynamic imports for lazy-loaded modules, improved Ivy, faster testing, improved type-checking, improved logging,

### Angular 12 disadvantage

Like any technology, Angular 12 has its own set of disadvantages. Some of the most notable disadvantages of Angular 12 include:

1. **Steep Learning Curve:** Angular 12 has a relatively steep learning curve, especially for developers who are new to the framework. Angular 12 uses a lot of advanced concepts and technologies, such as dependency injection, directives, and observables, which can be difficult to understand and master.

2. **Complexity:** Angular 12's architecture and design can be quite complex, especially for large and complex applications. This can make it difficult to understand the overall structure and organization of the application, and can make it challenging to debug and troubleshoot issues.

3. **Performance:** Angular 12 can have performance issues, especially when working with large and complex applications. This is due to the framework's use of two-way data binding and change detection, which can cause the application to slow down and become unresponsive.

4. **Size:** Angular 12 has a relatively large file size, which can make it take longer to load and can slow down the performance of the application, especially on low-end devices or with slow internet connection.

5. **Limited Flexibility:** Angular 12 follows a specific pattern and structure, which can be limiting for developers who want to experiment with different approaches or use different libraries.

6. **Limited Mobile Support:** Angular 12 is primarily geared towards building web applications, and its mobile support is limited. While it's possible to build mobile apps with Angular 12, it's not as well suited for mobile development as other frameworks like React Native.

In summary, Angular 12 is a powerful and widely-used framework for building web applications, but it has its own set of disadvantages, such as a steep learning curve, complexity, performance issues, large file size, limited flexibility and limited mobile support.

---

## Angular 10 scope types

* In Angular (version 2 and above), the concept of scope is not used, Instead, Angular uses a different way to handle data binding, change detection, and component hierarchy which is called Zones.

* In Angular, components and directives have access to their own change detection and data binding, and the framework uses a unidirectional data flow, where data is passed down from a parent component to its children through inputs and events. Components can also communicate with each other by using a shared service or by emitting events.

* The change detection system in Angular is based on the concept of zones, which are responsible for running change detection checks on all the components of an application. When something changes in the application, the change detection system runs a check on all the components and updates the view accordingly.

In summary, Angular (version 2 and above) does not use the concept of scopes, Instead, it uses Zones and unidirectional data flow. Components and directives have access to their own change detection and data binding, and they can communicate with each other through shared services or events. The change detection system in Angular is based on Zones which are responsible for running change detection checks on all the components of an application. This applies to Angular 10 as well.

### Angular 10 Features

Angular 10 is the latest version of Angular and it brings several new features and improvements over previous versions. Some of the most notable features in Angular 10 include:

1. **Automatic Inlining of Fonts:** Angular 10 includes a new feature that automatically inlines fonts in the application, which can result in faster load times and better performance.

2. **TypeScript 4.0 Support:** Angular 10 supports TypeScript 4.0, which includes several new features and improvements, such as improved support for destructuring, improved type-checking, and better type inference.

3. **Deprecation of the ngModelChange event:** Angular 10 deprecates the ngModelChange event and replaces it with the ngModelInput event. This change is intended to make the event names more consistent and to improve the handling of input events.

4. **Deprecation of the ngOutletContext directive:** Angular 10 deprecates the ngOutletContext directive and replaces it with the ngTemplateOutletContext directive. This change is intended to improve the consistency of the API and to make it more intuitive.

5. **Improved Error Handling:** Angular 10 includes improved error handling, which makes it easier to identify and fix errors in the application.

6. **Improved Internationalization (i18n):** Angular 10 includes improved support for internationalization, which makes it easier to create applications that can be localized for different languages and cultures.

7. **Improved Lazy Loading:** Angular 10 includes improved support for lazy loading, which makes it easier to create large and complex applications that load faster and perform better.

8. **Improved Testing:** Angular 10 includes improved testing, which makes it easier to test the application and to identify and fix issues.

In summary, Angular 10 is the latest version of Angular and it brings several new features and improvements over previous versions, such as Automatic Inlining of Fonts, TypeScript 4.0 Support, Deprecation of the ngModelChange event, Deprecation of the ngOutletContext directive, Improved Error Handling, Improved Internationalization, Improved Lazy Loading, Improved Testing.

### Angular 10 Disadvantage

Like any technology, Angular 10 has its own set of disadvantages. Some of the most notable disadvantages of Angular 10 include:

1. **Steep Learning Curve:** Angular 10 has a relatively steep learning curve, especially for developers who are new to the framework. Angular 10 uses a lot of advanced concepts and technologies, such as dependency injection, directives, and observables, which can be difficult to understand and master.

2. **Complexity:** Angular 10's architecture and design can be quite complex, especially for large and complex applications. This can make it difficult to understand the overall structure and organization of the application, and can make it challenging to debug and troubleshoot issues.

3. **Performance:** Angular 10 can have performance issues, especially when working with large and complex applications. This is due to the framework's use of two-way data binding and change detection, which can cause the application to slow down and become unresponsive.

4. **Size:** Angular 10 has a relatively large file size, which can make it take longer to load and can slow down the performance of the application, especially on low-end devices or with slow internet connection.

5. **Limited Flexibility:** Angular 10 follows a specific pattern and structure, which can be limiting for developers who want to experiment with different approaches or use different libraries.

6. **Limited Mobile Support:** Angular 10 is primarily geared towards building web applications, and its mobile support is limited. While it's possible to build mobile apps with Angular 10, it's not as well suited for mobile development as other frameworks like React Native.

In summary, Angular 10 is a powerful and widely-used framework for building web applications, but it has its own set of disadvantages, such as a steep learning curve, complexity, performance issues, large file size, limited flexibility and limited mobile support.

---
## Angular Scope Tutorial

### Overview

In this post, we are reviewing scope in Angular. It is passed as an argument when we make a controller:

```log
<script>
var myApp = angular.module('myApp', []);

myApp.controller('myController', function($scope) {
    $scope.name = "Red Dead Redemption";
});
</script>
```

* Scope is actually an object that refers to the model in an application structure, such as Model View Controller (MVC) .

* It provides definitions – also known as context – for JavaScript-like code snippets called expressions. Scopes are structured in a hierarchy that mimics the Document Object Model (DOM) structure of the application. Scopes can watch expressions and propagate events in a similar way to DOM events.

### Scope Is a Data Model

What does it mean for Scope to be a data model? It is a JavaScript object with properties and methods that can be accessed by both the view and controller.

Here, we have an example that demonstrates how modifying the view can affect the controller and model:

```log
<!DOCTYPE html>
<html>
   <script src = "https://ajax.googleapis.com/ajax/libs/angularjs/1.7.5/angular.min.js"></script>
<body>

<div ng-app="demoApp" ng-controller="demoCtrl">

<input ng-model="word">

<h1>Hello, {{word}}!</h1>

</div>

<script>
var app = angular.module('demoApp', []);
app.controller('demoCtrl', function($scope) {
    $scope.word = "word";
});
</script>

<p>If we change the word in the input field, the change will affect the model and the word property in the controller.</p>

</body>
</html>
```
In this simple example, if we modify the input in the web page, we see the value change for the greeting in the <h1> tags.

### 3. Root Scope and Hierarchies

* Each Angular application has only one root scope but can have any number of child scopes.

* An application can have several scopes because directives can create new child scopes. When new scopes are created, they become children of their parent scope. This creates a tree structure which parallels the DOM where they’re attached.

The example below:

```log
<script src = "https://ajax.googleapis.com/ajax/libs/angularjs/1.7.5/angular.min.js"></script>
  <script>
  (function(angular) {
  'use strict';
angular.module('scopeExample', [])
  .controller('HelloController', ['$scope', '$rootScope', function($scope, $rootScope) {
    $scope.name = 'World';
    $rootScope.department = 'Red Dead Redemption 2';
  }])
  .controller('ListController', ['$scope', function($scope) {
    $scope.names = ['Arthur', 'Dutch', 'Bill'];
  }]);
})(window.angular);

  </script>

</head>
<body ng-app="scopeExample">
  <div class="show-scope-demo">
  <div ng-controller="HelloController">
    Hello {{name}}!
  </div>
  <div ng-controller="ListController">
    <ol>
      <li ng-repeat="name in names">{{name}} from {{department}}</li>
    </ol>
  </div>
</div>
```

---

## Angular Decorators

An Angular decorator is a function that modifies the behavior or properties of a class, method, or property. They are used to add metadata to a class, method, or property, which is used by Angular to change the way it behaves or is displayed. Decorators in Angular are prefixed with the **@** symbol and are applied to the class, method, or property that they are modifying. For example, the `@Component` decorator is used to define a class as an Angular component, while the `@Input` decorator is used to define a property as an input to a component.

### Significance of Angular Decorators

* The significance of decorators in Angular is that they allow developers to add metadata to a class, method, or property, which is then used by the Angular framework to change the behavior or display of that class, method, or property.

* **For example**, the `@Component` decorator is used to define a class as an Angular component, which allows Angular to recognize the class as a component and treat it as such. The `@Input` decorator is used to define a property as an input to a component, allowing the component to receive data from its parent component.

* Decorators are also significant because they make the code more readable and maintainable by providing a clear and concise way to add metadata to a class, method, or property. They also make it easy to reuse and share code between different parts of an application by allowing developers to define a set of decorators that can be applied to multiple classes, methods, or properties.

In summary, decorators in Angular are a powerful tool that allows developers to easily add metadata to classes, methods, and properties which helps the Angular framework to understand and interact with the code, and also makes the code more readable and maintainable.

### Example of Angular Decorators

1. One example of an Angular decorator is the `@Component` decorator, which is used to define a class as an Angular component. Here is an example of how it can be used:

```log
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<h1>Hello, Angular!</h1>`,
  styles: [`h1 { color: blue; }`]
})
export class AppComponent {
  title = 'my-app';
}

```

In this example, the `@Component` decorator is applied to the AppComponent class, and it is given a configuration object that defines the component's selector, template, and styles. The selector is used to define the HTML tag that will be used to display the component, the template is used to define the component's template, and the styles are used to define the component's styles.

2. Another example is `@Input()` decorator, which is used to define a property as an input to a component. Here is an example:

```log
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <p>The value of myInput is: {{ myInput }}</p>
  `
})
export class ChildComponent {
  @Input() myInput: string;
}

```

In this example, the `@Input()` decorator is applied to the myInput property, which means that this property can receive data from its parent component.

These are just a couple examples of how decorators are used in Angular, there are many other decorators that are available in Angular framework like `@Output`, `@ViewChild`, `@ViewChildren`,` @HostBinding`, `@HostListener`, etc.

---

## Angular Local Storage

* In Angular, `local storage` is a way to store data on the client-side (in the browser) that can be accessed and used even after the user closes the browser or the browser tab. Local storage is a key-value store, where you can store data using a string key and retrieve it using the same key.

* Angular provides the `localStorage` object, which is an instance of the Storage interface, and it is part of the Window object. It provides the same methods as the `sessionStorage` object, such as `setItem`, `getItem`, `removeItem`, and `clear`. Here is an example of how to use `localStorage` in Angular:

```log
import { Inject } from '@angular/core';

export class MyService {
  constructor(@Inject(Window) private window: Window) {}

  setData(key: string, value: any) {
    this.window.localStorage.setItem(key, JSON.stringify(value));
  }

  getData(key: string) {
    return JSON.parse(this.window.localStorage.getItem(key));
  }
}

```

* In this **example**, a service `MyService` is created which is using the `localStorage` object to store and retrieve data. The `setData` method is used to store data in the local storage, and the `getData` method is used to retrieve data from the local storage. Note that the `localStorage` object can only store strings, so when you store an object, you need to use JSON.stringify to convert it to a string, and when you retrieve it, you need to use JSON.parse to convert it back to an object.

* It's worth noting that Local storage is a powerful feature and it can be used to store sensitive data, such as user tokens, it's important to be aware of security concerns such as XSS attacks.

* Yes, it's important to be aware of security concerns when working with local storage. One of the main security concerns with local storage is cross-site scripting (XSS) attacks. XSS attacks occur when an attacker injects malicious code into a web page, which can then access and steal sensitive information stored in the local storage. To protect against XSS attacks, it is important to properly validate and sanitize any data that is stored in the local storage, and to use the HttpOnly and Secure flags when storing sensitive data in cookies.

* Another security concern is that local storage data is persisted even if the user closes the browser or the browser tab, so it's important to properly handle user logouts and session expirations. It's also important to be aware that local storage data is shared across all tabs and windows of the same origin, which could lead to security vulnerabilities if the data is not properly protected.

* In summary, it's important to be aware of security concerns when working with local storage in Angular, such as XSS attacks, user logouts and session expirations, and data sharing across tabs and windows. The best practice is to validate, sanitize, and properly handle sensitive data and use the HttpOnly and Secure flags when storing sensitive data in cookies.

---

## Angular Architecture

* Angular architecture refers to the design and structure of an Angular application, including the organization of components, services, and modules. A well-designed architecture makes an Angular application more maintainable, testable, and scalable.

* One of the key components of Angular architecture is the use of components, which are the building blocks of an Angular application. Components define the view and behavior of an application, and they are usually organized into a tree-like structure, with parent and child components.

* Another important component of Angular architecture is the use of services, which are used to encapsulate business logic and share data across components. Services are typically stateless and are injected into components using Angular's dependency injection system.

* Modules are also an important component of Angular architecture. They are used to group related components, services, and other code together. Angular uses a modular structure, where an application is divided into multiple modules, each one with its own set of components, services, and routing configurations.

* Angular also provides support for reactive programming through RxJS, which allows you to handle asynchronous data streams in a consistent and efficient way. This approach is known as reactive programming.

* One of the best practices in Angular architecture is the use of the Model-View-Controller (MVC) design pattern. This design pattern separates the application into three main components: the model (which holds the data), the view (which displays the data), and the controller (which handles the logic). This pattern allows the code to be more organized and maintainable.

* In summary, Angular architecture is the design and structure of an Angular application, including the organization of components, services, and modules. It is important to follow best practices such as modular structure, proper use of dependency injection, and reactive programming in order to create maintainable, testable, and scalable applications.

---

## Angular declaration vs Provider

### Angular Declaration

* In Angular, a declaration is used to add a component, directive, or pipe to a module. The process of adding these elements to a module is called "declaring" them.

* A component, directive, or pipe is typically defined as a class, which is then decorated with the appropriate decorator (`@Component()`, `@Directive()`, or `@Pipe()`) to indicate its *type*. Once a class is decorated as a component, directive, or pipe, it can be added to a module by including it in the `declarations` array of the `@NgModule()` decorator.

* For example, if you have a component called MyComponent that you want to add to your application, you would first define the component class and decorate it with `@Component()`. Then, you would include the component in the `declarations` array of the `@NgModule()` decorator for the module that you want to add it to.

* It's worth mentioning that once a component, directive, or pipe is declared in a module, it can be used in the template of any component that is part of that module. Also, when a component is declared in a module, it is only available for the template of that specific module and its child modules, unless it's exported.

### Angular Provider

* In Angular, a provider is a way to configure a service or value that can be injected into other components or services. Providers are registered with Angular's dependency injection system, which allows other parts of the application to access the service or value through injection.

* A provider is typically defined using the `@Injectable()` decorator, which can be applied to a class to indicate that it should be treated as a provider. The class should also have an `ngOnInit` method. Once a class is decorated as an injectable, it can be registered with Angular by adding it to the `providers` array of an NgModule or the `providers` array of a component.

* In addition to services, providers can also be used to configure other types of values, such as constants or objects. This allows these values to be easily shared across multiple parts of the application, making them more manageable and testable.

* It's worth mentioning that when a service is provided in the providers array of a module, it creates a new instance of that service for every instance of that module. In case you want to share a single instance of the service among all the components, you can provide that service in the providers array of the @NgModule decorator.

### Declaration vs Provider

* In Angular, a `declaration` is used to add a component, directive, or pipe to a module. A `provider` is used to configure a service or value that can be injected into other components or services.

* For **example**, if you have a component that needs to use a service, you would use a provider to register the service with Angular's dependency injection system. Then, you can use the component's constructor to inject the service and use it in the component.

* On the other hand, if you want to create a new component and add it to your application, you would use a declaration to add the component to an NgModule.

* In summary, `declarations` are used to create new elements that can be used in templates and are declared in the declarations array of a module. `Providers` are used to configure services and values that can be injected into other parts of the application and are declared in the providers array of a module or component.

---




## For more information

1. [Angular Routing and Navigation](https://github.com/sunilsoni/interview-notes/blob/main/angular/angular-routing.md#1-angular-routing-and-navigation)
2. [Routing and navigation with Angular 11](https://www.ganatan.com/tutorials/routing-with-angular)

