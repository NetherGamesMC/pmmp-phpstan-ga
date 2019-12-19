# GithubAction for PHPStan

**NETHERGAMES is currently providing reasonable support for this through the issue tracker. However, please note we have the right to deny any support as this is provided in the public domain without any support implied.**

**Credits for the Docker-Image goes to Oskar Stark - thank you for what you've done!**

## Usage

You can use it as a Github Action like this:

_.github/workflows/test.yml_
```
on: [push, pull_request]
name: Test
jobs:
  phpstan:
    name: PHPStan
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: PHPStan
      uses: docker://oskarstark/phpstan-ga
      with:
        args: analyse src/
```

_to use a specific level:_
```diff
on: [push, pull_request]
name: Test
jobs:
  phpstan:
    name: PHPStan
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: PHPStan
      uses: docker://oskarstark/phpstan-ga
      with:
-        args: analyse src/
+        args: analyse src/ --level=5
```

_to use a phpstan.neon.dist configuration file:_

just drop the `phpstan.neon.dist` in your repository root and it will be taken into account.

**Requirements:**

You're by default required to autoload your classes. In the case of PMMP, we recommend using `composer.json` to autoload the classes like so:

```json
{
    "name": "vendorname/projectname",
    "description": "your description",
    "type": "project",
    "authors": [
        {
            "name": "YourName"
        }
    ],
    "minimum-stability": "stable",
    "require": {
        "php": ">=7.2.0",
        "pocketmine/math": "0.2.3"
    },
    "autoload": {
        "classmap": [
            "path/to/class.php",
            "path/to/class/two.php",
            "path/to/class/three.php"
        ]
    },
    "prefer-stable": true,
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/pmmp/Math"
        }
    ]
} 
```

This allows you to autoload the PMMP repositories and it's dependancies by default. Although it's recommended that if you're dependant on a specific library, specifically add that in your `require` section. You can also autoload with PSR-4. You can google how composer autoloading works for more information. A tutorial for that will not be provided.
