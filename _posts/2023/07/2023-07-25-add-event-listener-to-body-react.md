---
layout: post
permalink: add-event-listener-to-body-react
title: How to add event listener to body in React
date: 2023-07-26T04:14:01.121Z
description: In certain cases, you'll need to add a custom event listener to a `body` element in React. In this article, I'm going to explain a few ways how you can handle such cases.
tags: [react]
---

In certain cases, you'll need to add a custom event listener to a `body` element in React. In this article, I'm going to explain a few ways how you can handle such cases.

Before we move on, let's identify the problem. Say, you have a sidebar that slides into view from outside of the screen or you have a modal opened.

In this case, you want to let users close it by clicking on the "body", or outside of the active element.

So there can be two possibilities for how to apply a custom event to a `body` element.

1. Assign event listener as a side effect for a component
2. Assign the event listener to a React event handler e.g. click

## Event listener as a side effect

One way to add a custom event to the `body` element is to specify it inside the component's lifecycle, hence `useEffect` hook or `componentDidMount` method.

This is a good approach when the element is rendered conditionally and the event is needed only when the component exists in the DOM.

### Hooks component

For the Hooks component specify the event listener method inside the [`useEffect` hook](https://react.dev/reference/react/useEffect){:target="_blank"}.

```javascript
const handleBodyClick = () => {
  console.log('click')
}

useEffect(() => {
  document.body.addEventListener('click', handleBodyClick)

  return () => {
    document.body.removeEventListener('click', handleBodyClick)
  }
})
```

<p class="note">💡 NOTE: Make sure to specify the <code>return</code> statement to remove the event listener when a component is removed from the DOM.</p>

### Class component

Similarly, you can add an event listener inside the [Class component](https://react.dev/reference/react/Component#defining-a-class-component){:target="_blank"}.

Use the `componentDidMount` method to add the event listener and `componentWillUnmount` to remove the event listener when component is removed from the DOM.


```javascript
componentDidMount () {
  document.body.addEventListener('click', this.handleBodyClick)
}

componentWillUnmount () {
  document.body.removeEventListener('click', this.handleBodyClick)
}

handleBodyClick () {
  console.log('click')
}
```

<p class="note">💡 NOTE: Make sure you bind the event handler method to a <a href="https://react.dev/reference/react/Component#constructor" target="_blank">class instance</a>.</p>

## Custom event inside an event handler

In case you want to listen for an event onhe t `body` element when no additional components are rendered you can do that inside one of the component's event handlers.

Say you want to only listen for an event when another event had occurred, like a click.

In this case, you specify the event listener inside the component's event handler function.

Have a look at the following component which has an `onClick` event handler, and inside of it a state set.

```javascript
function Button () {
  const [isActive, setIsActive] = useState(false)

  const handleButtonClick = () => {
    setIsActive(!isActive)
  }

  return (
    <button onClick={handleButtonClick}>
      Apply here
    </button> 
  )
}
```

Now inside the `handleButtonClick` event handler function, we can add or remove an event listener for the `body` element based on the state of the component.

<style>.err{visibility:hidden}.highlight .sr{color:inherit}</style>


```javascript
function Button () {
  const [isActive, setIsActive] = useState(false)

  const handleBodyClick = () => {
    console.log('click')
  }

  const handleButtonClick = () => {
    setIsActive(!isActive)

    if (isActive) {
      document.body.addEventListener('click', handleBodyClick)
    } else {
      document.body.removeEventListener('click', handleBodyClick)
    }
  }

  return (
    <button onClick={handleButtonClick}>
      Apply here
    </button> 
  )
}
```

## Conclusion

You can use these approaches to set event listeners for various HTML elements, not only `body`, as well as to perform specific actions like fetching data or other side effects.

Keep in mind to always perform a cleanup e.g. remove event listeners to avoid memory leaks.