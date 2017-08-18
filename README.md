# Vue Clazy Load

> _Claziest_ lazy loader out there!

Component-based image lazy loader allowing deep customization, transitions and optimizations for Vue.js 2.

[![npm](https://img.shields.io/npm/dm/vue-clazy-load.svg)](https://www.npmjs.com/package/vue-clazy-load)
[![npm](https://img.shields.io/npm/v/vue-clazy-load.svg)](https://www.npmjs.com/package/vue-clazy-load)
[![npm](https://img.shields.io/npm/l/vue-clazy-load.svg)](https://www.npmjs.com/package/vue-clazy-load)
[![GitHub pull requests](https://img.shields.io/badge/PR-welcome-green.svg)]()
[![GitHub stars](https://img.shields.io/github/stars/matheusgrieger/vue-clazy-load.svg?style=social&label=Star)]()

## Goals and objectives

There are plenty of other Lazy Loaders out there, but they are all `directive`-based. Clazy Load is `component`-based, meaning you can use other components as the preloader or loading message, such as spinners from component kits like Vuetify and KeenUI and transition between loading and loaded states. That is not possible with other libraries.

This project is also lightweight (<800 bytes gzipped) and uses the latest web APIs for best performance.

## Installation

Select one option:

1. Install using **npm**

  ```sh
  npm install vue-clazy-load --save
  ```
  You can emit the `--save` option if using `npm@^5`.

  You can also use Yarn as:

  ```sh
  yarn add vue-clazy-load
  ```

  In your JavaScript file:

  ```js
  import VueClazyLoad from 'vue-clazy-load'
  ```

  \- or -

  ```js
  var VueClazyLoad = require('vue-clazy-load')
  ```

2. Embed script tag

  ```html
  <script src="https://unpkg.com/vue-clazy-load/dist/vue-clazy-load.min.js"></script>
  ```

Then register the component into Vue:

```js
Vue.use(VueClazyLoad)
```

## Documentation

Using Clazy Load is easy. The HTML code you need is the following:

```html
<clazy-load src="https://unsplash.it/500">
  <img src="https://unsplash.it/500" slot="image">
  <div class="preloader" slot="placeholder">
    Loading message
  </div>
</clazy-load>
```

And no JS code is needed whatsoever, Clazy Load works out of the box.

### Props

The component needs some configuration, though. It's only one required option, so it remains pretty simple.

| Prop | Description | Type | Default |
|------|-------------|------|---------|
| src | Image source that will be loaded. | String | _required_ |
| tag | What tag the component will render to, like [vue-router router-link component](https://router.vuejs.org/en/api/router-link.html). | String | div
| element | Selector for IntersectionObserver's root element. Leave blank to use _viewport_. See below for more details. | String | `null`
| threshold | Values for IntersectionObserver's threshold option. See below for more details. | Array/Number | `[0, 0.5, 1]`

### Classes

Custom classes on the Clazy Load component are passed to the rendered output.

Also, the component adds `loading` and `loaded` classes to the **root** element regarding the two possible states, enabling further customization with CSS.

### Sub-components and elements

The reason the component has a `src` prop while the `<img>` does as well is to unbind them and allow you to use whatever you want in the `image` slot. For instance, a simple case in which you would separate the image from the loader:

```html
<clazy-load src="imgsrc">
  <figure class="image-wrapper" slot="image">
    <img src="imgsrc">
  </figure>
  <div class="preloader-wrapper" slot="placeholder">
    <preloader-component></preloader-component>
  </div>
</clazy-load>
```

Another case would be to use transitions. Check out the [example](example/index.html) for details in using transitions.

### Scroll watching behavior

Clazy Load uses the new IntersectionObserver API to watch for element visibility on screen. This way it is not only optimized due to use native browser API, it has no proprietary code or gimmicks watching for scroll and making checks, so it will be easier to maintain.

The downside is that this API is quite recent, so there still is small browser compatibility. Gladly, [Polyfill.io](https://polyfill.io/) covers this use case, and if you need to support older browsers, such as IE, you can include the following tag in your page:

```html
<script src="https://cdn.polyfill.io/v2/polyfill.min.js?features=IntersectionObserver"></script>
```

Or simply add `IntersectionObserver` to the `?features=` query of the URL if already using Polyfill.

The two configurable props `element` and `threshold` are bound to IntersectionObserver. `element` is used in a `document.querySelector` to pass the element to the `root` option, and `threshold` is used as it is. More details on those two options are available on [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API).

## TODOs

- [ ] Configurable loading error, possibly with another slot
- [ ] Configurable `intersectionRatio` comparison value
- [ ] Custom state class names

## Contributing

Issues, questions and pull requests are always welcome. Just don't be unpleasant.

## License

[MIT](http://opensource.org/licenses/MIT)

Copyright (c) 2017, Matheus Grieger
