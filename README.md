puredom-sync [![Version](https://img.shields.io/npm/v/puredom-sync.svg?style=flat)](https://www.npmjs.org/package/puredom-sync) ⎔ [![Build Status](https://img.shields.io/travis/developit/puredom-sync.svg?style=flat&branch=master)](https://travis-ci.org/developit/puredom-sync)
=============

A [puredom](http://puredom.org) plugin that lets you synchronously chain asynchronous functions.  


---


What it Does
------------

Normally, puredom's chained selection functions run in parallel (asynchronously). They
do not wait for pending operations to finish before moving on to the next chained call.

This is ideal for many cases, but it can become cumbersome when chaining animation callbacks.
To solve this problem, puredom.async adds a few selector functions: `sync()`, `async()` and `then()`.


`.sync()`: Run everything in the order I say
--------------------------------------------

`.sync()` switches the chain into "sync" mode. In this mode,
	all chained selection functions you call will run **in order**.

```JavaScript
puredom('.foo')       // anything that returns a selection
	.sync()           // switch the chain to sync mode
	.fadeOut('slow')  // fade out the selection
	.fadeIn('fast')   // `-> fade the selection back in
	.hide();          //    `-> finally, hide the selection
```

`.async()`: Run everything at once
----------------------------------

`.async()` reverts the chain back to puredom's normal (asynchronous) mode.

```JavaScript
// selection in sync mode:
var sel = puredom('.foo').sync();

// these animations run sequentially:
sel.fadeIn().fadeOut();

// back to async: (this runs prior to the animations!)
console.log(sel.async().width());
```

`.then()`: Let me know when sync() is done
------------------------------------------

`.then()` lets you specify a function to call once the synchronous
chain's current operations have finished executing:

```JavaScript
puredom('.foo').sync().fadeIn().fadeOut().then(function() {
	alert("fade in and out have completed");
});
```


---


License
=======
This plugin is available under the BSD-3-Clause License:

>	Copyright (c) Jason Miller. All rights reserved.
>
>	Redistribution and use in source and binary forms, with or without modification,
>	are permitted provided that the following conditions are met:
>
>	*	Redistributions of source code must retain the above copyright notice,
>		this list of conditions and the following disclaimer.
>
>	*	Redistributions in binary form must reproduce the above copyright notice,
>		this list of conditions and the following disclaimer in the documentation
>		and/or other materials provided with the distribution.
>
>	*	Neither the name of Jason Miller, nor the names of its contributors may be used to endorse
>		or promote products derived from this software without specific prior written permission.
>
>	THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS
>	OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY
>	AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER
>	OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
>	DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
>	DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER
>	IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY
>	OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
