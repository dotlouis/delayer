# delayer
Angular service to prevent the user from spamming UI elements (toggles, buttons, searchbars, refreshes)


### Installation

`bower install dot-louis/delayer`

### Usage

1. Add it to your project dependencies

`angular.module('myapp',['delayer'])`

2. Add it to your HTML

`<script src="bower_components/delayer/delayer.service.js"></script>`

3. Inject it in the controller/service of your choice to use it

```JS
angular.module('myapp').controller('$scope','delayer', function(){

    // define the delayed switch here
    $scope.mySwitch = new delayer([
        function on(){
            // do something when switched on
            // for example send a network request
        },
        function off(){
            // do something when switched off
        }
    ]);

    // to toggle it simply call:
    $scope.mySwitch.toggle();

});
```
### API

- `new Delayer([functions], options)` **constructor** returns a delayer object

The array of function is mandatory and must have at least one function.
If multiple functions, they must be defined in the order they will be called.

```JS
// options are optionals.
// here are the defaults
options = {
    delay: 2000, // the delayer's timeout
    block: this.fns.length > 1 ? false : true // Wether to block subsequent call until the delay is passed
}
```


- `.toggle(params)` return a promise with the result of the called function

params are arguments that can be passed to the called function
