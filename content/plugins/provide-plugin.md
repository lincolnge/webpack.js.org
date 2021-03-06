---
title: ProvidePlugin
contributors:
  - sokra
  - simon04
  - re-fort
---

```javascript
new webpack.ProvidePlugin({identifier1: 'module1', /* ... */})
// or
new webpack.ProvidePlugin({identifier1: ['module1', 'property1'], /* ... */})
```

Automatically loads modules. Whenever the `identifier` is encountered as free variable in a module, the `module` is loaded automatically and the `identifier` is filled with the exports of the loaded `module` (of `property` in order to support named exports).

W> For importing the default export of an ES2015 module, you have to specify the default property of module.

## Typical use-cases

### Use jQuery

```javascript
new webpack.ProvidePlugin({
  $: 'jquery',
  jQuery: 'jquery'
})
```

```javascript
// in a module
$('#item'); // <= just works
jQuery('#item'); // <= just works
// $ is automatically set to the exports of module "jquery"
```

### Use jQuery with Angular 1

Angular looks for `window.jQuery` in order to determine whether jQuery is present, see the [source code](https://github.com/angular/angular.js/blob/v1.5.9/src/Angular.js#L1821-L1823)

```javascript
new webpack.ProvidePlugin({
  'window.jQuery': 'jquery'
})
```

### Use map from Lodash

```javascript
new webpack.ProvidePlugin({
  _map: ['lodash', 'map']
})
```

### Use Vue.js

```javascript
new webpack.ProvidePlugin({
  Vue: ['vue/dist/vue.esm.js', 'default']
})
```
