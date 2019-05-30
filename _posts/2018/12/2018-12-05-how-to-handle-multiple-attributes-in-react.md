---
layout: post
title: How to handle multiple attributes in ReactJS
description: Handle multiple HTML attributes on an element with ease in ReactJS
tags: [react, jsx, javascript]
comments: true
---

Have you ever had a situation when your JSX code is cluttered with multiple attributes?
If you have, there is a simple solution to handle this situation.

Suppose you have a component that has an input element. The `render` method could look something like this:

```jsx
render () {
  return <div className='form-field'>
    <label className='form-label' htmlFor='user-email'>Email: </label>
    <input className='form-input form-input--email' id='user-email' type='email' name='user-email' placeholder={this.props.placeholder} required>
  </div>	
}
```

As you can see there are quite a few attributes applied to the `input` element already.

You can store all of the attributes in an object and use **Spread syntax** on the element to assign them.

```jsx
render () {
  const attributes = {
    className: 'form-input form-input--email',
    id: 'user-email',
    type: 'email',
    name: 'user-email',
    placeholder: this.props.placeholder,
    required: this.state.required
  }
  return <div className='form-field'>
    <label className='form-label' htmlFor='user-email'>Email: </label>
    <input {...attributes}>
  </div>	
}
```
As you can see now your code looks more structured. This way you'll avoid excessive amount of inline attributes on an element and keep your code clean, readable and easy to maintain.

To take it even further you can also assign values based on a condition.
```jsx
render () {
  const attributes = {
    className: 'form-input form-input--email',
    id: 'user-email',
    type: 'email',
    name: 'user-email',
    placeholder: this.props.placeholder || '',
    required: this.state.required
  }
  return <div className='form-field'>
    <label className='form-label' htmlFor='user-email'>Email: </label>
    <input {...attributes}>
  </div>	
}
```

You can also add multiple inline styles.
```jsx
render () {
  const attributes = {
    className: 'form-input form-input--email',
    id: 'user-email',
    type: 'email',
    name: 'user-email',
    placeholder: this.props.placeholder || '',
    required: this.state.required,
    style: {
    	borderRadius: '3px',
    	color: '#3e3e3e'
    }
  }
  return <div className='form-field'>
    <label className='form-label' htmlFor='user-email'>Email: </label>
    <input {...attributes}>
  </div>	
}
```

The best thing about it, that you can split your code into small bits and then combine them all together. Like adding multiple classes. Learn how to [add multiple classes in React](http://nikitahl.com/how-to-assign-multiple-classes-in-react) in my article.
```jsx
render () {
  const inputClasses = [
    'form-input',
    'form-input--email'
  ]
  const inputStyles = {
    borderRadius: '3px',
    color: '#3e3e3e'
  }
  const attributes = {
    className: inputClasses.join(' '),
    id: 'user-email',
    type: 'email',
    name: 'user-email',
    placeholder: this.props.placeholder || '',
    required: this.state.required,
    style: inputStyles
  }
  return <div className='form-field'>
    <label className='form-label' htmlFor='user-email'>Email: </label>
    <input {...attributes}>
  </div>	
}
```

However there are exceptions. Some attributes that cannot be defined within an `attributes` object. These are:
* `data-*`
* `aria-*`

To add these kind of attributes to your `attributes` object use brackets notation.

```
attributes['data-validate'] = true
attributes['aria-label'] = 'User email'
```



