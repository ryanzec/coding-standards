# Code Standards

These are the coding standards that I follow in the all of my coding whether it is front-end or back-end.

**_These standards are a living document and will change as I continue to develop code._**

## JavaScript

### General

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

If you which to keep a variable private, use a closure instead of prefixing with underscore

```javascript
//good
var someObject = (function() {
  var privateData;
  privateData = 123;

  return {
    //...
  };
})();

//bad
var someObject = (function() {
  return {
    _privateData: 123
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

If you which to keep a function private, use a closure instead of prefixing with underscore

```javascript
//good
var someObject = (function() {
  var doSomethingPrivate;
  doSomethingPrivate = function() {
    //...
  };
  
  return {
    //...
  };
})());

//bad
var someObject = (function() {
  return {
    _doSomethingPrivate: function() {
      //...
    },
    //...
  };
})();
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

Ternary operators (inline-ifs) MUST have spaces around both the ? and : operators.

```javascript
//good
value = (data.length > 1) ? data[1] : data[0];

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

#### DocBlock

TBD

#### Special Comments

There are a few special comment that should be added when the situation arises:

- Hacks: When writing code that you know is hacky, piece add a comment starting with ```//HACK: ``` and then describe why you are writing hacky code
- Todo: If when writing code you think of something that should be done but can't do it then, add a comment starting with ```//TODO: ``` and the describe what need to be done
- Mocked Data: If you are mocking data in application code, add comment beginning with ```///MOCKEDDATA: ``` and describe why you are mocking the data (this does not apply to code speicific for UI unit testing mocks
- Performance: When writing code that is specific for performance reasons  add comment beginning with ```///PERFORMANCE: ``` and describe how the code helps with performance

### Testing

#### Low Level Unit Testing (Karma)

All low level unit tests (non-DOM) MUST be written with the Mocha/Chai/Sinon libraries and executed with the Karma test runner.  The test files themselves should live in a folder called tests that is in the folder with the code it is testing.  The test files should be the same name of the files that it is testing along with .spec.js at the end.

```
|-- app/
| |-- components/
| | |-- core/
| | | |-- tests/
| | | | |-- session-factory.spec.js
| | | |-- session-factory.js
```

You must use the ```expect``` BDD style of the Chai library.

```javascript
//good
expect(test).to.be.a('string');

//bad
test.should.be.a('string');
```

When you need to test that an object deeply matches, you must use the ```to.deep.equal``` instead of ````to.eql```.  This is to make it clear when reading the test that you know it is doing a deep match.

```javascript
//good
expect(test).to.deep.equal(expectedObject);

//bad
expect(test).to.eql(expectedObject);
```

Describe's and it's should be typed in all lowercase.

```javascript
//good
describe('login controller', function(){
  //...
  it('should load login form', function() {
    //..
  });
});

//bad
describe('Login Controller', function(){
  //...
  it('Should load login form', function() {
    //..
  });
});
```

#### UI Unit Testing (DalekJS)

All DOM unit tests MUST be written with DalekJS.  All the tests should live in a folder called dalek that live at the root directory of the project.  The test files should be named in a way where the user can tell what the file is testing just by the name.

Anything that you might want to include in all the test files (variables, page objects, etc...), that should be put into the lib folder in the dalek folder.

```
|-- dalek/
| |-- lib/
| | |-- page-objects/
| | | |-- desktop-page.js
| | | |-- users-page.js
| | |-- variables.js
| |-- desktop.js
| |-- users-list.js
| |-- users-create-workflow.js
|-- web/
| |-- app/
| | |-- components/
| | | |-- core/
| | | |-- desktop/
| | | |-- users/
| | | |-- user-card/
|-- Dalekfile.json
```

##### Mocking Data

The UI unit tests should run against mocked in order to make sure they run as fast as possible.  The mocked data should in defined in a separate file called ui-testing-config.js and the should live at the root of your javascript application code.

```
|-- app/
| |-- components/
| |-- applicationl.js
| |-- ui-testing-config.js
```

Separating the file out allow you to only include that code when the application in in UI testing mode (which could be indicated by a query string parameter or a custom HTTP HEADER).

##### Page/Component Objects

The test files should never directly call any actions or assertions on the test object itself.  All interactions with the test object should be done through the use of a page or component object.  If you need a starting point for building page and component objects with DalekJS, use/look at this project:

https://github.com/ryanzec/dalek-angular-component-objects

So lets take a look at what a regular test file might look like for an application that uses angular:

```javascript
//file: /dalek/live-chat.js
var scripts = require('../client-scripts');

module.exports = {
  name: 'live chat component',

  'should open new window when live chat is clicked': function(test) {
    test.open('/home?uiTestingMode=true')
    .waitFor(scripts.angular);
    .click('.page > header .support .live-chat')
    .waitFor(scripts.angular);
    .toWindow('live-chat-window')
    .assert.url().to.match(/livechat\.example\.com/, 'live chat window opened')
    .toParentWindow()
    .done();
  }
};
```

Now lets rewrite this test with the assumption we are using the base system mentioned above:

```javascript
//file: /dalek/lib/objects/components/live-chat.js
var BaseComponent = require('../base-component');

var LiveChatComponent = BaseComponent.extend({
  initialize: function(test, baseSelector) {
    this.baseSelector = baseSelector; 
    this.selectors = {
      liveChat: '.live-chat',
    };

    BaseComponent.initialize.call(this, test);
  },

  clickLiveChat: function() {
    this.test.click(this.getSelector('liveChat'));
    this.waitForAngular();
  },
});

module.exports = LiveChatComponent;


//file: /dalek/lib/objects/pages/home.js
var BasePageObject = require('../base-page-object');
var LiveChatComponent = require('../components/live-chat');

var HomePage = BasePageObject.extend({
  initialize: function(test, urlAppend) {
    this.baseUrl = '/home?uiTestingMode=true';
        
    BasePageObject.initialize.call(this, test, urlAppend);
  },
  
  getLiveChatComponent: function() {
    return LiveChatComponent.new(this.test, '.page > header .support');
  },
    
  liveChatWindowOpened: function() {
    this.test.toWindow('live-chat-window');
    this.test.assert.url().to.match(/livechat\.example\.com/, 'live chat window opened')
    this.test.toParentWindow();
  },
});

module.exports = HomePage;


//file: /dalek/live-chat.js
var HomePage = require('./lib/objects/pages/home');

module.exports = {
  name: 'live chat component',

  'should open new window when live chat is clicked': function(test) {
    var homePage = HomePage.new(test);
    var liveChatComponent = homePage.getLiveChatComponent();
    
    liveChatComponent.clickLiveChat();
    
    homePage.liveChatWindowOpened();
    
    homePage.done();
  }
};
```

When looking at the just the test, the biggest advantage that can be seen is it is a lot clearer on what the test is doing.  While the test name clearly states what functionality is being tested, now you can clearly see what it is doing in order to test the functionality.  There are other advantages that might not be as apparent with this example.

Using component objects make it easier to test the same functionality that might live on different pages.  If we take the live chat component example, that might live on every page however there might be an issue with it work on a specific page.  All you have to do is include the LiveChatComponent object in the other page test that is having issues so you don't have to duplicate all test code for that component.

This structure also makes it so all your selectors are stored at the top of the page/component objects.  This makes it easy to find selectors and make changes if needed.

You also have a place to normalize functionality that your application might need, for example with an AngularJS application.  In order to be able to test an AngularJS without having a bunch of ```wait()```'s or ```waitForElement()```'s is to be able to hook into AngularJS's ```$browser.notifyWhenNoOutstandingRequests()``` method.  Now you can have a place to normalize calling that so that if it changes, you can change one place instead of having it littered all across your test files.

While there this more code in this structure, it helps improve the stability and maintainability of tests which is more important.

## AngularJS

All the javascript standard apply to AngularJS code.  This section only contains standards that relate directly to AngularJS functionality.

### Structure

AngularJS code should be structured into code that make re-usability easy.  Code should to organized into as small as possible components that can be easily copied from one application to another.  You should also move any code that can live as a plain javascript library and would be useful in multiple situations out of any AngularJS module.

For example, say you have a form max value validation directive that makes sure a input numeric value does not exceed a certain value.  Instead of doing the validation of the value directly inside the validation directive, you should extract the validation part of the code into a plain javascript library that just does data validation and then use that inside of the validation directive.  This way you can use the same data validation logic in multiple locations.

There is also a component an application can have that is called ```core``` which is to group items that are core to the application but are not generic enough to be moved into there own component or that you want to moved from the application.js file into its own file to make the code more readable (in this case, by making the files smaller).

```javascript
//file app/components/core/globals-config.js
//this code could just be part of the applications.config however moving into its own file
//can make it easier to find code
angular.module('app.core')
.config([
    'nagGlobalsProvider',
    function(nagGlobalsProvider) {
        nagGlobalsProvider.addConstant('BASE_URL', 'http://www.example.com');
        nagGlobalsProvider.addConstant('BASE_REST_URL', '/api');
    }
]);
```

The main component folder can have javascript files and an assets folder for any non-javascript related assets (templates, SASS, font files, images, etc...).

```
|-- index.html
|-- app/
| |-- application.js
| |-- core/
| | |-- module.js
| | |-- globals-config.js
| |-- users/
| | |--assets/
| | | |-- templates/
| | | | |-- list.html
| | | | |-- view.html
| | | |-- styles/
| | | | |-- _styles.scss
| | | | |-- _list.scss
| | | | |-- _view.scss
| | |-- module.js
| | |---list-controller.js
| | |---view-controller.js
| |-- issues/
| | |-- assets/
| | | |-- templates/
| | | | |-- list.html
| | | | |-- view.html
| | | |-- styles/
| | | | |-- _styles.scss
| | | | |-- _list.scss
| | | | |-- _view.scss
| | | |-- fonts/
| | | | |-- fonts.eot
| | |-- module.js
| | |-- list-controller.js
| | |-- view-controller.js
```

### UI Router

The default router provider by AngularJS is ok for simple things but it can quickly become an issue as the complexity of an application grows.  For this reason, all AngularJS projects should be using the [UI Router](https://github.com/angular-ui/ui-router).

#### State Naming

When naming states with [UI Router](https://github.com/angular-ui/ui-router) you must use the dot notation, this make inheritance more seamless.

The main application module should have a state define like ```app```.  This would be the location where you would place resolve that needs to happen application wide (like verifying the users session is still valid) and define application level template that don't change often (like headers, footers, navigation, etc...).

```javascript
//file app/application.js
angular.module('app', [
  'app.core'
])
.config([
  '$stateProvider',
  function($stateProvider) {
    $stateProvider
    .state('app', {
      url: '',
      views: {
        '': {
          template: '/app/components/core/assets/templates/module-wrapper.html'
        },
        'header': {
          templateUrl: 'app/components/core/assets/templates/header.html'
        },
        'footer': {
          templateUrl: 'app/components/core/assets/templates/footer.html'
        }
      }
    });
  }
]);
```

When defining a component that is going to have routable controllers, then it should setup the component route (if needed) when defining the component's module.

```javascript
//file app/components/users/module.js
angular.module('app.users', [])
.config([
  '$stateProvider',
  function($stateProvider) {
    $stateProvider
    .state('app.users', {
      url: '/users',
      abstract: true,
      views: {
        '': {
          templateUrl: 'app/components/core/assets/templates/module-wrapper.html'
        }
      }
    });
  }
]);
```

So for example, if we had a users list controller, that state would be named ```app.users.list``` which would inherit from the ```app.users``` and ```app``` states.

```javascript
//file app/components/users/list-controller.js
angular.module('app.users')
.config([
  '$stateProvider',
  function($stateProvider) {
    $stateProvider
    .state('app.users.list', {
      url: '/list',
      views: {
        '': {
          templateUrl: 'app/components/users/assets/templates/list.html',
          controller: 'UsersListCtrl'
        }
      }
    });
  }
])
.controller('HomeCtrl', ...);
```

### Modules

All modules are defined in a single module.js file for a given component.  This is done so that when you are defining the individual items for the components, those files can assume the module they belong to is already defined and you can skip the process of checking to see if the module is already define (which would have to be done since getting the module is different based on whether or not it already exists).

An exception to this in the top level application module which should be define in a application.js file at the top level of where your application code lives.

```
|-- index.html
|-- app/
| |-- application.js **application module**
| |-- components/
| | |-- users/
| | | |-- module.js **component module**
```

### Config/Run

An AngularJS module and have ```config()``` and ```.run()``` definitions.  These definitions should be located when first declaring the module in the module file (except for routes).

```javascript
//file app/components/users/module.js
angular.module('app.users', [
  'app.users'
])
.config(...)
.run(...);
```

If you want, you can also move any ```config()``` or ```run()``` into there own files.  These files should end with ```-config.js```.

```javascript
//file app/components/core/globals-config.js
angular.module('app.core', [
    'nag'
])
.config([
    'nagGlobalsProvider',
    function(nagGlobalsProvider) {
        nagGlobalsProvider.addConstant('BASE_URL', 'http://www.example.com');
        nagGlobalsProvider.addConstant('BASE_REST_URL', '/api');
    }
]);
```

The definition of routes should be done within each controller file.

### Events

Event driven programming is favored over promise/callback based programming in most cases.

An example of a case where event driven programming make sense if for a directive that triggers focusing of an input element.  Maybe you want to focus an element after a piece of data has loaded.  Since you don't want to access the DOM logic directly in the data loading code, once the data is loaded you just trigger the focus event and if an element has that directive, it will focus.

In a more complex example, lets say you have form reset directive and an extend text directive (like with auto completing, tagging, etc...).  When you reset a form, the extend text directive needs to be able to hook into that event so that so it can clear the element that is modifies but that would not be reset by the form reset since it is only assuming regular form elements.  While you could grab the form reset directive's controller and add callback in that manner, I feel events is a cleaner way to go about this.

Events should be attached to the ```$rootScope``` and should use ```$rootScope.$emit()``` to trigger events.

You should trigger event where they need to be triggered.  Events that you are listening to should be called in whatever item needs to be listening to them.  It is important to remember to detach any events you might be listening to when directives or controller are destroyed so listen on the ```$destroy``` event to properly detach listeners.

Application wide events can be attached in the ```application.js``` file or an ```events-config.js``` file in the core component.

Events should be named with the name of the component in PascalCase and the name of the event in camelCase separated by a forward slash (/).  Application wide events should use ```Application``` as the component name part of the event name.  So if we wanted an application wide rest error event, the name of the event would be ```Application/restError```.  If there was a dashboard data poll event for the desktop component, the name of the event would be ```Desktop/dashboardDataPoll```.

```javascript
//file app/components/core/events-config.js
angular.module('of.core', [
  'nag'
])
.run([
  '$rootScope',
  'nagGlobals',
  function($rootScope, nagGlobals) {
      $rootScope.$on('Application/restError');
  }
]);
```

There there will be times where you will need to separator the same event that can happen on multiple element in the same page.  For example, you can have a form reset event but have multiple form on a single page.  To handle this you need a unique identifier and add that to the component part of the name wrapping it in square brackets (and making sure it is camcelCase).  Directives should use the attribute data-id to get the unique identifier.  You'll end up with an event name like ```NagForm[userCreate]/reset```.

```html
<!-- this would trigger an reset of 'NagForm[userCreate]/reset' -->
<form data-id="user-create">
  ...
</form>
```

If you are going to handle a certain event (like a formError event) generally in a consistent way, you can create a event handlers factory for the component.

```
|-- app/
| |-- components/
| | |-- users/
| | | |-- module.js
| | | |-- event-handlers-factory.js
| | | |-- create-controller.js
```
```javascript
//file app/components/users/event-handers-factory.js
angular.module('of.users', [])
.factory('usersEventHandlers', [
  function() {
    return {
      formError: function(formData) {
        //generic form error handling code
      }
    };
  }
]);
```
```javascript
//file app/components/users/create-controller.js
//some where in the logic
var detachFormErrorFunction = $rootScope.$on('Users[userCreate]/createFormError', function(formData) {
  usersEventHandlers.formError(formData);
});
```

### Controllers

Every controller should be in its own file and the name of the file should end with ```-controller.js```.  The name given to the controller in the code should end with Ctrl.

```
|-- index.html
|-- app/
| |-- components/
| | |-- users/
| | | |-- module.js
| | | |-- list-controller.js
| | | |-- view-controller.js
```

Each controller is probably going to have at least 1 route associated with it.  The way to define the routes is in the controller file itself.

```javascript
//file list-controller.js
angular.module('app.users')
.config([
  '$stateProvider',
  function($stateProvider) {
    //route defined within the controller file
    $stateProvider
    .state('app.users.list', {
      url: '/list',
      views: {
        '': {
          templateUrl: 'app/components/users/assets/templates/list.html',
          controller: 'UsersListCtrl'
        }
      }
    });
  }
])
.controller('UsersListCtrl', [
  '$scope',
  function($scope) {
    //your code
  }
]);
```

### Directives

Directives should be split into two parts, the directive and the directive controller.  The file with the directives should end with ```-directive.js``` and the file with the directive controller should end with ```-controller.js``` just like other controllers.  Directive controller names should end with ```DCtrl``` to distinguish them from regular regular controllers. 

```
|-- index.html
|-- app/
| |-- components/
| | |-- users/
| | |-- user-card
| | | |-- assets/
| | | | |-- templates/
| | | | |-- styles/
| | | | | |-- _styles.scss
| | | | | |-- _user-card.scss
| | | |-- module.js
| | | |-- user-card-controller.js
| | | |-- user-card-directive.js
```

#### Directive Controller

The directive controller is responsible for attaching all non-DOM related functionality to the $scope.  This is done so that unit tests can easily be written against the directive controller without having to mock HTML which is not allowed in Karma unit tests (because of standards and not technical limitations of DalekJS).

#### Directive

The directive is responsible for all DOM related functionality.

### Services/Factories/Providers

When you create a service, you should only ever use the ```factory()``` or the ```provider()``` methods.  While there is also the ```service()``` method for creating services, keeping the ways to creating services down to 2 will help keep coding consistent.

When creating a service that will not need to be able to be injected in to the ```config()``` method of a module, use the ```factory()``` method.  When creating a service in this method, the file name that defines the service should end with ```-factory.js```.

When creating a service that will need to be able to be injected in to the ```config()``` method of a module, use the ```provider()``` method.  When creating a service in this method, the file name that defines the service should end with ```-provider.js```.

```
|-- index.html
|-- app/
| |-- application.js
| |-- components/
| | |-- users/
| | | |-- module.js
| | | |-- service1-factory.js
| | | |-- service2-provider.js
```

### Filters

Filters should be defined as their own independent component.  The component folder and file should end with ```-filter``` and ```-filter.js``` respectively.

The folder has the ```-filter``` in its name to be able to easily identify filters.

```
|-- index.html
|-- app/
| |-- application.js
| |-- components/
| | |-- users/
| | |-- date-format-filter
| | | |-- module.js
| | | |-- date-format-filter.js
```

### Values/Constants

Values and Constants should be defined once per component in a file called ```values.js```.

```
|-- index.html
|-- app/
| |-- application.js
| |-- components/
| | |-- users/
| | | |-- module.js
| | | |-- values.js
```

### Tests

#### Karma Tests

The following components will always have Karma tests and not Dalek tests since they never directly deal with the UI:

- services
- filters
- page/directive controllers

#### DalekJS Tests

The following components will always have DalekJS tests and not Karma tests since they directly deal with the UI:

- directives

You should also have DalekJS tests for the output of the application (the output of the page controllers).

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

```css
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

```css
/* good */
.selector {
  color: $white;
}

/* bad */
.selector {
  color:$white;
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

### Whitespace

Tabs are NOT permitted at all.

All code MUST be indented with 2 spaces

```css
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

```css
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

```css
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

```css
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

```css
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

```css
/* good */
.user-page .item {
}

/* bad */
#user-page .item {
}
```

### Properies

You SHOULD always use shorthand notion for properties that support where appropriate.

```css
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
