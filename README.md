# Vanilla JS vs jQuery

## Events

```javascript
// jQuery
$(document).ready(function() {
  // code
})

// Vanilla
document.addEventListener('DOMContentLoaded', function() {
  // code
})
```

```javascript
// jQuery
$('a').click(function() {
  // code…
})

// Vanilla
[].forEach.call(document.querySelectorAll('a'), function(el) {
  el.addEventListener('click', function() {
    // code…
  })
})
```

## Selectors

```javascript
// jQuery
var divs = $('div')

// Vanilla
var divs = document.querySelectorAll('div')
```

```javascript
// jQuery
var newDiv = $('<div/>')

// Vanilla
var newDiv = document.createElement('div')
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
var clonedElement = $('#about').clone()

// Vanilla
var clonedElement = document.getElementById('about').cloneNode(true)
```

```javascript
// jQuery
$('#wrap').empty()

// Vanilla
var wrap = document.getElementById('wrap')
while(wrap.firstChild) wrap.removeChild(wrap.firstChild)
```

## Transversing

```javascript
// jQuery
var parent = $('#about').parent()

// Vanilla
var parent = document.getElementById('about').parentNode
```

```javascript
// jQuery
if($('#wrap').is(':empty'))

// Vanilla
if(!document.getElementById('wrap').hasChildNodes())
```

```javascript
// jQuery
var nextElement = $('#wrap').next()

// Vanilla
var nextElement = document.getElementById('wrap').nextSibling
```

## AJAX

### GET
```javascript
// jQuery
$.get('//example.com', function (data) {
  // code
})

// Vanilla
var httpRequest = new XMLHttpRequest()
httpRequest.onreadystatechange = function (data) {
  // code
}
httpRequest.open('GET', url)
httpRequest.send()
```

### POST
```javascript
// jQuery
$.post('//example.com', { username: username }, function (data) {
  // code
})

// Vanilla
var httpRequest = new XMLHttpRequest()
httpRequest.onreadystatechange = function (data) {
  // code
}
httpRequest.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
httpRequest.open('POST', url)
httpRequest.send('username=' + encodeURIComponent(username))
```

### JSONP
```javascript
// jQuery
$.getJSON('//openexchangerates.org/latest.json?callback=?', function (data) {
  // code
})

// Vanilla
function success(data) {
  // code
}
var scr = document.createElement('script')
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
$(el).fadeIn();

```
##### IE8+
```javascript
// Vanilla
const fadeIn = (el) => {
  const opacity = 0;

  el.style.opacity = 0;
  el.style.filter = '';

  const last = +new Date();
  const tick = () => {
    opacity += (new Date() - last) / 400;
    el.style.opacity = opacity;
    el.style.filter = 'alpha(opacity=' + (100 * opacity)|0 + ')';

    last = +new Date();

    if (opacity &lt; 1) {
      (window.requestAnimationFrame &amp;&amp; requestAnimationFrame(tick)) || setTimeout(tick, 16);
    }
  };

  tick();
}

fadeIn(el);
```
##### IE9+
```javascript
// Vanilla
const fadeIn = (el) => {
  el.style.opacity = 0;

  const last = +new Date();
  const tick = () => {
    el.style.opacity = +el.style.opacity + (new Date() - last) / 400;
    last = +new Date();

    if (+el.style.opacity &lt; 1) {
      (window.requestAnimationFrame &amp;&amp; requestAnimationFrame(tick)) || setTimeout(tick, 16);
    }
  };

  tick();
}

fadeIn(el);
```
##### IE10+
```javascript
// Vanilla
el.classList.add('show');
el.classList.remove('hide');
```
##### CSS
```css
.show {
  transition: opacity 400ms;
}
.hide {
  opacity: 0;
}
```
#### Hide
```javascript
//jQuery
$(el).hide();
```
##### IE8+
```javascript
// Vanilla
el.style.display = 'none';
```
#### Show
```javascript
//jQuery
$(el).show();
```
##### IE8+
```javascript
// Vanilla
el.style.display = '';
```
