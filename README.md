# jquery.directive.js #

## What does it do?

This jQuery plugin recreates some of the directive magic (https://docs.angularjs.org/guide/directive) possible with Angular.
For example, with Angular you can write something like this:

```html
<div my-directive></div>
```

```javascript
angular.module('app').directive('myDirective', function() {

    return function($scope, element, attrs, controller) {
        // This function will be called for every individual element in the page
        // that has a "my-directive" attribute, even when the elements is
        // created after the script is run.
    };

});
```

With `jquery.directive.js`, you can achieve the same effect:

```javascript
$.directive('my-directive',  function(element, attrs) {  
    // This function will be called for every individual element in the page
    // that has a "my-directive" attribute, even when the elements is
    // created after the script is run.
});
```

For each matching element the plugin also provides a convenient
object containing all the element's attribute/value pairs:

```html
<div my-directive foo="bar" value="123"></div>
```

```javascript
$.directive('my-directive',  function(element, attrs) {  
    // attrs = {
    //    "my-directive": "",
    //    "foo": "bar",
    //    "value": 123
    // }
});
```

Attribute values will automatically be converted to booleans, integers,
floats and JSON objects when appropriate.

## How can I use it?

One way to use it, is to make initializing (3rd party) jQuery plugins a breeze.
Let's say you want to use a plugin called `jquery.foo.js`, you usually
have to do something like this:

```html
<div class="foo"></div>
```

```javascript
// Initialize jquery.foo.js plugin
$('.foo').foo();
```

Great, but this only works for elements with class="foo" that are already in
the document when the script is run. If you add new .foo elements (for example
via ajax), they will not initialized. With jQuery directives
you can do this:

```html
<div foo><div>
```

```javascript
$.directive('foo',  function(element, attrs) {  
    // Initialize jquery.foo.js plugin
    element.foo();
});
```
