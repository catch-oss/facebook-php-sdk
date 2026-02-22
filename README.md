# Facebook SDK for PHP

<!-- PROJECT SHIELDS -->
[![SonarCloud](https://github.com/catch-oss/facebook-php-sdk/actions/workflows/sonar.yml/badge.svg)](https://github.com/catch-oss/facebook-php-sdk/actions/workflows/sonar.yml)
[![Test](https://github.com/catch-oss/facebook-php-sdk/actions/workflows/test.yml/badge.svg)](https://github.com/catch-oss/facebook-php-sdk/actions/workflows/test.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=catch-design_catch-oss-facebook-php-sdk)
[![Bugs](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=bugs)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Code Smells](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=code_smells)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=coverage)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Duplicated Lines Density](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=duplicated_lines_density)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Lines of Code](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=ncloc)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Reliability Rating](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=reliability_rating)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Security Rating](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=security_rating)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Technical Debt](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=sqale_index)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Maintainability Rating](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=sqale_rating)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)
[![Vulnerabilities](https://sonarcloud.io/api/project_badges/measure?project=catch-design_catch-oss-facebook-php-sdk&metric=vulnerabilities)](https://sonarcloud.io/component_measures?id=catch-design_catch-oss-facebook-php-sdk)

This repository contains the open source PHP SDK that allows you to access the Facebook Platform from your PHP app. Based on `facebookarchive/php-graph-sdk` v6.

## Installation

The Facebook PHP SDK can be installed with [Composer](https://getcomposer.org/). Run this command:

    composer require janu-software/facebook-php-sdk

You must use some client using `php-http/client-implementation`.

For example: Using with Guzzle:

    composer require janu-software/facebook-php-sdk guzzlehttp/guzzle php-http/guzzle7-adapter

## Compatibility

| Version | PHP  |
|---------|------|
| 0.1     | ^8.0 |
| 0.2     | ^8.1 |
| 0.3     | ^8.1 |
| 0.4     | ^8.3 |

## Usage

Simple GET example of a user's profile.

```php
require_once __DIR__ . '/vendor/autoload.php'; // change path as needed

$fb = new \JanuSoftware\Facebook\Facebook([
  'app_id' => '{app-id}',
  'app_secret' => '{app-secret}',
  'default_graph_version' => 'v22.0',
  //'default_access_token' => '{access-token}', // optional
]);

try {
  // If you provided a 'default_access_token', the '{access-token}' is optional.
  $response = $fb->get('/me', '{access-token}');
} catch(\JanuSoftware\Facebook\Exception\ResponseException $e) {
  // When Graph returns an error
  echo 'Graph returned an error: ' . $e->getMessage();
  exit;
} catch(\JanuSoftware\Facebook\Exception\SDKException $e) {
  // When validation fails or other local issues
  echo 'Facebook SDK returned an error: ' . $e->getMessage();
  exit;
}

$me = $response->getGraphNode();
echo 'Logged in as ' . $me->getField('name');
```

Complete documentation, installation instructions, and examples are available [here](docs/).


## Tests

1. [Composer](https://getcomposer.org/) is a prerequisite for running the tests. Install composer globally, then run `composer install` to install required files.
2. Create a test app on [Facebook Developers](https://developers.facebook.com), then create `tests/FacebookTestCredentials.php` from `tests/FacebookTestCredentials.php.dist` and edit it to add your credentials.
3. The tests can be executed by running this command from the root directory:

```bash
$ ./vendor/bin/phpunit
```

By default the tests will send live HTTP requests to the Graph API. If you are without an internet connection you can skip these tests by excluding the `integration` group.

```bash
$ ./vendor/bin/phpunit --exclude-group integration
```


## License

Please see the [license file](https://github.com/janu-software/facebook-php-sdk/blob/main/LICENSE) for more information.


## Security Vulnerabilities

If you have found a security issue, please contact the maintainers directly at [s@janu.software](mailto:s@janu.software).
