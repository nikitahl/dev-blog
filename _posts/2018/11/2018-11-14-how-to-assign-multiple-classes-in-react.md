---
layout: post
title: How to assign multiple classes to an element in React
description: Examples and explanation of how to assign multiple classes to an element in React
tags: [react, jsx, javascript]
comments: true
---

There are a few ways how to assign multiple classes to an element in React. It can be achieved via an external package or natively.

Depending on your project and requirements you can choose whichever method suits your needs best.

* [using `classNames` package](#classnames-package)
* [natively](#natively)

Let's say we have the following button component.

```jsx
export default class Button extends React.Component {
  render () {
    return <button className='btn'>{this.props.title}</button>
  }
}
```

## classNames package
It's pretty simple:
* [install `classNames`](https://github.com/JedWatson/classnames#classnames){:target="blank"} package if you haven't already.
* Import it to your component
```javascript
import classNames from 'classnames'
```
* Use it like so:
```jsx
export default class Button extends React.Component {
    render () {
      let btnClass = classNames('btn', 'btn-primary')
      return <button className={btnClass}>{this.props.title}</button>
    }
}
```

`classNames` package allows other cool stuff like conditional classes and dynamic class names.
* conditional classes
```jsx
export default class Button extends React.Component {
    render () {
      let btnClass = classNames({
        btn: true,
        'btn-pressed': this.state.isPressed,
        'btn-over': !this.state.isPressed && this.state.isHovered
      })
      return <button className={btnClass}>{this.props.title}</button>
    }
}
```
* dynamic class name
```jsx
let buttonType = 'primary'
classNames({ [`btn-${buttonType}`]: true })
```

## Natively
You can assign multiple classes to an element by using plain old JavaScript. And even imitate `classNames` package.

* multiple classes as a string
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
* multiple classes as an array
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
* multiple classes as an array with condition
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
* dynamic class with multiple classes as an array
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

If you have a complex system you can do lots of cool stuff with that. You can define the classes array outisde of the render function and manipulate it as you want.

So you might not need `classNames` package in the first place unless it's been already used in your project.

---


