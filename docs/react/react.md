---
layout: default
title: React
nav_order: 2
permalink: docs/react
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


React is a front-end and open-source JavaScript library which is useful in developing user interfaces specifically for applications with a single page. It is helpful in building complex and reusable user interface(UI) components of mobile and web applications as it follows the component-based approach.

The important features of React are:

It supports server-side rendering.
It will make use of the virtual DOM rather than real DOM (Data Object Model) as RealDOM manipulations are expensive.
It follows unidirectional data binding or data flow.
It uses reusable or composable UI components for developing the view.

---

## Features of React:

 It uses **VirtualDOM** instead of RealDOM considering that RealDOM manipulations are expensive.
 Supports **server-side rendering**.
 Follows **Unidirectional** data flow or data binding.
 Uses **reusable/composable** UI components to develop the view.

###  Advantages of using React

- Use of Virtual DOM to improve efficiency:
React uses virtual DOM to render the view. As the name suggests, virtual DOM is a virtual representation of the real DOM. Each time the data changes in a react app, a new virtual DOM gets created. Creating a virtual DOM is much faster than rendering the UI inside the browser. Therefore, with the use of virtual DOM, the efficiency of the app improves.

- Gentle learning curve: 
React has a gentle learning curve when compared to frameworks like Angular. Anyone with little knowledge of javascript can start building web applications using React.

- SEO friendly: 
React allows developers to develop engaging user interfaces that can be easily navigated in various search engines. It also allows server-side rendering, which boosts the SEO of an app.

- Reusable components: 
React uses component-based architecture for developing applications. Components are independent and reusable bits of code. These components can be shared across various applications having similar functionality. The re-use of components increases the pace of development.

- Huge ecosystem of libraries to choose from: 
React provides you with the freedom to choose the tools, libraries, and architecture for developing an application based on your requirement.

###  Disadvantages or limitations of React

The few limitations of React are as given below:

React is not a full-blown framework as it is only a library.
The components of React are numerous and will take time to fully grasp the benefits of all.
It might be difficult for beginner programmers to understand React.
Coding might become complex as it will make use of inline templating and JSX.
 
###  JSX - JavaScript XML

JSX stands for JavaScript XML. It allows us to write HTML inside JavaScript and place them in the DOM without using functions like appendChild( ) or createElement( ).

As stated in the official docs of React, JSX provides syntactic sugar for React.createElement( ) function.

> Note- We can create react applications without using JSX as well.

Let’s understand how JSX works:

Without using JSX, we would have to create an element by the following process:

```jsx
const text = React.createElement('p', {}, 'This is a text');
const container = React.createElement('div','{}',text );
ReactDOM.render(container,rootElement);
 ```

Using JSX, the above code can be simplified:



```jsx
const container = (
<div>
  <p>This is a text</p>
</div>
);
ReactDOM.render(container,rootElement);
```

As one can see in the code above, we are directly using HTML inside JavaScript.



---

## Virtual DOM

The Virtual DOM (VDOM) is an in-memory representation of Real DOM. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called reconciliation.

The *Virtual DOM* works in three simple steps.

1. Whenever any underlying data changes, the entire UI is re-rendered in Virtual DOM representation.

<img src="react/images/vdom1.png" width="700"/>

2. Then the difference between the previous DOM representation and the new one is calculated.

<img src="react/images/vdom2.png" width="700"/>

3. Once the calculations are done, the real DOM will be updated with only the things that have actually changed.

<img src="react/images/vdom3.png" width="500"/>


> As stated by the react team, virtual DOM is a concept where a virtual representation of the real DOM is kept inside the memory and is synced with the real DOM by a library such as ReactDOM.

<img src="react/images/vdom4.png" width="500"/>


### Why was virtual DOM introduced?

DOM manipulation is an integral part of any web application, but DOM manipulation is quite slow when compared to other operations in JavaScript. The efficiency of the application gets affected when several DOM manipulations are being done. Most JavaScript frameworks update the entire DOM even when a small part of the DOM changes.

For example, consider a list that is being rendered inside the DOM. If one of the items in the list changes, the entire list gets rendered again instead of just rendering the item that was changed/updated. This is called inefficient updating.

To address the problem of inefficient updating, the react team introduced the concept of virtual DOM.

<img src="react/images/vdom5.png" width="500"/>

For every DOM object, there is a corresponding virtual DOM object(copy), which has the same properties. The main difference between the real DOM object and the virtual DOM object is that any changes in the virtual DOM object will not reflect on the screen directly. Consider a virtual DOM object as a blueprint of the real DOM object. Whenever a JSX element gets rendered, every virtual DOM object gets updated.

> Note- One may think updating every virtual DOM object might be inefficient, but that’s not the case. Updating the virtual DOM is much faster than updating the real DOM since we are just updating the blueprint of the real DOM.

React uses two virtual DOMs to render the user interface. One of them is used to store the current state of the objects and the other to store the previous state of the objects. Whenever the virtual DOM gets updated, react compares the two virtual DOMs and gets to know about which virtual DOM objects were updated. After knowing which objects were updated, react renders only those objects inside the real DOM instead of rendering the complete real DOM. This way, with the use of virtual DOM, react solves the problem of inefficient updating.




---













