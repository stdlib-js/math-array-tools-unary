<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# Unary

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Constructor for applying a unary function to each element in an input array.



<section class="usage">

## Usage

```javascript
import Unary from 'https://cdn.jsdelivr.net/gh/stdlib-js/math-array-tools-unary@esm/index.mjs';
```

#### Unary( fcn, idtypes, odtypes, policy )

Constructor for applying a unary function to each element in an input array.

```javascript
import abs from 'https://cdn.jsdelivr.net/gh/stdlib-js/math-base-special-abs@esm/index.mjs';

var dtypes = [ 'float64', 'float32', 'generic' ];
var policy = 'same';

var unary = new Unary( abs, dtypes, dtypes, policy );
```

The constructor has the following parameters:

-   **fcn**: unary function to apply.
-   **idtypes**: list of supported input data types.
-   **odtypes**: list of supported input data types.
-   **policy**: output data type policy.

#### Unary.prototype.apply( x\[, options] )

Applies a unary function to each element in a provided input array.

```javascript
import abs from 'https://cdn.jsdelivr.net/gh/stdlib-js/math-base-special-abs@esm/index.mjs';

var dtypes = [ 'float64', 'float32', 'generic' ];
var policy = 'same';

var unary = new Unary( abs, dtypes, dtypes, policy );

var v = unary.apply( [ -1.0, 2.0, -3.0, 4.0 ] );
// returns [ 1.0, 2.0, 3.0, 4.0 ]
```

The method has the following parameters:

-   **x**: input array.
-   **options**: function options.

The method accepts the following options:

-   **dtype**: output array data type. Setting this option, overrides the output data type policy.

By default, the method returns an array having a data type determined by the output data type policy. To override the default behavior, set the `dtype` option.

```javascript
import abs from 'https://cdn.jsdelivr.net/gh/stdlib-js/math-base-special-abs@esm/index.mjs';

var dtypes = [ 'float64', 'float32', 'generic' ];
var policy = 'same';

var unary = new Unary( abs, dtypes, dtypes, policy );

var v = unary.apply( [ -1.0, 2.0, -3.0, 4.0 ], {
    'dtype': 'float64'
});
// returns <Float64Array>[ 1.0, 2.0, 3.0, 4.0 ]
```

#### Unary.prototype.assign( x, out )

Applies a unary function to each element in a provided input array and assigns results to a provided output array.

```javascript
import abs from 'https://cdn.jsdelivr.net/gh/stdlib-js/math-base-special-abs@esm/index.mjs';
import zeros from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-zeros@esm/index.mjs';

var dtypes = [ 'float64', 'float32', 'generic' ];
var policy = 'same';

var unary = new Unary( abs, dtypes, dtypes, policy );

var out = zeros( 4, 'float64' );
// returns <Float64Array>[ 0.0, 0.0, 0.0, 0.0 ]

var v = unary.assign( [ -1.0, 2.0, -3.0, 4.0 ], out );
// returns <Float64Array>[ 1.0, 2.0, 3.0, 4.0 ]

var bool = ( v === out );
// returns true
```

The method has the following parameters:

-   **x**: input array.
-   **out**: output array.

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   The output data type policy only applies to the `apply` method. For the `assign` method, the output array is allowed to be any array-like object, including [accessor arrays][@stdlib/array/base/accessor].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="module">

import base from 'https://cdn.jsdelivr.net/gh/stdlib-js/math-base-special-sin@esm/index.mjs';
import uniform from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-array-uniform@esm/index.mjs';
import dtypes from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-dtypes@esm/index.mjs';
import dtype from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-dtype@esm/index.mjs';
import logEach from 'https://cdn.jsdelivr.net/gh/stdlib-js/console-log-each@esm/index.mjs';
import Unary from 'https://cdn.jsdelivr.net/gh/stdlib-js/math-array-tools-unary@esm/index.mjs';

// Define the supported input and output data types:
var idt = dtypes( 'real_and_generic' );
var odt = dtypes( 'real_floating_point_and_generic' );

// Define the policy mapping an input data type to an output data type:
var policy = 'real_floating_point_and_generic';

// Create an interface for computing the element-wise sine:
var sin = new Unary( base, idt, odt, policy );

// Generate an array of random numbers:
var x = uniform( 10, -1.0, 1.0, {
    'dtype': 'generic'
});

// Compute the element-wise sine:
var y = sin.apply( x );

// Resolve the output array data type:
var dt = dtype( y );
console.log( dt );

// Print the results:
logEach( 'sin(%0.5f) = %0.5f', x, y );

</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2025. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/math-array-tools-unary.svg
[npm-url]: https://npmjs.org/package/@stdlib/math-array-tools-unary

[test-image]: https://github.com/stdlib-js/math-array-tools-unary/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/math-array-tools-unary/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/math-array-tools-unary/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/math-array-tools-unary?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/math-array-tools-unary.svg
[dependencies-url]: https://david-dm.org/stdlib-js/math-array-tools-unary/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/math-array-tools-unary/tree/deno
[deno-readme]: https://github.com/stdlib-js/math-array-tools-unary/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/math-array-tools-unary/tree/umd
[umd-readme]: https://github.com/stdlib-js/math-array-tools-unary/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/math-array-tools-unary/tree/esm
[esm-readme]: https://github.com/stdlib-js/math-array-tools-unary/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/math-array-tools-unary/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/math-array-tools-unary/main/LICENSE

[@stdlib/array/base/accessor]: https://github.com/stdlib-js/array-base-accessor/tree/esm

</section>

<!-- /.links -->
