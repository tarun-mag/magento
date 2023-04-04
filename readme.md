# Magento 2.4.1 Magento Commerce Cloud

This repository contains a sample Magento Commerce (on-premise) version 2.4.1 instance for you to deploy in the cloud. You must have an active Magento Commerce Cloud user license to use the example in this repository.

The example requires the use of [Composer](https://getcomposer.org/doc/) to load and manage dependencies and Magento vendor folders.

-  [Authentication](#authentication)
    -  [Authenticating in Docker](#authenticating-in-docker)
-  [Repository structure](#repository-structure)
-  [Developer documentation](#developer-documentation)

## Authentication

You must have an authentication key to access the Magento Commerce repository and to enable install and update commands for your Magento Commerce Cloud project. 
The following method is best to prevent accidental exposure of credentials, such as pushing an `auth.json` file to a public repository. If you plan to use Docker for your local development, then jump to the [Authenticating in Docker](#authenticating-in-docker) section.

To add authentication keys using an environment variable:

1.  In the _Project Web UI_, click the configuration icon in the upper left corner.

1.  In the _Configure Project_ view, click the **Variables** tab.

1.  Click **Add Variable**.

1.  In the _Name_ field, enter `env:COMPOSER_AUTH`.

1.  In the _Value_ field, add the following and replace `<public-key>` and `<private-key>` with your Magento Commerce Cloud authentication credentials.

    ```json
    {
       "http-basic": {
          "repo.magento.com": {
          "username": "<public-key>",
          "password": "<private-key>"
        }
      }
    }
    ```

1.  Select **Visible during build** and deselect **Visible at run**.

1.  Click **Add Variable**.

See [Adding Magento authentication keys](https://devdocs.magento.com/cloud/setup/first-time-setup-import-prepare.html#auth-json).

### Authenticating in Docker

You must have an `auth.json` file that contains your Magento Commerce authorization credentials in your Magento Commerce Cloud root directory.

1.  Using a text editor, create an `auth.json` file and save it in your Magento root directory.

1.  Replace <public-key> and <private-key> with your Magento Commerce authentication credentials.

    ```json
    {
      "http-basic": {
        "repo.magento.com": {
          "username": "<public-key>",
          "password": "<private-key>"
        }
      }
    }
    ```

1.  Save your changes to `auth.json` file and exit the text editor.

To use Docker for local development, see [Launching a Docker configuration](https://devdocs.magento.com/cloud/docker/docker-config.html).

## Repository structure

The following is a list of the specific files required for this example to work in the Magento Commerce Cloud:

```bash
.magento/
        /routes.yaml
        /services.yaml
.magento.app.yaml
auth.json
composer.json
magento-vars.php
php.ini
```

-  `.magento/routes.yaml`—redirects `www` to the naked domain and `php` application to serve HTTP.
-  `.magento/services.yaml`—sets up a MySQL instance, including Redis and ElasticSearch. 
-  `composer.json`—fetches the Magento Enterprise Edition and configuration scripts to prepare your application.

## Developer documentation

See the [Magento Commerce Cloud Guide](https://devdocs.magento.com/cloud/bk-cloud.html).

## Basic Coding Standard
Code MUST follow all rules outlined in [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md).

## Files
All PHP files MUST use the Unix LF (linefeed) line ending.

All PHP files MUST end with a single blank line.

The closing ?> tag MUST be omitted from files containing only PHP.

## Lines
There MUST NOT be a hard limit on line length.

The soft limit on line length MUST be 120 characters; automated style checkers MUST warn but MUST NOT error at the soft limit.

Lines SHOULD NOT be longer than 80 characters; lines longer than that SHOULD be split into multiple subsequent lines of no more than 80 characters each.

There MUST NOT be trailing whitespace at the end of non-blank lines.

Blank lines MAY be added to improve readability and to indicate related blocks of code.

There MUST NOT be more than one statement per line.

## Indenting
Code MUST use an indent of 4 spaces, and MUST NOT use tabs for indenting.
```
Using only spaces, and not mixing spaces with tabs, helps to avoid problems with diffs, patches, history, and annotations. The use of spaces also makes it easy to insert fine-grained sub-indentation for inter-line alignment.
```

## Keywords and True/False/Null

PHP [keywords](http://php.net/manual/en/reserved.keywords.php) MUST be in lower case.

The PHP constants ```true```, ```false```, and ```null``` MUST be in lower case.

## Magento Coding Standard

A set of Magento rules for [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) tool.

## Installation within a Magento 2 site

To use within your Magento 2 project you can use:

```bash
composer require --dev magento/magento-coding-standard
```
Due to security, when installed this way the Magento standard for phpcs cannot be added automatically. You can achieve this by adding the following to your project's ```composer.json:```

```bash
"scripts": {
    "post-install-cmd": [
      "([ $COMPOSER_DEV_MODE -eq 0 ] || vendor/bin/phpcs --config-set installed_paths ../../magento/magento-coding-standard/)"
    ],
    "post-update-cmd": [
      "([ $COMPOSER_DEV_MODE -eq 0 ] || vendor/bin/phpcs --config-set installed_paths ../../magento/magento-coding-standard/)"
    ]
}
```
## Installation for development

You can install Magento Coding Standard by cloning this GitHub repo:

```bash 
git clone git@github.com:magento/magento-coding-standard.git
cd magento-coding-standard
composer install
```

It is possible also to install a standalone application via [Composer](https://getcomposer.org/)

```bash
composer create-project magento/magento-coding-standard --stability=dev magento-coding-standard
```
## Verify installation
Command should return the list of installed coding standards including Magento2.
```bash
vendor/bin/phpcs -i
```
## Usage

Once installed, you can run phpcs from the command-line to analyze your code MyAwesomeExtension

```bash
vendor/bin/phpcs --standard=Magento2 app/code/MyAwesomeExtension
```
## Fixing issues automatically
Also, you can run phpcbf from the command-line to fix your code MyAwesomeExtension for warnings like "PHPCBF CAN FIX THE [0-9]+ MARKED SNIFF VIOLATIONS AUTOMATICALLY"

```bash
vendor/bin/phpcbf --standard=Magento2 app/code/MyAwesomeExtension
```

## Namespace and Use Declarations

When present, there MUST be one blank line after the ```namespace``` declaration.
When present, all ```use``` declarations MUST go after the ```namespace``` declaration.
There MUST be one ```use``` keyword per declaration.
There MUST be one blank line after the ```use``` block.

For example:

```bash
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...
```

## Classes, Properties, and Methods
The term "class" refers to all classes, interfaces, and traits.

## Extends and Implements

The ```extends``` and ```implements``` keywords MUST be declared on the same line as the class name.

The opening brace for the class MUST go on its own line; the closing brace for the class MUST go on the next line after the body.

```bash
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Lists of ```implements``` MAY be split across multiple lines, where each subsequent line is indented once. When doing so, the first item in the list MUST be on the next line, and there MUST be only one interface per line.

```bash
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```
## Properties
Visibility MUST be declared on all properties.

The ```var``` keyword MUST NOT be used to declare a property.

There MUST NOT be more than one property declared per statement.

Property names SHOULD NOT be prefixed with a single underscore to indicate protected or private visibility.

A property declaration looks like the following.

```bash
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```
## Methods
Visibility MUST be ```declared``` on all methods.

Method ```names``` SHOULD NOT be prefixed with a single underscore to indicate protected or private visibility.

Method ```names``` MUST NOT be declared with a space after the method name. The opening brace MUST go on its own line, and the closing brace MUST go on the next line following the body. There MUST NOT be a space after the opening parenthesis, and there MUST NOT be a space before the closing parenthesis.

A method declaration looks like the following. Note the placement of parentheses, commas, spaces, and braces:

```bash
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```



## License
Each Magento source file included in this distribution is licensed under the OSL-3.0 license.

Please see [LICENSE.txt](https://github.com/magento/magento-cloud/blob/master/LICENSE.txt) for the full text of the [Open Software License v. 3.0 (OSL-3.0)](http://opensource.org/licenses/osl-3.0.php).
