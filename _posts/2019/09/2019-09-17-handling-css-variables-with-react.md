---
layout: post
title: Handling CSS variables (Custom Properties) in React
description: In this article, I'll explain how to handle (update) CSS variables in React.
tags: [css, react]
comments: true
---

In this article, I'll explain how to handle (update) CSS variables in React. I'll give you the concept for both Class components approach and Hooks approach.

[CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties){:target="blank"} or variables are a great way to update styles in your app without using pre or post processors or creating additional CSS classes.

A quick reminder on the browser support for the CSS Variables:
<p class="ciu_embed" data-feature="css-variables" data-periods="future_1,current,past_1" data-accessible-colours="false">
<a href="https://caniuse.com/#feat=css-variables">Can I Use CSS Variables (Custom Proprties)?</a> Data on support for the CSS Variables (Custom Properties) feature across the major browsers from caniuse.com.
</p>

In this example, I'll be using a simple button component with an `onCLick` event which will change `background-color` and `color` properties of the button, just for the sake of demonstration.

## Markup
For the markup, we'll be using a `button` element inside a `div` container. The `.container` will store the CSS variables for the button.

```html
<div class="container">
  <button className="btn">Click me!</button>
</div>
```
**NOTE:** The reason we've wrapped button inside a container is that there might be other elements and storing CSS variables on the container will scope them only for the child elements of this container.

## Style
Let's define the initial CSS variables on the `.container` element and use them on the `button`.
```css
.container {
  --btn-bg-color: #ff9900;
  --btn-color: #1780cc;
}

.btn {
  background-color: var(--btn-bg-color);
  color: var(--btn-color);
  
  padding: 15px 30px;
  border: none;
  cursor: pointer;
}
```
Now for the React part. Conceptually Class and Hooks approaches are very similar, we'll go through each one of them step by step.

## 1. React Class component approach

Let's create a React class and name it `ButtonClassComponent`.
```jsx
class ButtonClassComponent extends React.Component {

}
```

Then we'll define the default state in the `constructor` method. The state will hold only one property `isClicked`.
```jsx
constructor (props) {
  super(props)
  this.state = {
    isClicked: false
  }
}
```

Next, we'll create a `render` method. As you can see, now it just returns the markup like above.
```jsx
render () {
  let btnText = 'Click me!'

  return (
    <div className='container'>
      <button className='btn'>
        {btnText}
      </button>
    </div>
  )
}
```

Then let's create a `cssProperties` object inside `render` method and assign this object to a `style` attribute. This way CSS variables and other CSS properties will be assigned to a `.container` element if exists.
```jsx
render () {
  let cssProperties = {}
  let btnText = 'Click me!'

  return (
    <div className='container' style={cssProperties}>
      <button className='btn'>
        {btnText}
      </button>
    </div>
  )
}
```

Finally let's add an `onClick` event to a `button` element. The handler will be a `this.setState` method call.
And also let's add a condition where we check if the button was clicked. If so, we'll assign properties to a `cssProperties` object and change button text.

```jsx
render () {
  let cssProperties = {}
  let btnText = 'Click me!'
  if (this.state.isClicked) {
    btnText = 'Hello World!'
    cssProperties['--btn-bg-color'] = '#1780cc'
    cssProperties['--btn-color'] = '#ff9900'
  }

  return (
    <div className='container' style={cssProperties}>
      <button className='btn' onClick={() => { this.setState({ isClicked: !this.state.isClicked }) }}>
        {btnText}
      </button>
    </div>
  )
}
```

Final React class component should look like this:

```jsx
class ButtonClassComponent extends React.Component {
  constructor (props) {
    super(props)
    this.state = {
      isClicked: false
    }
  }
  
  render () {
    let cssProperties = {}
    let btnText = 'Click me!'
    if (this.state.isClicked) {
      btnText = 'Hello World!'
      cssProperties['--btn-bg-color'] = '#1780cc'
      cssProperties['--btn-color'] = '#ff9900'
    }

    return (
      <div className='container' style={cssProperties}>
        <button className='btn' onClick={() => { this.setState({ isClicked: !this.state.isClicked }) }}>
          {btnText}
        </button>
      </div>
    )
  }
}
```

## 2. React Hooks approach

This is very similar to a Class component. For the Hooks approach, let's create a function, and name it `ButtonHooksComponent`.

```jsx
function ButtonHooksComponent () {

}
```

This function will return the known markup.

```jsx
function ButtonHooksComponent () {
  let cssProperties = {}
  let btnText = 'Click me!'
  return (
    <div className='container' style={cssProperties}>
      <button className='btn'>
        {btnText}
      </button>
    </div>
  )
}
```

Assuming you've already imported `useState` hook, we'll add a default state.
```jsx
function ButtonHooksComponent () {
  const [ isClicked, setIsClicked ] = useState(false)

  let cssProperties = {}
  let btnText = 'Click me!'
  return (
    <div className='container' style={cssProperties}>
      <button className='btn'>
        {btnText}
      </button>
    </div>
  )
}
```

Finally let's add an `onClick` event and a condition like in the class component.

```jsx
function ButtonHooksComponent () {
  const [ isClicked, setIsClicked ] = useState(false)
  
  let cssProperties = {}
  let btnText = 'Click me!'
  if (isClicked) {
    btnText = 'Hello World!'
    cssProperties['--btn-bg-color'] = '#1780cc'
    cssProperties['--btn-color'] = '#ff9900'
  }
 
  return (
    <div className='container' style={cssProperties}>
      <button className='btn' onClick={() => {setIsClicked(!isClicked)}}>
        {btnText}
      </button>
    </div>
  )
}
```

That's it!

So the main concept is to set the desired CSS properties to an object conditionally and then assign this object to a `style` attribute of an element.

You can check the end result and whole code on [CodePen](https://codepen.io/nikitahl/pen/gOYdayy/){:target="blank"}:
<p class="codepen" data-height="360" data-theme-id="0" data-default-tab="js,result" data-user="nikitahl" data-slug-hash="gOYdayy" style="height: 360px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="gOYdayy">
  <span>See the Pen <a href="https://codepen.io/nikitahl/pen/gOYdayy/">
  gOYdayy</a> by Nikita Hlopov (<a href="https://codepen.io/nikitahl">@nikitahl</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<script src="https://cdn.jsdelivr.net/gh/ireade/caniuse-embed/caniuse-embed.min.js"></script>