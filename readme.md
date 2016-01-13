﻿# js-data-jsonapi
JsonApi Adapter for [js-data](www.js-data.io) 
This adapter implements the [JsonApi Protocol](http://jsonapi.org/) and ties it to a js-data data store.

It ties 
 - JsonApi **types** to js-data **resource**
 - JsonApi **relations** to js-data **toOne, toMany Relationships**

##Goals
1. Serialize JsonApi requests (Status: code complete, some tests).
1. When deserializing JsonApi data add 'ParentIds' so that js-data **belongsTo** relationships can work (Status: code complete, some tests). 
1. When deserializing JsonApi data add **'LocalKey/LocalKeys'** or **'ForeignKeys'** depending on js-data configurations so that js-data **hasOne** and **hasMany** relationships can work (Status: code complete, some tests). 
1. Add metadata to indicate if anobject is a jsonApi reference, indicating thhat it is partually populated only (Status: code complete, some tests).
1. Transparenetly request full objects when requested from js-data cache and object is a jsonApi reference only, e.g. Not fully populated (Not started).
1. Store hyperlinking data within metadata of stored data (Not started).
1. Use metadata hyperlinks to request related data from JsonApi data store (Barley started).
1. Use metadata hyperlinks to add new items to relationships (Not started).

### Known Issues
1. Testing is by no menas complete, there are many more scenarios that need to be covered off.
1. None of the xxxxAll adapter methods have been tested yet. e.g  findAll, destroyAll, updateAll
1. Bower package has not been tested
1. The code creates the DSHttpDataAdapter internally,however i believe for example that there is an angular specific version. The HttpAdapter may not be created correctly using this package.
   - Allow the adpater to be injected or a constructor function passed via constructor options.
1. Code has been developed using typescript, the generated java-script code DOES NOT pass jslint.
   - Could add typescript linting or port to compliant js by had.But i prefer to work in typescript as i am not a pro javascript developer and typescript checks lets you know when you nake mistakes!!
   - tslint using microsoft recommended rules still some outstanding lint issues
1. Code is some what brittle in terms of requiring your js-data configuration to match very closely your jsonApi
   - Could look at adding additional configuration to allow flexable mapping between js-data and jsonapi
1. I haven't actually tested this against a jsonApi implementation yet like ember, but i have had previous experience with jsonApi and am fairly confident that this implementation is good.
   - More testing to be done......


### Quick Start
`npm install --save js-data js-data-http js-data-jsonapi` or `bower install --save js-data js-data-http js-data-jsonapi`.

Load `js-data-jsonapi.js` after and `js-data-http.js` after `js-data.js`.

```js
var adapter = new DSJsonApiAdapter.JsonApiAdapter();

var store = new JSData.DS();
store.registerAdapter('jsonApi', adapter, { default: true });

// "store" will now use the jsonApi adapter for all async operations
```

### Version
0.0.0-alpha.1

### Tech

js-data-jsonapi uses a number of open source projects to work properly:

* [js-data](https://github.com/js-data/js-data) - makes use of js-data apis for integration
* [js-data-http](https://github.com/js-data/js-data-http) - Provides HTTP services!

### License

The MIT License (MIT)

Copyright (c) 2015-2016 Blair Jacobs

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.