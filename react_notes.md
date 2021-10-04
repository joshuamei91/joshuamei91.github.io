---
layout: page
title: System Design
permalink: /react/
---

- [Higher Order Components](https://reactjs.org/docs/higher-order-components.html): function that usually contains reusable logic (eg. fetching data) and takes in a child component as one of its arguments and returns a new component. ie. it transform a component into another component

- [Render Props](https://reactjs.org/docs/render-props.html): A render prop is a function prop that a component uses to know what to render. Used to dynamically determine what to render.
  ``` jsx
  <DataProvider render={data => (
    <h1>Hello {data.target}</h1>
  )}/>
  ```