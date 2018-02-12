---
layout: default
group: mftf
title: Update the Magento Functional Testing Framework and pull new tests
version: 2.2
github_link: magento-functional-testing-framework/release-2/update.md
functional_areas:
 - Testing
mftf-release: 2.0.2
---

_This topic corresponds to the MFTF {{page.mftf-release}} release._
{: style="text-align: right"}

## Overview

Magento tests and the Framework are stored in different repositories.

Magento tests are stored in the same repository as the Magento code base.
When you pull changes in the Magento code, you're potentially pulling corresponding tests .

The Framework is installed separately as a dependency using Composer.
When pulling the latest Magento code, you need to update the corresponding Composer dependencies in the `magento2/dev/tests/acceptance` directory. This ensures that the MFTF is up to date.

## Update the MFTF

* When you updated Magento, verify that the Magento [WYSIWYG settings] and [Security settings] are set appropriately.

* Go to the `magento2/dev/tests/acceptance` directory:

```bash
$ cd dev/tests/acceptance
```

* Update your own tests, including data, metadata etc, if they contain tags that are unsupported anymore in newer version. Check details about backward incompatible changes in [Changelog], and learn documentation of new MFTF release.

* Run `composer update` to get the latest framework version:

```bash
$ composer update
```

* Generate newly pulled tests:

```bash
$ vendor/bin/robo generate:tests
```

<!-- LINK DEFINITIONS -->

[Changelog]: ../changelog.html

[`develop`]: https://github.com/magento/magento2-functional-testing-framework
[Security settings]: getting-started.html#security-settings
[WYSIWYG settings]: getting-started.html#wysiwyg-settings

<!-- Abbreviations -->

*[MFTF]: Magento Functional Testing Framework