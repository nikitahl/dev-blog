---
layout: post
title: Positioning content inside a flexbox container with CSS
description: CSS flexbox property allows simple and diverse ways for positioning content inside a container
tags: [css]
comments: true
---

This article will cover the approach that uses CSS flexbox property for positioning a content inside a container element.

Before we dive in I want to specify that the content might be another element or content as it is e.g. text. I'll provide examples for both.

**Note: The following examples are going to feature a single element inside a flexbox container, for the sake of demonstrating the positioning capabilities of a flexbox property.**

Flexbox property allows you to set content in 9 main positions:

1. Top Left;
2. Top Center;
3. Top Right;
4. Center Left;
5. Center Center;
6. Center Right;
7. Bottom Left;
8. Bottom Center;
9. Bottom Right.

**Note: The amount of values of CSS flexbox related properties allows to set more than 9 positions. I'm just going to cover 9 most popular ones!**

<style type="text/css">
  .content-container {
    background: lightgreen
  }
  .content-container span {
    background: lightcoral
  }
  .content-container-flex {
    height: 100px;
    display: flex;
    flex-direction: row
  }
  .content-container-top-left {
    justify-content: flex-start;
    align-items: flex-start
  }
  .content-container-top-center {
    justify-content: center;
    align-items: flex-start
  }
  .content-container-top-right {
    justify-content: flex-end;
    align-items: flex-start
  }
  .content-container-center-left {
    justify-content: flex-start;
    align-items: center
  }
  .content-container-center-center {
    justify-content: center;
    align-items: center
  }
  .content-container-center-right {
    justify-content: flex-end;
    align-items: center
  }
  .content-container-bottom-left {
    justify-content: flex-start;
    align-items: flex-end
  }
  .content-container-bottom-center {
    justify-content: center;
    align-items: flex-end
  }
  .content-container-bottom-right {
    justify-content: flex-end;
    align-items: flex-end
  }
  .button-container {
    border: none;
    border-radius: 0;
    padding: 0;
    background: deeppink;
    color: white;
    font-size: 16px;
    cursor: pointer
  }
  .button-container-flex {
    width: 140px;
    height: 45px;
    display: inline-flex;
    flex-direction: column
  }
  .button-container-top-left {
    justify-content: flex-start;
    align-items: flex-start
  }
  .button-container-top-center {
    justify-content: flex-start;
    align-items: center
  }
  .button-container-top-right {
    justify-content: flex-start;
    align-items: flex-end
  }
  .button-container-center-left {
    justify-content: center;
    align-items: flex-start
  }
  .button-container-center-center {
    justify-content: center;
    align-items: center
  }
  .button-container-center-right {
    justify-content: center;
    align-items: flex-end
  }
  .button-container-bottom-left {
    justify-content: flex-end;
    align-items: flex-start
  }
  .button-container-bottom-center {
    justify-content: flex-end;
    align-items: center
  }
  .button-container-bottom-right {
    justify-content: flex-end;
    align-items: flex-end
  }
</style>

## Container with a content element

To start off, the HTML is the basic container with a content element inside:

```html
<div class="content-container">
  <span>Element with text content</span>
</div>
```
To give some visual aid let's add some basic CSS:

```css
.content-container {
  background: lightgreen;
}

.content-container span {
  background: lightcoral;
}
```

Result:

<div class="content-container">
  <span>Element with text content</span>
</div>

In order to set content in all 9 positions, a content container must have a `width` and `height` property greater than the content itself.

The `width` by default is equal to 100% if the container's `display` property is set to `flex`. The `height`, however, is dependent either on the content's `height`(some of the items might be higher than others) or it can be set manually.

The `flex-direction` property is optional, however, it might affect the further positioning of the content.

<blockquote>
The <code>flex-direction</code> CSS property sets how flex items are placed in the flex container defining the main axis and the direction
<br />
&mdash;<cite><a href="https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction" target="_blank">MDN</a></cite>
</blockquote>

