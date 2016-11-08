This repo shows a bug in the smarty template engine. (v3.1.30)

Link to the issue: 

## Usage

```
composer install
composer test
```

## Output

The output will be something like: https://github.com/smarty-php/smarty/issues/312

```
$ composer test
> phpunit ./InheritanceTest.php
    PHPUnit 5.6.2 by Sebastian Bergmann and contributors.

..F.FF                                                              6 / 6 (100%)

Time: 78 ms, Memory: 3.25MB

There were 3 failures:

1) InheritanceTest::testInheritance with data set #2 (array(Child Object (...), Child Object (...), BaseClone Object (...)), array('1 Child', '2 Child', '3 BaseClone'))
Failed asserting that two strings are identical.
--- Expected
+++ Actual
@@ @@
-3 BaseClone
+2 Child

...\smarty-bug\InheritanceTest.php:51

2) InheritanceTest::testInheritance with data set #4 (array(Child Object (...), Child Object (...), BaseClone Object (...), Child Object (...)), array('1 Child', '2 Child', '3 BaseClone', '4 Child'))
Failed asserting that two strings are identical.
--- Expected
+++ Actual
@@ @@
-3 BaseClone
+2 Child

...\smarty-bug\InheritanceTest.php:51

3) InheritanceTest::testInheritance with data set #5 (array(BaseClone Object (...), Child Object (...), Child Object (...), BaseClone Object (...)), array('1 BaseClone', '2 Child', '3 Child', '4 BaseClone'))
Failed asserting that two strings are identical.
--- Expected
+++ Actual
@@ @@
-4 BaseClone
+3 Child

...\smarty-bug\InheritanceTest.php:51

FAILURES!
Tests: 6, Assertions: 18, Failures: 3.
Script phpunit ./InheritanceTest.php handling the test event returned with an error

```

The tests #2, #4 and #5 currently fail, but shouldn't.