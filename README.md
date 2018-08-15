# Vanilla JS vs jQuery

## Events

```javascript
// jQuery
$(document).ready(() => {
  // code
})

// Vanilla
document.addEventListener('DOMContentLoaded', () => {
  // code
})
```

```javascript
// jQuery
$('a').click(() => {
  // code…
})

// Vanilla
[].forEach.call(document.querySelectorAll('a'), (el) => {
  el.addEventListener('click', () => {
    // code…
  })
})
```

## Selectors

```javascript
// jQuery
const divs = $('div')

// Vanilla
const divs = document.querySelectorAll('div')
```

```javascript
// jQuery
const newDiv = $('<div/>')

// Vanilla
const newDiv = document.createElement('div')
```

## Attributes

```javascript
// jQuery
$('img').filter(':first').attr('alt', 'My image')

// Vanilla
document.querySelector('img').setAttribute('alt', 'My image')
```

### Classes

```javascript
// jQuery
newDiv.addClass('foo')

// Vanilla
newDiv.classList.add('foo')
```

```javascript
// jQuery
newDiv.toggleClass('foo')

// Vanilla
newDiv.classList.toggle('foo')
```

## Manipulation

```javascript
// jQuery
$('body').append($('<p/>'))

// Vanilla
document.body.appendChild(document.createElement('p'))
```

```javascript
// jQuery
const clonedElement = $('#about').clone()

// Vanilla
const clonedElement = document.getElementById('about').cloneNode(true)
```

```javascript
// jQuery
$('#wrap').empty()

// Vanilla
const wrap = document.getElementById('wrap')
while(wrap.firstChild) wrap.removeChild(wrap.firstChild)
```

## Transversing

```javascript
// jQuery
const parent = $('#about').parent()

// Vanilla
const parent = document.getElementById('about').parentNode
```

```javascript
// jQuery
if($('#wrap').is(':empty'))

// Vanilla
if(!document.getElementById('wrap').hasChildNodes())
```

```javascript
// jQuery
const nextElement = $('#wrap').next()

// Vanilla
const nextElement = document.getElementById('wrap').nextSibling
```

## AJAX

### GET
```javascript
// jQuery
$.get('//example.com', (data) => {
  // code
})

// Vanilla
const httpRequest = new XMLHttpRequest()
httpRequest.onreadystatechange = (data) => {
  // code
}
httpRequest.open('GET', url)
httpRequest.send()
```

### POST
```javascript
// jQuery
$.post('//example.com', { username: username }, (data) => {
  // code
})

// Vanilla
const httpRequest = new XMLHttpRequest()
httpRequest.onreadystatechange = (data) => {
  // code
}
httpRequest.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
httpRequest.open('POST', url)
httpRequest.send('username=' + encodeURIComponent(username))
```

### JSONP
```javascript
// jQuery
$.getJSON('//openexchangerates.org/latest.json?callback=?', (data) => {
  // code
})

// Vanilla
const success = (data) => {
  // code
}
const scr = document.createElement('script')
scr.src = '//openexchangerates.org/latest.json?callback=formatCurrency'
document.body.appendChild(scr)
```

## EFFECTS
Alternatives:

http://daneden.github.io/animate.css/

https://github.com/visionmedia/move.js/

### Fade In
```javascript
//jQuery
$(el).fadeIn()

// Vanilla, IE8+
const fadeIn = (el) => {
  const opacity = 0

  el.style.opacity = 0
  el.style.filter = ''

  const last = +new Date()
  const tick = () => {
    opacity += (new Date() - last) / 400
    el.style.opacity = opacity
    el.style.filter = 'alpha(opacity=' + (100 * opacity)|0 + ')'

    last = +new Date()

    if (opacity &lt; 1) {
      (window.requestAnimationFrame && requestAnimationFrame(tick)) || setTimeout(tick, 16);
    }
  }

  tick()
}

fadeIn(el)

// Vanilla, IE9+
const fadeIn = (el) => {
  el.style.opacity = 0

  const last = +new Date()
  const tick = () => {
    el.style.opacity = +el.style.opacity + (new Date() - last) / 400
    last = +new Date()

    if (+el.style.opacity &lt; 1) {
      (window.requestAnimationFrame && requestAnimationFrame(tick)) || setTimeout(tick, 16)
    }
  }

  tick()
}

fadeIn(el)

// Vanilla, IE10+
el.classList.add('show')
el.classList.remove('hide')
```

```css
/* CSS */
.show {
  transition: opacity 400ms
}
.hide {
  opacity: 0
}
```
#### Hide
```javascript
//jQuery
$(el).hide()

// Vanilla IE8+
el.style.display = 'none'
```
#### Show
```javascript
//jQuery
$(el).show()

// Vanilla, IE8+
el.style.display = ''
```
