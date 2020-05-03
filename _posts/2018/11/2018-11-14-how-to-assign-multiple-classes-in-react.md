---
layout: post
title: How to assign multiple class names to an element in React
description: The complete guide on how to assign multiple class names to an element in React with examples and explanation
tags: [react, jsx, javascript]
comments: true
---

There are a few ways how to assign multiple classes to an element in React. It can be achieved via an external package or via Vanilla JavaScript.

Depending on your project and requirements you can choose whichever method suits your needs best.

1. [using `classNames` package](#1-classnames-package)
2. [using Vanilla JavaScript](#2-vanilla-javascript)

Let's say we have the following button component.

**React Class:**
```jsx
export default class Button extends React.Component {
  render () {
    return <button className='btn'>{this.props.title}</button>
  }
}
```

**React Hooks:**
```jsx
export function Button (props) {
  return <button className='btn'>{props.title}</button>
}
```

## 1. `classNames` package

It's pretty simple:
* [install `classNames`](https://github.com/JedWatson/classnames#classnames){:target="blank"} package if you haven't already.
* Import it to your component
```javascript
import classNames from 'classnames'
```
* Use it like so:
**React Class:**
```jsx
export default class Button extends React.Component {
    render () {
      const btnClass = classNames('btn', 'btn-primary')
      return <button className={btnClass}>{this.props.title}</button>
    }
}
```
**React Hooks:**
```jsx
export function Button (props) {
    const btnClass = classNames('btn', 'btn-primary')
    return <button className={btnClass}>{props.title}</button>
}
```

`classNames` package allows other cool stuff like conditional classes and dynamic class names.

### Conditional classes

**React Class:**
```jsx
export default class Button extends React.Component {
  render () {
    let btnClass = classNames({
      'btn': true,
      'btn-pressed': this.state.isPressed,
      'btn-over': !this.state.isPressed && this.state.isHovered
    })
    return <button className={btnClass}>{this.props.title}</button>
  }
}
```
**React Hooks:**
```jsx
export function Button (props) {
  const [isPressed, setPressed] = useState(false)
  const [isHovered, setHovered] = useState(false)

  const btnClass = classNames({
    'btn': true,
    'btn-pressed': isPressed,
    'btn-over': !isPressed && isHovered
  })
  return <button className={btnClass}>{props.title}</button>
}
```
### Dynamic class name

```jsx
const buttonType = 'primary'
classNames({ [`btn-${buttonType}`]: true })
```

## 2. Vanilla JavaScript

You can assign multiple class names to an element by using plain old JavaScript. And even imitate some of the `classNames` package functionality.

### Multiple class names as a string

**React Class:**
```jsx
export default class Button extends React.Component {
  render () {
    let btnClass = 'btn'
    if (this.state.isPressed) {
      btnClass += ' btn-pressed'
    }
    return <button className={btnClass}>{this.props.title}</button>
  }
}
```
**React Hooks:**
```jsx
export function Button (props) {
  const [isPressed, setPressed] = useState(false)

  let btnClass = 'btn'
  if (isPressed) {
    btnClass += ' btn-pressed'
  }
  return <button className={btnClass}>{props.title}</button>
}
```

### Multiple class names as an array

**React Class:**
```jsx
export default class Button extends React.Component {
  render () {
    let btnClass = [
      'btn',
      'btn-primary',
      'btn-info'
    ]
    btnClass = btnClass.join(' ')
    return <button className={btnClass}>{this.props.title}</button>
  }
}
```
**React Hooks:**
```jsx
export function Button (props) {
  let btnClass = [
    'btn',
    'btn-primary',
    'btn-info'
  ]
  btnClass = btnClass.join(' ')
  return <button className={btnClass}>{props.title}</button>
}
```
### Multiple class names as an array with condition

**React Class:**
```jsx
export default class Button extends React.Component {
  render () {
    let btnClass = [
      'btn',
      this.state.isPressed ? 'btn-pressed' : '',
      !this.state.isPressed && this.state.isHovered ? 'btn-over' : ''
    ]
    btnClass = btnClass.join(' ')
    return <button className={btnClass}>{this.props.title}</button>
  }
}
```
**React Hooks:**
```jsx
export function Button (props) {
  const [isPressed, setPressed] = useState(false)
  const [isHovered, setHovered] = useState(false)
  let btnClass = [
    'btn',
    isPressed ? 'btn-pressed' : '',
    !isPressed && isHovered ? 'btn-over' : ''
  ]
  btnClass = btnClass.join(' ')
  return <button className={btnClass}>{props.title}</button>
}
```
### Dynamic class with multiple classes as an array **React Class:**
```jsx
export default class Button extends React.Component {
  render () {
    let buttonType = 'primary'
    let btnClass = [
      'btn',
      `btn-${buttonType}`
    ]

    btnClass = btnClass.join(' ')
    return <button className={btnClass}>{this.props.title}</button>
  }
}
```
**React Hooks:**
```jsx
export function Button (props) {
  let buttonType = 'primary'
  let btnClass = [
    'btn',
    `btn-${buttonType}`
  ]

  btnClass = btnClass.join(' ')
  return <button className={btnClass}>{props.title}</button>
}
```

If you have a complex system you can do lots of cool stuff with that. You can define the classes array outisde of the render function and manipulate it as you want.

So you might not need `classNames` package in the first place unless it's been already used in your project.


