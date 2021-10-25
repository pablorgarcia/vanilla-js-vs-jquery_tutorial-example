# Vanilla JS vs jQuery Tutorial example

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

    if (opacity < 1) {
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

    if (+el.style.opacity < 1) {
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
### Hide
```javascript
//jQuery
$(el).hide()

// Vanilla IE8+
el.style.display = 'none'
```
### Show
```javascript
//jQuery
$(el).show()

// Vanilla, IE8+
el.style.display = ''
```

## Utils

### Bind
```javascript
// jQuery
$.proxy(fn, context)

// Vanilla, IE8+
fn.apply(context, arguments)

// Vanilla, IE9+
fn.bind(context)
```

### Array Each
```javascript
// jQuery
$.each(array, (i, item) => {
  // Code
})

// Vanilla, IE8+
const forEach = (array, fn) => {
  for (var i = 0; i < array.length; i++)
    fn(array[i], i)
}

forEach(array, (item, i) => {
  // Code
})

// Vanilla, IE9+
array.forEach((item, i) => {
  // Code
})
```

### Deep Extend
```javascript
//jQuery
$.extend(true, {}, objA, objB)

// Vanilla, IE8+
const deepExtend = (out) => {
  out = out || {}

  for (let i = 1; i < arguments.length; i++) {
    let obj = arguments[i];

    if (!obj)
      continue

    for (let key in obj) {
      if (obj.hasOwnProperty(key)) {
        if (typeof obj[key] === 'object')
          out[key] = deepExtend(out[key], obj[key]);
        else
          out[key] = obj[key];
      }
    }
  }

  return out;
};

deepExtend({}, objA, objB);
```

## Extend

Alternatives:

http://lodash.com/docs#assign

http://underscorejs.org/#extend

http://www.2ality.com/2014/01/object-assign.html ECMA6

```javascript
// jQuery
$.extend({}, objA, objB)

// Vanilla, IE8+
var extend = (out) => {
  out = out || {}

  for (var i = 1; i < arguments.length; i++) {
    if (!arguments[i])
      continue

    for (var key in arguments[i]) {
      if (arguments[i].hasOwnProperty(key))
        out[key] = arguments[i][key]
    }
  }

  return out;
}

extend({}, objA, objB);
```
### Index Of
```javascript
//jQuery
$.inArray(item, array);

// Vanilla, IE8+
const indexOf = (array, item) => {
  for (var i = 0; i < array.length; i++) {
    if (array[i] === item)
      return i;
  }
  return -1;
}

indexOf(array, item);

// Vanilla, IE9+
array.indexOf(item);
```
### Is Array
```javascript
//jQuery
$.isArray(arr);

// Vanilla, IE8+
isArray = Array.isArray || (arr) => {
  Object.prototype.toString.call(arr) == '[object Array]';
};

isArray(arr);

// Vanilla, IE9+
Array.isArray(arr);
```
### Map
```javascript
//jQuery
$.map(array, (value, index) => {
  // Code
});

// Vanilla, IE8+
const map = (arr, fn) => {
  const results = []
  for (let i = 0; i < arr.length; i++)
    results.push(fn(arr[i], i))
  return results
}

map(array, (value, index) => {
  // Code
})

// Vanilla, IE9+
array.map((value, index) => {
  // Code
})
```
### Now
```javascript
// jQuery
$.now()

// Vanilla, IE8+
new Date().getTime()

// Vanilla, IE9+
Date.now()
```
### Parse Html
```javascript
// jQuery
$.parseHTML(htmlString)

// Vanilla, IE8+
const parseHTML = (str) => {
  const el = document.createElement('div')
  el.innerHTML = str
  return el.children
}

parseHTML(htmlString);

// Vanilla, IE9+
const parseHTML = (str) => {
  const tmp = document.implementation.createHTMLDocument()
  tmp.body.innerHTML = str
  return tmp.body.children
}

parseHTML(htmlString)
```
### Parse Json
```javascript
// jQuery
$.parseJSON(string)

// Vanilla, IE8+
JSON.parse(string)
```
### Trim
```javascript
// jQuery
$.trim(string)

// Vanilla, IE8+
string.replace(/^\s+|\s+$/g, '')

// Vanilla, IE9+
string.trim()
```
