---
layout: default
title: Component
parent: Angular
resource: true
grand_parent: UI Design
desc: "Angular Component interview questions and answers."
categories: [Angular Component]
---

# Angular Component
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



Components are the most basic UI building block of an Angular app which formed a tree of Angular components. These components are subset of directives. Unlike directives, components always have a template and only one component can be instantiated per an element in a template.

```typescript
import { Component } from '@angular/core';

@Component ({
    selector: 'my-app',
    template: ` <div>
        <h1>{{title}}</h1>
        <div>Angular components example</div>
    </div> `,
})

export class AppComponent {
    title: string = 'Welcome to Angular world';
}
```


Angular Component = HTML Template + Component Class + Component Metadata

 <img src="images/angular-component.png" width="300" border="2" />

Every Angular application has at least one component that is used to display the data on the view. Technically, a
component is nothing but a simple typescript class and composed of three things as follows:

    1. Class (Typescript class)
    2. Template (HTML Template or Template URL)
    3. Component Metadata (@Component Decorator)


---

##  Template

The template is used to define an interface with which the user can interact. As part of that template, you can define
HTML Mark-up; you can also define the directives, and bindings, etc. So in simple words, we can say that the template
renders the view of the application with which the end-user can interact i.e. user interface.

---

##  Class

The Class is the most important part of a component in which we can write the code which is required for a template to
render in the browser. You can compare this class with any object-oriented programming language classes such as C++, C#
or Java. The angular component class can also contain methods, variables, and properties like other programming
languages. The angular class properties and variables contain the data which will be used by a template to render on the
view. Similarly, the method in an angular class is used to implement the business logic like the method does in other
programming languages.

---

##  Component Metadata

Metadata is some extra data for a component used by Angular API to execute the component, such as the location of HTML
and CSS files of the component, selector, providers, etc.

`Note:` Whenever we create any component, we need to define that component in `@NgModule`.

Components are like the basic building block in an Angular application. Components are defined using the `@component`
decorator. A component has a `selector`, `template`, `style` and other properties, using which it specifies the metadata
required to process the component.

From the official docs:

> Components are the most basic building block of an UI in an Angular application. An Angular application is a tree of Angular components. 
Angular components are a subset of directives. Unlike directives, components always have a template and only one component can be instantiated per an element in a template.


---

##  Communication Between Components


There are 4 ways to share data between components:

1. Parent to Child: Sharing Data via `Input`
2. Child to Parent: Sharing Data via `ViewChild` with `AfterViewInit`
3. Child to Parent: Sharing Data via `Output()` and `EventEmitter`
4. Unrelated Components: Sharing Data with a `Service`


###   Parent to Child: Sharing Data via Input

It works by using the `@Input()` decorator to allow data to be passed via the template.

parent.component.ts

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child [childMessage]="parentMessage"></app-child>
  `,
  styleUrls: ['./parent.component.css']
})
export class ParentComponent{
  parentMessage = "message from parent"
  constructor() { }
}
```

child.component.ts

```typescript
import { Component, Input } from '@angular/core';

@Component({
    selector: 'app-child',
    template: `
      Say {{ message }}
  `,
    styleUrls: ['./child.component.css']
})
export class ChildComponent {

    @Input() childMessage: string;

    constructor() { }

}
```

###   Child to Parent: Sharing Data via ViewChild

`ViewChild` allows a one component to be injected into another, giving the parent access to its attributes and functions. One caveat, however, is that child won’t be available until after the view has been initialized. This means we need to implement the `AfterViewInit` lifecycle hook to receive the data from the child.

parent.component.ts
```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { ChildComponent } from "../child/child.component";

@Component({
  selector: 'app-parent',
  template: `
    Message: {{ message }}
    <app-child></app-child>
  `,
  styleUrls: ['./parent.component.css']
})
export class ParentComponent implements AfterViewInit {

  @ViewChild(ChildComponent) child;

  constructor() { }

  message:string;

  ngAfterViewInit() {
    this.message = this.child.message
  }
}

```

child.component.ts