CSS:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
}
```

Result:
<div class="content-container content-container-flex">
  <span>Element with text content</span>
</div>

For the `flex-direction: row` the horizontal positioning is set with `justify-content` property.

For the `flex-direction: row` the vertical positioning is set with `align-items` property.

For the `flex-direction: column` the horizontal positioning is set with `align-items` property.

For the `flex-direction: column` the vertical positioning is set with `justify-content` property.

The values for the `justify-content` and `align-items` properties are the same:

* `flex-start` - for horizontal it's left, for vertical it's top;
* `center` - for horizontal it's center, for vertical it's center;
* `flex-end` - for horizontal it's right, for vertical it's bottom.

### *Top Left* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: flex-start; /* horizontal position */
  align-items: flex-start; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-top-left">
  <span>Element with text content</span>
</div>

### *Top Center* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: center; /* horizontal position */
  align-items: flex-start; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-top-center">
  <span>Element with text content</span>
</div>

### *Top Right* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: flex-end; /* horizontal position */
  align-items: flex-start; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-top-right">
  <span>Element with text content</span>
</div>

### *Center Left* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: flex-start; /* horizontal position */
  align-items: center; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-center-left">
  <span>Element with text content</span>
</div>

### *Center Center* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: center; /* horizontal position */
  align-items: center; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-center-center">
  <span>Element with text content</span>
</div>

### *Center Right* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: flex-end; /* horizontal position */
  align-items: center; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-center-right">
  <span>Element with text content</span>
</div>

### *Bottom Left* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: flex-start; /* horizontal position */
  align-items: flex-end; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-bottom-left">
  <span>Element with text content</span>
</div>

### *Bottom Center* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: center; /* horizontal position */
  align-items: flex-end; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-bottom-center">
  <span>Element with text content</span>
</div>

### *Bottom Right* position:
```css
.content-container {
  background: lightgreen;
  height: 100px;
  display: flex;
  flex-direction: row;
  justify-content: flex-end; /* horizontal position */
  align-items: flex-end; /* vertical position */
}
```

Result:
<div class="content-container content-container-flex content-container-bottom-right">
  <span>Element with text content</span>
</div>


## Container with a pure content (text)

This time the container element will contain pure content (text):

```html
<button class="button-container">Hello World</button>
```
Again to give some visual aid let's add some basic CSS:

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  cursor: pointer;
}
```

Result:

<button class="button-container">Hello World</button>

Because we use the `button` element for this example, I'm going to set the `display` property to `inline-flex` value. As well as set the `flex-direction` property with a value of `column` which will allow to position content vertically.

Also since the button is stripped out of the default styles, its size is matching its content, so I'll add a `width` and `height` properties to give some room for the content.

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;
}
```

Result:

<button class="button-container button-container-flex">Hello World</button>

### Button content *Top Left* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: flex-start; /* vertical position */
  align-items: flex-start; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-top-left">Hello World</button>


### Button content *Top Center* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: flex-start; /* vertical position */
  align-items: center; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-top-center">Hello World</button>


### Button content *Top Right* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: flex-start; /* vertical position */
  align-items: flex-end; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-top-right">Hello World</button>


### Button content *Center Left* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: center; /* vertical position */
  align-items: flex-start; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-center-left">Hello World</button>


### Button content *Center Center* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: center; /* vertical position */
  align-items: center; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-center-center">Hello World</button>


### Button content *Center Right* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: center; /* vertical position */
  align-items: flex-end; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-center-right">Hello World</button>


### Button content *Bottom Left* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: flex-end; /* vertical position */
  align-items: flex-start; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-bottom-left">Hello World</button>


### Button content *Bottom Center* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: flex-end; /* vertical position */
  align-items: center; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-bottom-center">Hello World</button>


### Button content *Bottom Right* position: 

```css
.button-container {
  border: none;
  border-radius: 0;
  padding: 0;
  background: deeppink;
  color: white;
  font-size: 16px;
  
  width: 140px;
  height: 45px;

  display: inline-flex;
  flex-direction: column;

  justify-content: flex-end; /* vertical position */
  align-items: flex-end; /* horizontal position */
}
```

Result:

<button class="button-container button-container-flex button-container-bottom-right">Hello World</button>

---