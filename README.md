ng-bs-daterangepicker
=====================

Angular directive for Dan Grossman's [bootstrap-daterangepicker](https://github.com/dangrossman/bootstrap-daterangepicker).

Demo: http://luisfarzati.github.io/ng-bs-daterangepicker

Installation
------------

Using bower:

```
bower install ng-bs-daterangepicker
```

Using npm:

```
npm install ng-bs-daterangepicker
```


How to use it
-------------

You should already have a bunch of scripts and CSS required for bootstrap-daterangepicker:

```
<link rel="stylesheet" type="text/css" href="bootstrap.min.css">
<link rel="stylesheet" type="text/css" href="daterangepicker-bs3.css">
<script type="text/javascript" src="jquery.min.js"></script>
<script type="text/javascript" src="bootstrap.min.js"></script>
<script type="text/javascript" src="moment.min.js"></script>
<script type="text/javascript" src="daterangepicker.js"></script>
<script type="text/javascript" src="angular.min.js"></script>
```

to the list above, you should add:

```
<script type="text/javascript" src="ng-bs-daterangepicker.js"></script>
```

Then, inject `ngBootstrap` in your application module:

```
angular.module('myApp', ['ngBootstrap']);
```

and then just add an `input` of type `daterange`:

```
<input type="daterange" ng-model="data.myDateRange">
```

The result object `$scope.data.myDateRange` has a `startDate` and `endDate` properties, which are instances of `moment()`.

Why we not directly use $scope.myDateRange, to understand this, we need to look at the way that AngularJS deals with inheritances of data values in scopes and how this is affected by the ng-model directive.

When you read the value of a property that is defined directly on the scope, AngularJS checks to see whether there is a local property in the controller’s scope and, if not, starts working its way up the scope hierarchy to see whether it has inherited one. However, when you use the ng-model directive to modify such a property, AngularJS checks to see whether the scope has a property of the right name and, if not, assumes you want to implicitly define it. The effect is to override the property value.

And sometimes we use <input type="daterange" ng-model="data.myDateRange"> insides ng-switch, ng-if directives, these directives creates new scope, if you use $scope.myDateRange as your ng-model, in such conditions your $scope.myDateRange will never be updated as your wish.

Then how can $scope.data.myDateRange handle this? This is because JavaScript implements what is known as prototype inheritance—a topic so dry and confusing that I am not going to attempt to explain it here. To ensure that ng-bs-daterangepicker will work at any condition, then define your data properties via an object like $scope.data.myDateRange.

### Implemented features so far

* `startDate`, `endDate`: are taken from the `ng-model` object;
* `minDate`, `maxDate`: mapped from `min-date` and `max-date` attributes;
* `dateLimit`: mapped from `limit` attribute;
* `format`: mapped from `format` attribute;
* `separator`: mapped from `separator` attribute.
* `ranges`: mapped from `ranges` attribute. Can be a JSON string or scoped object. (check daterangepicker for formatting)

Example with all above features:

```
<input
	type="daterange"
	ng-model="dates"
	min-date="2013-09-10"
	max-date="2013-09-25"
	limit="3 days"
	format="L"
	separator="/"
	ranges="{'Special Range':{'startDate': '2013-09-2', 'endDate': '2013-09-5'}}">
```

The `limit` attribute lets you specify a number and unit similarly as you would invoke `moment.duration()`.

### Features to be implemented:

* `timePicker*`
* `show*`
* other formatting options like `*Class` and stuff

### Build

You can run the tests by running

```
npm install
bower install
grunt
```

assuming you already have `grunt` installed, otherwise you also need to do:

```
npm install -g grunt-cli
```






[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/luisfarzati/ng-bs-daterangepicker/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