```typescript
import { Component} from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
  `,
  styleUrls: ['./child.component.css']
})
export class ChildComponent {

  message = 'Hola Mundo!';

  constructor() { }

}

```


###   Child to Parent: Sharing Data via Output() and EventEmitter
  
Another way to share data is to emit data from the child, which can be listened to by the parent. This approach is ideal when you want to share data changes that occur on things like button clicks, form entires, and other user events.

In the parent, we create a function to receive the message and set it equal to the message variable.

In the child, we declare a messageEvent variable with the Output decorator and set it equal to a new event emitter. Then we create a function named sendMessage that calls emit on this event with the message we want to send. Lastly, we create a button to trigger this function.

The parent can now subscribe to this messageEvent that’s outputted by the child component, then run the receive message function whenever this event occurs.

parent.component.ts
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    Message: {{message}}
    <app-child (messageEvent)="receiveMessage($event)"></app-child>
  `,
  styleUrls: ['./parent.component.css']
})
export class ParentComponent {

  constructor() { }

  message:string;

  receiveMessage($event) {
    this.message = $event
  }
}
```

child.component.ts

```typescript
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
      <button (click)="sendMessage()">Send Message</button>
  `,
  styleUrls: ['./child.component.css']
})

export class ChildComponent {

  message: string = "Hola Mundo!"

  @Output() messageEvent = new EventEmitter<string>();

  constructor() { }

  sendMessage() {
    this.messageEvent.emit(this.message)
  }
}
```

###   Unrelated Components: Sharing Data with a Service

When passing data between components that lack a direct connection, such as siblings, grandchildren, etc, you should you a shared service. When you have data that should aways been in sync, I find the RxJS BehaviorSubject very useful in this situation.

You can also use a regular RxJS Subject for sharing data via the service, but here’s why I prefer a `BehaviorSubject`.

- It will always return the current value on subscription - there is no need to call onnext
- It has a getValue() function to extract the last value as raw data.
- It ensures that the component always receives the most recent data.

In the service, we create a private `BehaviorSubject` that will hold the current value of the message. We define a currentMessage variable handle this data stream as an observable that will be used by the components. Lastly, we create function that calls next on the `BehaviorSubject` to change its value.

The parent, child, and sibling components all receive the same treatment. We inject the DataService in the constructor, then subscribe to the currentMessage observable and set its value equal to the message variable.

Now if we create a function in any one of these components that changes the value of the message. when this function is executed the new data it’s automatically broadcast to all other components.

data.service.ts

```typescript
import {Injectable} from '@angular/core';
import {BehaviorSubject} from 'docs/angular/RxJS';

@Injectable()
export class DataService {

    private messageSource = new BehaviorSubject('default message');
    currentMessage = this.messageSource.asObservable();

    constructor() {
    }

    changeMessage(message: string) {
        this.messageSource.next(message)
    }

}
```
parent.component.ts

```typescript
import {Component, OnInit} from '@angular/core';
import {DataService} from "../data.service";
import {Subscription} from 'docs/angular/rxjs';

@Component({
    selector: 'app-parent',
    template: `
    {{message}}
  `,
    styleUrls: ['./sibling.component.css']
})
export class ParentComponent implements OnInit, OnDestroy {

    message: string;
    subscription: Subscription;

    constructor(private data: DataService) {
    }

    ngOnInit() {
        this.subscription = this.data.currentMessage.subscribe(message => this.message = message)
    }

    ngOnDestroy() {
        this.subscription.unsubscribe();
    }

}
```

sibling.component.ts

```typescript
import {Component, OnInit} from '@angular/core';
import {DataService} from "../data.service";
import {Subscription} from 'docs/angular/rxjs';

@Component({
    selector: 'app-sibling',
    template: `
    {{message}}
    <button (click)="newMessage()">New Message</button>
  `,
    styleUrls: ['./sibling.component.css']
})
export class SiblingComponent implements OnInit, OnDestroy {

    message: string;
    subscription: Subscription;

    constructor(private data: DataService) {
    }

    ngOnInit() {
        this.subscription = this.data.currentMessage.subscribe(message => this.message = message)
    }

    ngOnDestroy() {
        this.subscription.unsubscribe();
    }

    newMessage() {
        this.data.changeMessage("Hello from Sibling")
    }

}
```


