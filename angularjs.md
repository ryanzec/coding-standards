**These are old standards that have note been or will be updated as I longer do AngularJS development**


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
