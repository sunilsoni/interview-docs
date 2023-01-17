---
layout: default
title: Pipes
parent: Angular
resource: true
desc: "Angular Pipes interview questions and answers."
categories: [Angular Pipes]
---

# Angular Pipes
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

Angular Pipes are used to transform data on a template, without writing a boilerplate code in a component.

A pipe takes in data as input and transforms it to the desired output. It is like a filter in Angular 1 (AngularJS).

Generally, If we need to transform data, we write the code in the component, For example, we want to transform today’s date into a format like `'16 Apr 2018'` or `'16-04-2018'`
,We need to write separate code in the component.

So instead of writing separate boilerplate code, we can use the built-in pipe called `DatePipe` which will take input and transform it into the desired date format.

---

##  Syntax to use Pipes in Angular Application

<img src="images/anular-pipes.png" width="600"/>


A pipe takes in data as input and transforms it to a desired output. For example, let us take a pipe to transform a component birthday property into a human-friendly date using date pipe.


---

##  Angular Pipes

https://github.com/sunilsoni/interview-notes/blob/main/angular/angular-pipes.md

---

## what is pure vs impure pipes angular?

In Angular, pipes are a way to transform data in a template. Pipes take an input value and return a transformed output value.

There are two types of pipes in Angular: **pure** and **impure**.

A pure pipe is a pipe that only runs when one of the following is true:

* The input value to the pipe is different from the previous input value.

* The pipe is marked as pure and the component that contains the pipe is being destroyed.


* A `pure pipe` is efficient because it only runs when it needs to, which can improve the performance of your application.

* An `impure pipe` is a pipe that runs on every change detection cycle, regardless of whether the input value has changed.

* A pure pipe is the default in Angular, and the pipe is marked as pure by default. You can mark a pipe as impure by setting the `pure` property of the `@Pipe` decorator to `false`.

**An example of a pure pipe:**

```log
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filter',
  pure: true
})
export class FilterPipe implements PipeTransform {
  transform(value: any, filterString: string, propName: string): any {
    if (value.length === 0 || filterString === '') {
      return value;
    }
    const resultArray = [];
    for (const item of value) {
      if (item[propName] === filterString) {
        resultArray.push(item);
      }
    }
    return resultArray;
  }
}

```
* In this example, the `FilterPipe` is a pure pipe, it only runs when the input value or filterString changes.

**An example of an impure pipe:**

```log
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'random',
  pure: false
})
export class RandomPipe implements PipeTransform {
  transform(value: any): any {
    return value[Math.floor(Math.random() * value.length)];
  }
}

```
* In this example, the `RandomPipe` is an impure pipe, it runs on every change detection cycle, regardless of whether the input value has changed.

In summary, pure pipes are efficient because they only run when they need to, while impure pipes run on every change detection cycle. By default, pipes are pure, but you can mark a pipe as impure by setting the pure property of the `@Pipe` decorator to `false`.

---