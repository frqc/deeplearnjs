<a id="travis-badge" href="https://travis-ci.org/PAIR-code/deeplearnjs" alt="Build Status">
  <img src="https://travis-ci.org/PAIR-code/deeplearnjs.svg?branch=master" />
</a>

# Getting started

**deeplearn.js** is an open source hardware-accelerated JavaScript library for
machine intelligence. **deeplearn.js** brings performant machine learning
building blocks to the web, allowing you to train neural networks in a browser
or run pre-trained models in inference mode.

We provide two APIs, an immediate execution model (think NumPy) and a deferred
execution model mirroring the TensorFlow API.
**deeplearn.js** was originally developed by the Google Brain PAIR team to build
powerful interactive machine learning tools for the browser, but it can be used
for everything from education, to model understanding, to art projects.

## Usage

#### Typescript / ES6 JavaScript

```
npm install deeplearn
```

A simple example that sums an array with a scalar (broadcasted):

```ts
import {Array1D, NDArrayMathGPU, Scalar} from 'deeplearn';

const math = new NDArrayMathGPU();
const a = Array1D.new([1, 2, 3]);
const b = Scalar.new(2);

const result = math.add(a, b);

// Option 1: With async/await.
// Caveat: in non-Chrome browsers you need to put this in an async function.
console.log(await result.data());  // Float32Array([3, 4, 5])

// Option 2: With a Promise.
result.data().then(data => console.log(data));

// Option 3: Synchronous download of data.
// This is simpler, but blocks the UI until the GPU is done.
console.log(result.dataSync());
```

#### ES3/ES5 JavaScript

You can also use **deeplearn.js** with plain JavaScript. Load the latest version
of the library from [unpkg](https://unpkg.com):

```html
<script src="https://unpkg.com/deeplearn"></script>
```

To use a specific version, add `@version` to the unpkg URL above
(e.g. `https://unpkg.com/deeplearn@0.2.0`), which you can find in the
[releases](https://github.com/PAIR-code/deeplearnjs/releases) page on GitHub.
After importing the library, the API will be available as `deeplearn` in the
global namespace:

```js
var dl = deeplearn;

var math = new dl.NDArrayMathGPU();
var a = dl.Array1D.new([1, 2, 3]);
var b = dl.Scalar.new(2);

var result = math.add(a, b);

// Option 1: With a Promise.
result.data().then(data => console.log(data)); // Float32Array([3, 4, 5])

// Option 2: Synchronous download of data. This is simpler, but blocks the UI.
console.log(result.dataSync());
```


## Development

To build **deeplearn.js** from source, we need to clone the project and prepare
the dev environment:

```bash
$ git clone https://github.com/PAIR-code/deeplearnjs.git
$ cd deeplearnjs
$ npm run prep # Installs node modules and bower components.
```

We recommend using [Visual Studio Code](https://code.visualstudio.com/) for
development. Make sure to install the `clang-format` command line tool as
well as the [Clang-Format VSCode extension](https://marketplace.visualstudio.com/items?itemName=xaver.clang-format) for auto-formatting.

To interactively develop any of the demos (e.g. `demos/nn-art/`):

```bash
$ ./scripts/watch-demo demos/nn-art
>> Starting up http-server, serving ./
>> Available on:
>>   http://127.0.0.1:8080
>> Hit CTRL-C to stop the server
>> 1357589 bytes written to dist/demos/nn-art/bundle.js (0.85 seconds) at 10:34:45 AM
```

Then visit `http://localhost:8080/demos/nn-art/`. The
`watch-demo` script monitors for changes of typescript code and does
incremental compilation (~200-400ms), so users can have a fast edit-refresh
cycle when developing apps.

Before submitting a pull request, make sure the code passes all the tests and is clean of lint errors:

```bash
$ npm run test
$ npm run lint
```

To build a standalone ES5 library that can be imported in the browser with a
`<script>` tag:

```bash
$ ./scripts/build-standalone.sh # Builds standalone library.
>> Stored standalone library at dist/deeplearn(.min).js
```

To do a dry run and test building an npm package:

```bash
$ ./scripts/build-npm.sh
>> Stored npm package at dist/deeplearn-VERSION.tgz
```

To install it locally, run `npm install ./dist/deeplearn-VERSION.tgz`.

> On Windows, use bash (available through git) to use the scripts above.

## Supported environments

**deeplearn.js** targets WebGL 1.0 devices with the `OES_texture_float`
extension and also targets WebGL 2.0 devices. For platforms without WebGL,
we provide CPU fallbacks.

However, currently our demos do not support Mobile, Firefox, and Safari. Please
view them on desktop Chrome for now. We are working to support more devices.
Check back soon!

## Resources

* [Tutorials](http://pair-code.github.io/deeplearnjs/docs/tutorials/index.html)
* [API Reference](http://pair-code.github.io/deeplearnjs/docs/api/globals.html)
* [Demos](http://pair-code.github.io/deeplearnjs/index.html#demos)
* [Roadmap](http://pair-code.github.io/deeplearnjs/docs/roadmap.html)

## Thanks

<p style="display:flex; align-items:center;">
  <a href="https://www.browserstack.com/">
    <img src="https://www.browserstack.com/images/layout/browserstack-logo-600x315.png" height="70" style="height:70px;">
  </a>
  <span>&nbsp; for providing testing support.</span>
</p>

This is not an official Google product.