---
## when to use angular component vs directive ?

In Angular, both components and directives are used to create reusable UI elements, but they are used for different purposes.

* `Components` are the building blocks of an Angular application, they allow you to create custom elements that can be used in your templates. Components have a well-defined lifecycle, and they are associated with a specific view. They are used to create reusable UI elements that can be composed to create more complex views.

* `Directives`, on the other hand, are used to add behavior to existing elements. They do not have their own view and don't have a lifecycle of their own. Directives are used to manipulate the DOM, and they can be used to add functionality to existing elements, such as adding validation to form inputs or creating custom directives that can be used to create reusable UI elements.

* In general, you should use a component when you need to create a reusable UI element that has its own view and lifecycle. You should use a directive when you need to add behavior to existing elements, such as adding validation to form inputs, or creating custom directives that can be used to create reusable UI elements.

* It's worth noting that starting Angular 9 version, Angular introduced a new feature called `Component Directives` which allows you to define a directive with a template, this way you can create reusable components using directive with less boilerplate code.

In summary, you should use a component when you need to create a reusable UI element with its own view and lifecycle, and use a directive when you need to add behavior to existing elements or create reusable UI elements that don't have their own view.

### Difference between in angular component vs directive

The main difference between components and directives in Angular is their purpose and how they are used.

* `Components` are the building blocks of an Angular application, they allow you to create custom elements that can be used in your templates. `Components` have a well-defined lifecycle, and they are associated with a specific view. They are used to create reusable UI elements that can be composed to create more complex views. Components have a template, a class, and metadata (decorated by @Component) that defines the behavior of the component.

* `Directives`, on the other hand, are used to add behavior to existing elements. They do not have their own view and don't have a lifecycle of their own. `Directives` are used to manipulate the DOM, and they can be used to add functionality to existing elements, such as adding validation to form inputs or creating custom directives that can be used to create reusable UI elements. Directives have a class and metadata (decorated by @Directive) that defines the behavior of the directive.

* `Components` are used to create reusable UI elements that have a view and lifecycle, while `directives` are used to add behavior to existing elements without having a view of their own.

* Another key difference is that `components` have a template and a class, while `directives` only have a class. `Components` can also have inputs and outputs, which allow them to communicate with other components, while `directives` do not have this capability.

* In summary, `components` are used to create reusable UI elements with their own view and lifecycle, while `directives` are used to add behavior to existing elements without having a view of their own.

* Another difference between **Angular components and directives** is how they are used in the template. Components are used as elements, with a custom tag name, for example, `<app-header>` or `<app-footer>`. Directives are used as attributes, and are applied to existing elements, for example,` <div *ngIf="showHeader"></div>` or`FAngular Http Interceptor`.

* It's also worth noting that Angular provides some built-in directives like ngIf, ngFor, ngSwitch, etc.., these directives are used to add behavior to the existing element, like adding or removing an element based on some condition, displaying a list of elements, etc..

* Another difference is that components can have their own styles, encapsulated to the component, while directives don't have this feature.

* In short, Components are more powerful than Directives, they have more features and capabilities, like having their own views, lifecycle, inputs, outputs, styles, etc. while Directives are mainly used to add behavior to existing elements and manipulate the DOM.

* It's worth mentioning that starting Angular 9 version, Angular introduced a new feature called 'Component Directives' which allows you to define a directive with a template, this way you can create reusable components using directive with less boilerplate code.



















##  For more information

1. [Angular Components with Examples](https://dotnettutorials.net/lesson/angular-components/)
2. [Angular Component](https://www.tutorialsteacher.com/angular/angular-component)
3. [Component interaction](https://angular.io/guide/component-interaction#component-interaction)
4. [How Angular components communicate?](https://www.thirdrocktechkno.com/blog/how-angular-components-communicate/)
5. [Sharing Data between Angular Components - Four Methods](https://fireship.io/lessons/sharing-data-between-angular-components-four-methods/)