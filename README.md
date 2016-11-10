This repo shows a bug in the smarty template engine. 

(Tested Commit e867ae125e95ff629eb3b748eb222200f50e1769)

Link to the issue: https://github.com/smarty-php/smarty/issues/312

## Usage

```
composer install
composer test
```

## Changes

`Child`-class now has a custom function

```php
    public function getText()
    {
        return $this->getHTML();
    }
```

and `child.tpl` calls it

```
{extends 'base.tpl'}{block name=elementContent}{$e->getText()}{/block}
```

## Output

The output will be something like: 

```

$ composer test
> phpunit ./InheritanceTest.php
PHPUnit 5.6.2 by Sebastian Bergmann and contributors.

..3
Fatal error: Call to undefined method BaseClone::getText() in <PATH>\smarty-bug\templates_c\4782f9d86a65ebee34d6e75a89ca06f82421c857_0.file.child.tpl.php on line 39

Call Stack:
    0.0002     130048   1. {main}() <PATH>\smarty-bug\vendor\phpunit\phpunit\phpunit:0
    0.0050     489776   2. PHPUnit_TextUI_Command::main() <PATH>\smarty-bug\vendor\phpunit\phpunit\phpunit:47
    0.0050     494856   3. PHPUnit_TextUI_Command->run() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\TextUI\Command.php:115
    0.0208    1802512   4. PHPUnit_TextUI_TestRunner->doRun() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\TextUI\Command.php:185
    0.0252    2092704   5. PHPUnit_Framework_TestSuite->run() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\TextUI\TestRunner.php:465
    0.0319    2103480   6. PHPUnit_Framework_TestSuite->run() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\Framework\TestSuite.php:753
    0.1055    4588056   7. PHPUnit_Framework_TestCase->run() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\Framework\TestSuite.php:753
    0.1055    4588024   8. PHPUnit_Framework_TestResult->run() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\Framework\TestCase.php:909
    0.1056    4588736   9. PHPUnit_Framework_TestCase->runBare() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\Framework\TestResult.php:701
    0.1060    4629360  10. PHPUnit_Framework_TestCase->runTest() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\Framework\TestCase.php:954
    0.1061    4629968  11. ReflectionMethod->invokeArgs() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\Framework\TestCase.php:1103
    0.1061    4629984  12. InheritanceTest->testInheritance() <PATH>\smarty-bug\vendor\phpunit\phpunit\src\Framework\TestCase.php:1103
    0.1084    4649464  13. Smarty_Internal_TemplateBase->fetch() <PATH>\smarty-bug\InheritanceTest.php:55
    0.1085    4649592  14. Smarty_Internal_TemplateBase->_execute() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_internal_templatebase.php:107
    0.1085    4668208  15. Smarty_Internal_Template->render() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_internal_templatebase.php:216
    0.1085    4668240  16. Smarty_Template_Compiled->render() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_internal_template.php:185
    0.1085    4668240  17. Smarty_Template_Resource_Base->getRenderedTemplateCode() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_template_compiled.php:172
    0.1085    4668272  18. content_58248f296f67c8_15065690() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_template_resource_base.php:128
    0.1085    4668456  19. Smarty_Internal_Runtime_Inheritance->instanceBlock() <PATH>\smarty-bug\templates_c\99c6af3931605fad329165443cdd8b4397e1d9ca_0.file.base.tpl.php:28
    0.1085    4668936  20. Smarty_Internal_Runtime_Inheritance->process() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_internal_runtime_inheritance.php:144
    0.1085    4668936  21. Smarty_Internal_Runtime_Inheritance->process() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_internal_runtime_inheritance.php:172
    0.1085    4668904  22. Smarty_Internal_Runtime_Inheritance->callBlock() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_internal_runtime_inheritance.php:170
    0.1085    4668952  23. Block_223358248f297456b6_02976359->callBlock() <PATH>\smarty-bug\vendor\smarty\smarty\libs\sysplugins\smarty_internal_runtime_inheritance.php:238

Script phpunit ./InheritanceTest.php handling the test event returned with an error
```
