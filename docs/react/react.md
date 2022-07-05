---
layout: default
title: React
nav_order: 2
permalink: docs/kafka
resource: true
desc: "React interview questions and answers."
categories: [React]
---

# React
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


React is an **open-source front-end JavaScript library** that is used for building user interfaces, especially for single-page applications. 
It is used for handling view layer for web and mobile apps. 

React was created by [Jordan Walke](https://github.com/jordwalke), a software engineer working for Facebook. React was first deployed on Facebook's News Feed in 2011 and on Instagram in 2012.


---

## Features of React:

 It uses **VirtualDOM** instead of RealDOM considering that RealDOM manipulations are expensive.
 Supports **server-side rendering**.
 Follows **Unidirectional** data flow or data binding.
 Uses **reusable/composable** UI components to develop the view.


###  JSX - JavaScript XML


*JSX* is a XML-like syntax extension to ECMAScript (the acronym stands for *JavaScript XML*). Basically it just provides syntactic sugar for the `React.createElement()` function, giving us expressiveness of JavaScript along with HTML like template syntax.

In the example below text inside `<h1>` tag is returned as JavaScript function to the render function.

```jsx harmony
    class App extends React.Component {
      render() {
        return(
          <div>
            <h1>{'Welcome to React world!'}</h1>
          </div>
        )
      }
    }
 ```


---

## Virtual DOM

The Virtual DOM (VDOM) is an in-memory representation of Real DOM. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called reconciliation.

The *Virtual DOM* works in three simple steps.

1. Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.

<img src="images/vdom1.png" width="700"/>

2. Then the difference between the previous DOM representation and the new one is calculated.

<img src="images/vdom2.png" width="700"/>

3. Once the calculations are done, the real DOM will be updated with only the things that have actually changed.

<img src="images/vdom3.png" width="500"/>




---













