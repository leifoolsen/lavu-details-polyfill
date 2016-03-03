# Details Element Polyfill

<img src="./etc/details-element.png"/>

**WORK IN PROGRESS ....**

The ```<details>``` element specifies additional details that the user can view or hide on demand. The ```<summary>``` element defines a visible heading for the ```<details>``` element. The heading can be clicked to view/hide the details.

The ```<details>``` element currently has very limited cross-browser support. This polyfill provides support for the &lt;detail&gt; element across all modern browsers.

The polyfill is based on the spec for the details element.
* [WhatWG, 4.11.1 The details element](http://www.whatwg.org/specs/web-apps/current-work/multipage/interactive-elements.html)
* [W3C Markup, details – control for additional on-demand information](http://dev.w3.org/html5/markup/details.html)
* [HTML/Elements/details Wiki](http://www.w3.org/wiki/HTML/Elements/details)

If you'd like to use the details element and don't know where to start, take a look at this tutorial 
[The details and summary elements](http://html5doctor.com/the-details-and-summary-elements/) at the html5doctor - 
or [read the tests](https://github.com/leifoolsen/lavu-details-polyfill/blob/master/test/index.spec.js). 

## Features
* `open` attribute support
* fires `click` event when open state changes
* keyboard and ARIA-friendly
* fully customisable via CSS

## Install
```sh
$ npm install --save lavu-details-polyfill
```

## Usage
Use it in your page
```html
<script src="node_modules/lavu-details-polyfill/dist/lavu-details-polyfill.js"></script>
```

... or require the polyfill
```javascript
var polyfillDetails = require('lavu-details-polyfill');
```

... or import the polyfill
```javascript
import { polyfillDetails } from 'lavu-details-polyfill';
```

The script uses the ```load``` event to polyfill the ```<details>``` elements.

If you load HTML fragments dynamically, e.g. in a single page application, then you must call the polyfill after loading the HTML.
```javascript
polyfillDetails(content);
```

Where ```content``` is the parent node of the loaded HTML fragment.


## Notes
The polyfill provides a minimal CSS meant to mimic the default unstyled browser look which
you can override in your own CSS/SASS/LESS module.
```CSS
details, details>summary {
  display: block;
}
details > summary {
  min-height: 1.4em;
  padding: 0.125em;
}
details > summary:before {
  content:"►";
  font-size: 1em;
  position: relative;
  display: inline-block;
  width: 1em;
  height: 1em;
  margin-right: 0.3em;
  -webkit-transform-origin: 0.4em 0.6em;
     -moz-transform-origin: 0.4em 0.6em;
      -ms-transform-origin: 0.4em 0.6em;
          transform-origin: 0.4em 0.6em;
}
details[open] > summary:before {
  content:"▼"
}
details > *:not(summary) {
  display: none;
  opacity: 0;
}
details[open] > *:not(summary) {
  display: block;
  opacity: 1;
}
```

Semantic (correct) markup example:
```html
<details role="group" open>
  <summary role="button">Show/Hide me</summary>
  <p>Some content ..... etc.</p>
</details>
```

There is no guarantee that the browser's implementation of the ```<details>``` element will
respect it's child elements layout when toggeling the details. To preserve the child elements layout,
you should always wrap the child elements inside a block element, e.g. a ```<div>```.

```html
<style>
  .inline-element { display : inline-block; }
</style
<details role="group">
  <summary role="button">Show/Hide me</summary>
  <div>
    <div class="inline-element">
      <p>Some content ..... etc.</p>
    </div>
  </div>
</details>
```

### Credits: The ```<select>``` polyfill is partly based on/inspired by the following sources:
* https://github.com/jordanaustin/Details-Expander
* https://github.com/chemerisuk/better-details-polyfill
* http://codepen.io/stevef/pen/jiCBE
* http://blog.mxstbr.com/2015/06/html-details/
* http://html5doctor.com/the-details-and-summary-elements/
* http://zogovic.com/post/21784525226/simple-html5-details-polyfill
* http://www.sitepoint.com/fixing-the-details-element/
* https://www.smashingmagazine.com/2014/11/complete-polyfill-html5-details-element/

## Licence
[MIT](http://www.opensource.org/licenses/mit-license.php)