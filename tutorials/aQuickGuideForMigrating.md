---
title: 'Quick guide to migrate your old BioJS component'
layout: tutorial-container
contributors: Seb
category: tutorials
estimated-time: 10 
---

{% alert danger %}
only use this guide for quick & dirty migration with `biojs-legacy`.
We highly encourage you to follow the [real guide](/categories/101_tutorial/index.html) and look at other new components of BioJS 2.0.
{% endalert %}

A working example for this quick migration can be found at [biojs-sequence](https://github.com/ljgarcia/biojs-vis-sequence).


I. Create your BioJS repository
-------------------------------

See the normal guide for more explanation about this or just copy an existing repo like biojs-template.


II. Apply Ugly way: include biojs-legacy
--------------------------------

Let your `BioJs(.*).js` be the `index.js` in the lib folder


### 1. Add  biojs-legacy

####  1.1) install it 

~~~
npm install biojs-legacy --save
~~~

####  1.2) require it 

Add this as the first line of your component.

~~~
var BioJs = require('biojs-legacy');
~~~

### 2. Export your module
 
export your module.
 
~~~
module.exports = Biojs.Sequence = Biojs.extend(
~~~


### 3. Edit your browser.js

~~~
if (typeof biojs === 'undefined') {
  module.exports = biojs = {}
}
if (typeof biojs.vis === 'undefined') {
  biojs.vis = {}
}
biojs.vis.sequence = require('./');

// legacy code begins - add only if absolutely needed
if (typeof Biojs === 'undefined') {
  module.exports = Biojs = {}
}

Biojs.Sequence = require('./');
~~~

### 4. Create your js file

~~~
browserify browser.js > biojs_vis_sequence.min.js
~~~

or 

~~~
npm run build-browser
~~~

This will create the file `biojs_vis_sequence.min.js`

### 5. Check your component with a `dummy.html`

Your component should work now ;-)
Check for third-party libs and error.

### 6. Upload your component to github & npm 

See the normal guide

#### Congrats. You have migrated to BioJS 2.0

and now we encourage you to ... 

### 7. Get rid of biojs-legacy and split your component in reusable modules

Now you can take a coffee break and have a look at the normal guide.


### 8. Event system

~~~
var BioJSEvents = require('biojs-events');
BioJSEvents.mixin(YourClass.prototype);
~~~

You can find more info about the event system on our [github](https://github.com/biojs/biojs-events).
