**The _Carbon Component library_ gives developers (Front End Developers & Engineers) a collection of re-usable HTML and Sass partials they can use for building websites and user-interfaces for Bluemix. The aim is for all developers to use consistent markup, styles, and behavior in their prototype and production work.**

## Quick start

Using npm:

```bash
$ npm install --save @carbon/components
```

## What's included

The `global` directory includes transpiled, minified assets needed to use the Carbon Design System. 


Including the minified or the non-minified assets as well as any HTML snippets will have Carbon work for you out of the box. This methodology is appropriate for sandbox environments or testing, but we recommmend people use the modules to create an optimized build.

```javascript
carbon/
├── global/
    ├── carbon.js
    └── carbon.min.js
    ├── carbon.css
    ├── carbon.min.css
├── components/
│   ├── modal
│   │   ├── _modal.scss
│   │   ├── modal.umd.js
│   │   ├── modal.js
│   │   ├── modal.es5.js
│   │   ├── modal.html
│   ├── button / etc
│   ├── index.es5.js
│   ├── index.umd.js
│   ├── index.js
│   ├── index.scss
```

## SASS

Using the Carbon sass files infers usage of the SASS pre-processor and a build step to process the files.

#### Importing a component style

To add a component style to your build, simply import the component directly

```javascript
@import 'node_modules/@carbon/components/card/card';
```

Importing a component this way will bring in any dependencies that component has well; the import system dedupes dependencies, so shared dependendencies between components will not create extra CSS

#### Namespacing

Carbon components are built to be included individually and not clobber global styles - all `class names` are prefixed by the `bx--` moniker.

#### Global Flags

Carbon exposes a few global flags to alter what CSS gets compiled

| SASS flag       | Default | Description                                                                         |
|-----------------|---------|-------------------------------------------------------------------------------------|
| $css--font-face | false   | If set to true, add in css font face definition                                     |
| $css--helpers   | true    | If set to true, create the css visual helper styles                                 |
| $css--body      | true    | If set to true, set default body and typographical styles                           |
| $css--reset     | false   | If set to true, remove the reset on individual components and apply to global scope |

## Javascript

### Using a module bundler: recommended

Using a module bundler will bring in only the component code your application needs, created an optimized build for production. Carbon components ships with a `umd` build for each component, as well as an `js:next` build for use with webpack 2 or rollup. After you've installed the components through `npm`, there are a few ways to initialize the component

#### Initialize all instances of a component

```javascript
import { Modal } from '@carbon/components'
Modal.init();
```

#### Initialize a specific instance

```javascript
import { Modal } from '@carbon/components';
const myModal = document.querySelector(querySelector('[data-modal]')); // element node of the modal itself
Modal.init(myModal);
```

#### Reference a previously initialized component

```javascript
import { Modal } from '@carbon/components';
const myModal = document.querySelector(querySelector('[data-modal]'));
const myModalInstance = Modal.components.get(myModal);
```

### Using the compiled carbon-components file directly

Users can also opt to use the pre-compiled `carbon-components.js` file directly. We recommend that most users do _not_ use this file, as it includes components your application may or may not actually be using. By default, including the javascript file will automatically instantiate any component on the page as well as create a global objected called `CarbonComponents`.

#### Initialize all instances of a component

```html
<html>
  <body>
    <script src="node_modules/@carbon/components/global/carbon-components.min.js"></script>
  </body>
</html>
```

#### Don't initialize components by default

```html
<html>
  <body>
    <script>
      CarbonComponents.settings.disableAutoInit = true;
    </script>
    <script src="node_modules/@carbon/components/global/carbon-components.min.js"></script>
  </body>
</html>
```

#### Initialize specific component

```html
<html>
  <body>
    <script>
      CarbonComponents.settings.disableAutoInit = true;
      var modal = document.querySelector('[data-model']);
      CarbonComponents.Modal.init(modal);
    </script>
    <script src="node_modules/@carbon/components/global/carbon-components.min.js"></script>
  </body>
</html>
```

#### Reference a previously initialized component

```html
<html>
  <body>
    <script src="node_modules/@carbon/components/global/carbon-components.min.js"></script>
    <script>
      var modal = document.querySelector('[data-model']);
      var myModalRef = CarbonComponents.Modal.components.get(modal);
    </script>
  </body>
</html>
```