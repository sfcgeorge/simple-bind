# simple-bind

A simple JS library for binding input fields to output elements.

I didn't want the bloat of Angular, Ember, React or similar; but I did want some simple binding capabilities:

* Get JSON from an API and insert it into placeholders in the page.
* Read an object from form fields.
* Live update a binding between fields and output elements.

See the simple demo.html for a full example.

# Markup

simple-bind uses data-attributes to read input data and output data. A namespace is used which means you can have multiple different data bindings in your app. You might have a blog post binding, and a user data binding for example.

## data-sb-namespace-input="name"

Name the element and set it as an input. The element must have a value attribute like an input.

## data-sb-demo-output="name" 

Name the element and set it as an output. Must be an element with an innerHTML like a div.

## data-sb-attributes="attr1 attr2 ..." 

Only use in conjunction with outputs. Optionally specify attributes on the element to also be updated. Examples:

* Set an element's id to its data.
* Set an element's title to it's data.

## data-sb-format="format string"

Perform some simple formatting on the data before setting it as the element's innerHTML.

Formatting options:

%s - Interpolate the data
%S - Interpolate the data surrounded by whitespace
%L - Interpolate the data with whitespace on the right
%R - Interpolate the data with whitespace on the left
%t{foo} - Interpolate foo if the data isn't blank
%f{bar} - Interpolate bar if the data is blank

For example to interpolate the data into the title, showing a dash when there is data:

`data-sb-format="%s%t{ - }Simple Bind"`

## data-sb-attr-format="format string"

Perform some simple formatting on the data before setting it as the element attribute.

For example to conditionally set the class to "hidden" when data is empty and "" when there is data:

`data-sb-class-format="%f{hidden}"`


# Methods

## new SimpleBind(namespace)

Create a simple-bind instance with a namespace, this means you can have multiple different data bindings in your app. You might have a blog post binding, and a user data binding for example.

```javascript
var demo = new SimpleBind('demo');
```

## inputData()

This gets an object of the values from input fields.

## inputData({ ... })

This sets the values of input fields.

## outputData()

This gets the data from output elements.

## outputData({ ... })

This sets the data of output elements.

## update()

Passes the input data to the output data. Equivalent of manually doing:

```javascript
demo.outputData(demo.inputData());
```

You can implement live updating quite simply:

```javascript
function update() {
  demo.update();
}
```

```html
<input type="text" data-sb-demo-input="title" onkeyup="update()">
```
