# Code Standards

These are the coding standards that I follow in the all of my coding whether it is front-end or back-end.

**_These standards are a living document and will change as I continue to develop code._**

## General

### Packaging

All javascript libraries are packaged with Browserify.  Is it preferred to install javascript libraries through npm instead of bower and leave bower packages to styling libraries (SASS/CSS).

## JavaScript

### General

Since all code will be packaged with Browserify, all code should be written in NodeJS/CommonJS style.

These are the rules that MUST be applied to all JavaScript that is written. These rules do NOT apply when modifying 3rd party libraries/scripts, in that case you SHOULD following the coding style code of whatever code you are work with (or follow the appeared style of the file if the code does not have a style guide).  These rules apply for both browser and Node.js code. 

Line length MUST NOT exceed 160 characters.

Avoid adding to much to the global object, use object literals as namespaces.

```javascript
//good
var namespace = {
  a: 1,
  b: 2,
  c: 3
};

//bad
var a = 1;
var b = 2;
var c = 3;
```

You MUST always use a semi-colon at the end of every statement.

```javascript
//good
var a = 1;
var b = 2;
var c = 3;

//bad
var a = 1
var b = 2
var c = 3
```

### DOM Data Storage

Always use `data-*` attributes to store data on a DOM element that you might later need to retrieve in JavaScript.  When dealing with these attributes, use the `*Attribute()` methods instead of the dataset as it provide better browser support and is faster (http://jsperf.com/html5-data-attribute-dataset-vs-getattribute).

```javascript
//good
var dataId = node.getAttribute('data-id');

//bad
var dataId = node.dataset.id;
```

### Files/Directories

MUST be named in all lowercase and use dashes in place of spaces (ex. something.js, system-notifications.js)

```
|-- app/
| |-- core/
| |-- system-notifications/
| |-- module.js
| |-- system-notifications-directive.js
| |-- system-notifications-factory.js
```

### Variables/Object Members

Declare one variable per var and wherever they make sense.  It does not help readability and when let becomes available in browsers and NodeJS, it will be harder to refactor code to use let.

```javascript
//good
var one = 1;
var two = 2;

for(var x = 0; x < two; x += 1) {
  var three = 3;
}

//bad
var one, two, x, three;
two = 2;

for(x = 0; x < two; x += 1) {
  three = 3;
}
```

All variables MUST use camelCase

```javascript
//good
var createdDateTime;

//bad
var created_date_time;
```

Constants MUST use all upper case with underscore in place of spaces

```javascript
//good
var BASE_URL = 'http://www.example.com';

//bad
var baseRrl = 'http://www.example.com';
```

You should mark "private" variables/methods with a leading underscore as an *internal use* indicator.  It is understood that anything marked with a leading underscore should not be used out of that module.  There are 2 reasons for doing this.  First is that if you create a new object from a base object using a leading underscore to mark *internal use*, the new object has access to that data which can be needed sometimes.  The other use is for testing.  Outside of these 2 use cases, anything marked with a leading underscore should not be used out of that module.

```javascript
//good
var someObject = (function() {
  return {
    _internalData: 123,
    _internalMethod: function() {
     //...
    },
    //...
  };
})();
```

Names SHOULD be descriptive as possible without making the name too long

```javascript
//good
var query;

//bad
var q;
```

Variables SHOULD be named as nouns or states

```javascript
//good
var username;
var isActive;
```

### Function/Object Methods.

```javascript
//good
var isActive = function(){...};

//bad
var is_active = function(){...};
```

The exception to the rule is function constructors designed to be used with the new keyword, these functions MUST be pascal case.

```javascript
//good
var User = function(){...};
var loggedInUser = new User();

//bad
var user = function(){...};
var loggedInUser = new user();
```

Names SHOULD be descriptive as possible without making the name too long (ex. use doSomething() instead of dst())

```javascript
//good
var doSomething = function(){...};

//bad
var dst = function(){...};
```

Functions MUST NOT be reserved words or web browser built-in objects

Functions SHOULD be named as actions or states (ex. parseResponse(), user.isActive())

```javascript
//good
var parseResponse = function(){...};
var isActive = function(){...};
```

### Whitespace

Tabs are NOT permitted at all.

All code MUST be indented with 2 spaces.

```javascript
//good
if(a === b) {
  test = true;
}

//bad
if(a === b) {
    test = true;
}
```

There MUST not be any spaces on blank lines.

Blanks lines SHOULD be used to separate blocks of logic.

```javascript
//good
if(a === b) {
  test = true;
}

if(c === d) {
  test = false;
}

//bad
if(a === b) {
  test = true;
}
if(c === d) {
  test = false;
}
```

Commas MUST be followed by a space.

```javascript
//good
function add(one, two) {
  //...
};

//bad
function add(one,two) {
  //...
};
```

Ternary operators (inline-ifs) must be multi-lines

```javascript
//good
value = (data.length > 1)
  ? data[1] 
  : data[0];

//bad
value = (data.length > 1)?data[1]:data[0];
```

Semi-colons in for loops MUST be followed by a space.

```javascript
//good
for(x = 0; x < data.length; x += 1) {
  //...
}

//bad
for(x =0;x < data.length;x += 1) {
  //...
}
```

Operands and operators MUST be separated by spaces.

```javascript
//good
x = 1 + 2;

//bad
x=1+2;
```

There MUST be NO space between the conditional and opening parentheses.

```javascript
//good
for(x = 0; x < data.length; x == 1) {
  //...
}

//bad
for (x = 0; x < data.length; x == 1) {
  //...
}
```

There MUST be a space between the closing parentheses and the open braces.

```javascript
//good
for(x = 0; x < data.length; x == 1) {
  //...
}

//bad
for(x = 0; x < data.length; x == 1){
  //...
}
```

### Braces

All block structures including if, else, switch, try, catch, function, while, for, and so on MUST use braces around body.

```javascript
//good
if(user.isActive === true) {
  //...
}

//bad
if(user.isActive === true)
  //...
```

Opening braces MUST be at the end of the first line of the block statement.  Closing braces MUST be on a separate line and indented to match indentation of the opening brace's line.

```javascript
//good
if(user.isActive === true) {
  //...
}

//bad
if(user.isActive)
{
  //...
}

if(user.isActive === true) {
  test = true;}
```

### Conditionals

You MUST always specific the values for the conditional

```javascript
//good
if(user.isActive === true) {
  //...
}

//bad
if(user.isActive) {
  //...
}
```

You SHOULD use an exact conditional whenever possible

```javascript
//good
if(user.isActive === true) {
  //...
}

//bad
if(user.isActive == true) {
  //...
}
```

### Immediately-Invoked Function Expression (IIFE)

When creating an IIFE, the function inself should always be wrapped with-in parathenes and executing parathenes should be on the outside of the wrapping parathenes (this is to prevent possible weirdness which is detailed https://github.com/airbnb/javascript/issues/21#issuecomment-10203921).

```javascript
//good
(function() {
  //code...
})();

//bad
function() {
  //code...
}();

(function() {
  //code...
}());

```

### Documentation

General object, method, function, variable, etc... naming should be done in a way so that the code it pretty good at self documenting itself however if you find yourself write a complex piece of logic, please add inline documentation to the code.

#### Single/Multi-Lined Comments

All single and multi-lined comments should use double slashes and should contain no spaces at the beginning.

```javascript
//good

//this is a comments

//this is a multi-lined
//comment

//bad

// this is a commnet

/*
 *this is a mutli-lined
 *comment
 */ 

```

#### DocBlock

TBD

#### Special Comments

There are a few special comment that should be added when the situation arises:

- Hacks: When writing code that you know is hacky, piece add a comment starting with ```//HACK: ``` and then describe why you are writing hacky code
- Todo: If when writing code you think of something that should be done but can't do it then, add a comment starting with ```//TODO: ``` and the describe what need to be done
- Mocked Data: If you are mocking data in application code, add comment beginning with ```///MOCKEDDATA: ``` and describe why you are mocking the data (this does not apply to code speicific for UI unit testing mocks
- Performance: When writing code that is specific for performance reasons  add comment beginning with ```///PERFORMANCE: ``` and describe how the code helps with performance

### Testing

#### Unit Testing

All code should be testable through Mocha using Chai for assertions and Sinon for javascript mocking when needed.  All code that requires a DOM should use the jsdom library to mock the DOM.  The nock library should be used to mock api requests.

## SASS/CSS

### General

These are the rules that MUST be applied to all SASS/CSS that is written. These rules do NOT apply when modifying 3rd party libraries/scripts, in that case you SHOULD following the coding style code of whatever code you are work with (or follow the appeared style of the file if the code does not have a style guide). 

Line length MUST NOT exceed 160 characters 

You MUST never use inline styles 

```html
<!-- good -->
<span class="danger-text">...</span>

<!-- bad -->
<span style="color: red;">...</span>
```

All property definitions MUST end with a semi-colon.

```scss
/* good */
.selector {
  color: $white;
  font: 14px;
}

/* bad */
.selector {
  color: $white;
  font: 14px
}
```

All properties should have a space after the colon.

```scss
/* good */
.selector {
  color: $white;
}

/* bad */
.selector {
  color:$white;
}
```

All selectors should have a blank line before them for readability.

```scss
/* good */
.pill {
  border-radius: 999px !important;
    
  .svg-icon {
    vertical-align: sub;
  }
}

/* bad */
.pill {
  border-radius: 999px !important;
  .svg-icon {
    vertical-align: sub;
  }
}
```

You should avoid using `!important` but if you do have a need for it (there are time where it is ok to use), you must write a comment explaining why it is being used.

```scss
/* good */
width: 10px !important; /* overriding JS based styles */

/* bad */
width: 10px !important;
```

You should avoid unnecessary nesting when possible.

```scss
/* optimal */
.user-widget {
    .content {
        
    }

    //assuming li elements are styling the name in .user-widget (regardless of being in the .content)
    li {...}

    //assuming .name elements are styling the name in .user-widget (regardless of being in the .content or on a li)
    .name {...}

    //assuming .logout elements are styling the name in .user-widget (regardless of being in the .content or on a li)
    .logout {...}

    //assuming a elements are styling the name in .user-widget (regardless of being in the .content)
    a {...}
}

/* not optimal */
.user-widget {
    .content {
        li {
            ...

            &.name {...}

            &.logout {...}

            a {...}
        }
    }
}
```

### Mixins/Functions

Mixin/Function parameters should always be maps.  This makes it easier when you want to add or remove parameters.

```scss
//good
@function my-function($parameters: ()) {
  $parameters: map-merge((
    a: 1,
    b: 2
  ), $parameters);
  
  //...
}

//bad
@function my-function($a: 1, $b: )) {
  //...
}
```

### Files/Directories

MUST be named in all lowercase and use dashes in place of spaces.

```
|-- main.sass
|-- _system-notifications.sass
```

SASS files that will not be compiled into is own CSS file MUST start with an underscore.

```
|-- main.css
|-- main.sass
|-- _system-notifications.sass
```

### Naming

All classes and ids MUST be named with lowercase and dashes to separate words.

```html
<!-- good -->
<button id="user-submit-form" class="primary is-active"></span>

<!-- bad -->
<button id="user_submit_form" class="PRIMARY isActive"></span>
```

Form elements SHOULD have names that are camelCase so that they line up with however variables are names in JavaScript/PHP.

```html
<input id="type-id" type="text" name="typeId" />
<input id="is-admin-user" type="checkbox" name="isAdminUser" /> Admin User

<!-- bad -->
<input id="type-id" type="text" name="type-id" />
<input id="is-admin-user" type="checkbox" name="is_admin_user" /> Admin User
```

SASS Variables should be named with dashes to keep is consistent to how CSS properties are named.

```scss
/* good */
$color-text: #DDDDDD;

/* bad */
$colorText: #DDDDDD;
```

SASS variables should be named from least specific (property) to most specific (component).

```scss
/* good */
$color-header-help: #DDDDDD;

/* bad */
$help-header-color: #DDDDDD;
```

### Component Naming

Component naming following a modified version of BEM naming.  All components should have a unique name used as the class name.

```html
<div class="content-box">
</div>
``` 

An item of a component should be unique to that component and have its class name prefix with the component name and 2 underscores.

```html
<div class="content-box">
  <header class="content-box__header">
    Header
    <span class="content-box__close"></span>
  </header>
  <div class="content-box__content">Component Content</div>
</div>
```

Modifiers for the component of its items should be prefixed with a dash.

```html
<div class="content-box -no-header">
  <div class="content-box__content">Component Content</div>
</div>

<div class="content-box">
  <header class="content-box__header -with-icon -no-close">
    <span class="content-box__icon"></span>
    Header
  </header>
  <div class="content-box__content">Component Content</div>
</div>
```

Component item names should be made as unique as needed.  For example, if the entire component is only ever going to have 1 icon, then it `component-name__icon` should be the name of that icon however it it will possibly have a header and content icon then that items names should be `component-name__header-icon` and `component-name__content-icon`.

### SASS Variable Scoping

Global variables should be defined in a file called `_variables.scss`.  You can import other files however those files should only be defining variables and should end with `-variables.css`:

```
|-- _variables.scss
|-- _colors-variables.scss
```

Variables that belongs to a specific component should always be defined with the root scope to prevent those variables from being used globally (which will come with SASS 3.4).  These variables should also be prefixed with the component they belong to:

```scss
/* good */
.help {
  $help-color-button: #DDDDDD;
  
  /* ... */
}

/* bad */
$color-button: #DDDDDD;
  
.help {
  /* ... */
}
```

### Whitespace

Tabs are NOT permitted at all.

All code MUST be indented with 2 spaces

```scss
/* good */
.selector {
  color: $white;
}

/* bad */
.selector {
    color: $white;
}
```

There MUST not be any spaces on blank lines

Blank lines SHOULD be used to separate selector blocks

```scss
/* good */
.selector {
  color: $white;
}

.selector2 {
  color: $blue;
}

/* bad */
.selector {
  color: $white;
}
.selector2 {
  color: $blue;
}
```

### Braces

Opening braces MUST be at the end of the first line of the block statement.

```scss
/* good */
.selector {
  color: $white;
}

/* bad */
.selector
{
  color:$white
}
```

Closing braces MUST be on a separate line and indented to match indentation of the opening brace's line.

```scss
/* good */
.selector {
  color: $white;
}

/* bad */
.selector {
  color:$white}
```

### Documentation

You should alway document code that is not straight forward to understand or that is done in such a way for a specific reason even if it seems weird.

```scss
/* good */
.selector {
  /* ... */

  /* IE needs this the render properly */
  display: block !important;
}

/* bad */
body {
  /* body text color is black */
  color: #000000;
}
```

### Selectors

Avoid IDs whenever possible in selectors.

```scss
/* good */
.user-page .item {
}

/* bad */
#user-page .item {
}
```

### Properies

You SHOULD always use shorthand notion for properties that support where appropriate.

```scss
/* good */
body {
  padding: 5px;
}

body {
  padding: 5px 10px;
}

body {
  padding: 5px 6px 7px 8px;
}

/* bad */
body {
  padding-top: 5px;
  padding-right: 5px;
  padding-bottom: 5px;
  padding-left: 5px;
}

body {
  padding-top: 5px;
  padding-right: 10px;
  padding-bottom: 5px;
  padding-left: 10px;
} 

body {
  padding-top: 5px;
  padding-right: 6px;
  padding-bottom: 7px;
  padding-left: 8px;
}
```

## HTML

### General

All HTML should be using the HTML5 DOCTYPE and HTML5 features when possible.

All attribute value must be quoted.

```html
<!-- good -->
<span class="name">...</span>

<!-- bad -->
<span class=name>...</span>
```

Always use a ```<label>``` for each form field and use the ```for``` attribute to associate it to it's input.  ```<label>``` tags should also always have the pointer cursor. 

```html
<!-- good -->
<label for="name">Name</label>
<input id="name" type="text" name="name" />

<!-- bad -->
<label>Name</label>
<input id="name" type="text" name="name" />
```

Tables must not be use for layout, only used for tabular

### Formatting

When an element has more than 3 attributes or the line exceeds the maximum length, the first attribute should be place on the same line as the tag and each attribute should line up with the first attribute and be on it's own line for readability.

```html
<!-- good -->
<div nag-extend-text="lastNameOptions"
     data-id="textarea"
     data-model="extendTextResettableObject"
     data-type="textarea"
     data-model-property="lastName">
</div>

<!-- bad -->
<div nag-extend-text="lastNameOptions" data-id="textarea" data-model="extendTextResettableObject" data-type="textarea" data-model-property="lastName">
</div>
```
