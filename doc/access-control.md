Access-Control
=======

Introduction
-------

This library is meant to perform access control with precise logic.

Using policy rules, we can analyze users, resources and environment attributes to determine if an user is able to perform an action.

Once our policy rules are defined, we can simply check if a policy rule is enforced in a given case.

Usage
---

```php
use PhpAbac\Abac;

$check = $abac->enforce('medical-reports-access', $userId, $reportId);
```

```$check``` have two possible values :

* ```true```, meaning that all the policy rules required attributes are matched for the given user and resource.
* An array of slugs, associated to the attributes which did not match.

Dynamic Attributes
------------------

In some cases, an attribute won't be expected to match a static value, but a dynamic value depending on the case.

In these cases, the library allows you to give an array as fourth argument of the enforce() method.

This associative array will contain the targetted attribute's slug as key and the dynamic value.

For example, it can be useful to check the ownership of a resource :

```php
use PhpAbac\Abac;

$check = $abac->enforce('medical-reports-access', $userId, $reportId, [
	'report-author' => $userId
]);
```

***To make this work, the expected value stored in the ```PolicyRuleAttribute``` object must be ```"dynamic"```***