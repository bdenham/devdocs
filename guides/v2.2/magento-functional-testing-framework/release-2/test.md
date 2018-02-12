---
layout: default
group: mftf
title: Tests in the Magento Functional Testing Framework
version: 2.2
github_link: magento-functional-testing-framework/release-2/test.md
functional_areas:
 - Testing
mftf-release: 2.0.2
---

_This topic corresponds to the MFTF {{page.mftf-release}} release._
{: style="text-align: right"}

## Overview

Test cases in the MFTF are defined in XML as [tests][test].
Tests is a [Codeception test container][codeception] that contains multiple individual tests with test metadata and before/after actions.
Tests in the MFTF are considered as a sequence of actions with associated parameters.
Any failed [assertion] within a test fails the test.

{% include note.html
type="info"
content="`<before>`and `<after>` hooks are not global within `<tests>` like in MFTF 1.0.
They only apply to the `<test>` they are declared under." %}

{% include note.html
type="info"
content="The steps in `<after>` are run in both successful **AND** failed test runs." %}

The following diagram demonstrates XML structure of a test case in the MFTF:

{% include_relative img/test-dia.svg %}

## Format

```xml
<?xml version="1.0" encoding="UTF-8"?>

<tests xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:noNamespaceSchemaLocation="../../../../../../vendor/magento/magento2-functional-testing-framework/src/Magento/FunctionalTestingFramework/Test/etc/testSchema.xsd">
        <test name="">
            <annotations>
                <!-- TEST ANNOTATIONS -->
            </annotations>
            <before>
                <!-- ACTIONS AND ACTION GROUPS PERFORMED BEFORE THE TEST -->
            </before>
            <after>
                <!-- ACTIONS AND ACTION GROUPS PERFORMED AFTER THE TEST -->
            </after>
            <!-- TEST ACTIONS, ACTION GROUPS, AND ASSERTIONS-->
        </test>
    </tests>
</config>
```

## Principles

* All names within the framework are in the CamelCase format
* Each action and action group has its own identifier `<stepKey>` to be able to reference on it
* A test may have any number of [assertions][assertion], at any point within the `<test>`
* File name and `<test>` name are equal.

Multiple <test> tags per XML file can be confusing and hard to find/organize.
We generate one _test.php_ file per <test> tag provided.
This is not a hard requirement and we obviously support both.

## Reference

Reference documentation with details about XML elements that may be used in tests.

### tests {#tests-tag}

A container for multiple tests. Logically, it is a group of test methods that define test flows within a test case.

It MUST contain at least one [`<test>`][test].

***
***

### test {#test-tag}

A set of steps including [actions][action] and [assertions][assertion].
Logically, it is a sequence of test steps that define test flow within a test method.


Attribute|Type|Use|Description
---|---|---|---
name|string|optional| Test identifier used while merging.
remove|boolean|optional|Set `true` to remove the test when merging.

It MAY contain [`<annotations>`][annotations], [`<before>`][before], [`<after>`][after], any [action], [`<actionGroup>`][action group tag]

***
***

### annotations {#annotations-tag}

Annotations are supported by both [Codeception][codeception] and [Allure].
Codeception annotations typically provide metadata. Also, they are able to influence test selection.
Allure annotations provide metadata for reporting.

Read about annotations in a separate topic [Annotations][annotations].

***
***

### before {#before-tag}

Wraps steps to perform before the [test].

It MAY contain the following child elements:

 * any [action]
 * [`<actionGroup>`][action group tag]

***
***

### after {#after-tag}

Wraps steps to perform after the [test].
The steps are run in both successful **AND** failed test runs.

It MAY contain:

 * any [action]
 * [`<actionGroup>`][action group tag]

***
***

### actionGroup {#actiongroup-tag}

Calls a corresponding [action group].

Attribute|Type|Use|Description
---|---|---|---
ref|string|required|Reference to the required action group by its `name`.
stepKey|string|required| Identifier of the element within `<test>`.
before|string|optional| `<stepKey>` of an action or action group that must be executed next while merging.
after|string|optional| `<stepKey>` of an action or action group that must be executed one step before the current one while merging.

It MAY contain [`<argument>`][argument]

***
***

### argument {#argument-tag}

Sets an argument that is used in parent [`<actionGroup>`][action group tag].

Attribute|Type|Use
---|---|---
name|string|optional| Name of the argument.
value|string|optional| Value of the argument.

Learn more in [Action groups][action group].

<!-- LINKS DEFINITIONS -->

[action]: ./test/actions.html
[action group]: ./test/action-groups.html
[action group tag]: #actiongroup-tag
[after]: #after-tag
[annotations]: ./test/annotations.html
[argument]: #argument-tag
[assertions]: ./test/assertions.html
[before]: #before-tag
[tests]: #tests-tag
[test]: #test-tag

[Allure]: https://github.com/allure-framework/
[codeception]: http://codeception.com/docs/07-AdvancedUsage

<!-- Abbreviations -->

*[MFTF]: Magento Functional Testing Framework
