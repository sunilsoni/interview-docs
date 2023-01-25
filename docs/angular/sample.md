---
layout: default
title: Code Samples
parent: Angular
resource: true
desc: "Angular Code interview questions and answers."
categories: [Samples]
---

# Code Samples
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


##  Call backend rest apis call

Angular 12 that makes a GET request to a Spring Boot RESTful API endpoint:

### Creates a new Angular project to call the backed API

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
    providedIn: 'root'
})
export class MyService {

    private baseUrl = 'http://localhost:8080/api';

    constructor(private http: HttpClient) { }

    getData(): Observable<any> {
        return this.http.get(`${this.baseUrl}/data`);
    }
}

```

This service is using the HttpClient module provided by Angular to make a GET request to the endpoint "http://localhost:8080/api/data". The http.get() method returns an observable, which can be subscribed to in a component to handle the response.

Here's an example of how a component can use this service to make the GET request and handle the response:

```typescript
import { Component, OnInit } from '@angular/core';
import { MyService } from './my.service';

@Component({
    selector: 'app-my-component',
    template: `
    <div *ngIf="data">
      {{ data }}
    </div>
  `
})
export class MyComponent implements OnInit {

    data: any;

    constructor(private myService: MyService) { }

    ngOnInit() {
        this.myService.getData().subscribe(
            data => {
                this.data = data;
            },
            error => {
                console.log(error);
            }
        );
    }
}

```

In this example, the component is injecting the service and using the ngOnInit() lifecycle hook to make the GET request when the component is initialized. The subscribe() method is used to handle the response of the GET request. If the request is successful, the response data is stored in the data property and displayed in the template using interpolation. In case of an error, it will log the error message.

This is a simple example of how you can use Angular HttpClient module to make a GET request to a Spring Boot RESTful API endpoint. You can also use the http.post(), http.put(), and http.delete() methods to make POST, PUT, and DELETE requests respectively.



