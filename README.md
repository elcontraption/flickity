# Flickity (customized)
This is essentially a hacked version of Flickity that introduces a hook to apply a function to manipulate cells during animation. It's called on every animation cycle (requestAnimationFrame) so handle with care.

There is a new option: `transitionEffect` that may be passed a function. Within the function, `this` is bound to the cell.

I needed to be able to scale cells as they move toward or away from the center point, as the slider is repositioned:

```js
var transitionEffect = function() {
    var proximity = Math.abs(this.target - Math.abs(this.parent.x));

    proximity *= 0.1;

    var scale = Math.round((100 - Math.round(proximity) / 1)) / 100;

    if (scale >= 0.8 && scale <= 1) {
        this.element.style.transform = 'scale(' + scale + ')';
    }
};

var flickity = new Flickity('.my-element', {
    transitionEffect: transitionEffect
});
```

```css
.cell {
    margin: 0 -50px; // allow cells to overlap
    width: 300px;
    transform: scale(0.5); // initial scale
}

.cell.is-selected {
    transform: scale(1); // selected scale
    z-index: 100 !important;
    opacity: 1;
}
```

_Touch, responsive, flickable galleries_

See [flickity.metafizzy.co](http://flickity.metafizzy.co) for complete docs and demos.

## Install

### Download

+ CSS:
  - [flickity.css](https://github.com/metafizzy/flickity/raw/master/dist/flickity.css) un-minified, or
  - [flickity.css](https://github.com/metafizzy/flickity/raw/master/dist/flickity.min.css) minified
+ JavaScript:
  - [flickity.pkgd.js](https://github.com/metafizzy/flickity/raw/master/dist/flickity.pkgd.js) un-minified, or
  - [flickity.pkgd.min.js](https://github.com/metafizzy/flickity/raw/master/dist/flickity.pkgd.min.js) minified

### CDN

Link directly to [Flickity files on cdnjs](https://cdnjs.com/libraries/flickity).

``` html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.css">
<!-- or -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.min.css">
```

``` html
<script src="https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.pkgd.js"></script>
<!-- or -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/flickity/1.1.2/flickity.pkgd.min.js"></script>
```

### Package managers

Bower: `bower install flickity --save`

npm: `npm install flickity --save`

## License

### Commercial license

If you want to use Flickity to develop commercial sites, themes, projects, and applications, the Commercial license is the appropriate license. With this option, your source code is kept proprietary. Purchase a Flickity Commercial License at [flickity.metafizzy.co](http://flickity.metafizzy.co/#commercial-license)

### Open source license

If you are creating an open source application under a license compatible with the [GNU GPL license v3](https://www.gnu.org/licenses/gpl-3.0.html), you may use Flickity under the terms of the GPLv3.

[Read more about Flickity's license](http://flickity.metafizzy.co/license.html).

## Usage

Flickity works with a container element and a set of child cell elements

``` html
<div class="gallery">
  <div class="cell">...</div>
  <div class="cell">...</div>
  <div class="cell">...</div>
  ...
</div>
```

### Options

``` js
var flky = new Flickity( '.gallery', {
  // options, defaults listed

  accessibility: true,
  // enable keyboard navigation, pressing left & right keys

  autoPlay: false,
  // advances to the next cell
  // if true, default is 3 seconds
  // or set time between advances in milliseconds
  // i.e. `autoPlay: 1000` will advance every 1 second

  cellAlign: 'center',
  // alignment of cells, 'center', 'left', or 'right'
  // or a decimal 0-1, 0 is beginning (left) of container, 1 is end (right)

  cellSelector: undefined,
  // specify selector for cell elements

  contain: false,
  // will contain cells to container
  // so no excess scroll at beginning or end
  // has no effect if wrapAround is enabled

  draggable: true,
  // enables dragging & flicking

  freeScroll: false,
  // enables content to be freely scrolled and flicked
  // without aligning cells

  friction: 0.2,
  // smaller number = easier to flick farther

  initialIndex: 0,
  // zero-based index of the initial selected cell

  lazyLoad: true,
  // enable lazy-loading images
  // set img data-flickity-lazyload="src.jpg"
  // set to number to load images adjacent cells

  percentPosition: true,
  // sets positioning in percent values, rather than pixels
  // Enable if items have percent widths
  // Disable if items have pixel widths, like images

  prevNextButtons: true,
  // creates and enables buttons to click to previous & next cells

  pageDots: true,
  // create and enable page dots

  resize: true,
  // listens to window resize events to adjust size & positions

  rightToLeft: false,
  // enables right-to-left layout

  setGallerySize: true,
  // sets the height of gallery
  // disable if gallery already has height set with CSS

  watchCSS: false,
  // watches the content of :after of the element
  // activates if #element:after { content: 'flickity' }
  // IE8 and Android 2.3 do not support watching :after
  // set watch: 'fallbackOn' to enable for these browsers

  wrapAround: false
  // at end of cells, wraps-around to first for infinite scrolling

});
```

---

By [Metafizzy](http://metafizzy.co)
