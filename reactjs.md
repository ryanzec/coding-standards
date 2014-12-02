# ReactJS Coding Standards

When applying an attribute that can have a character separated value, use array instead of managing the string manually.

```javascript
//good
var cssClasses = ['one'];

if(something === true) {
  cssClasses.push('two');
}

return (
  <div className={cssClasses.join(' ')}>...</div>
);

//bad
var cssClasses = 'one';

if(something === true) {
  cssClasses .= ' two';
}

return (
  <div className={cssClasses}>...</div>
);
```

Props that are required should have a default value of `null` in the `getDefaultProps()` method so that it become an easy way to identify all possible props that an element can have.

Always wrap JSX is parathenes.

```javascript
//good
return (
  <div>
    <SomeElement />
  </div>
);

//bad
return <div>
  <SomeElement />
</div>;
```

While variables should only be PascalCase when they are a class and require the `new` keyword, react should always be required as `React` as that is what the JSX compiles to

```javascript
//good
var React = require('react/addons');

//bad
var react = require('react/addons');
```

React elements should also be required with PascalCase:

```javascript
//good
var AutoComplete = require('./auto-complete.component.jsx');

//bad
var autoComplete = require('./auto-complete.component.jsx');
```
