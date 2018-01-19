# Slim 3 Session

[![Latest Version on Packagist](https://img.shields.io/github/release/odan/slim-session.svg)](https://github.com/odan/slim-session/releases)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg)](LICENSE.md)
[![Build Status](https://travis-ci.org/odan/slim-session.svg?branch=master)](https://travis-ci.org/odan/slim-session)
[![Code Coverage](https://scrutinizer-ci.com/g/odan/slim-session/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/odan/slim-session/?branch=master)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/odan/slim-session/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/odan/slim-session/?branch=master)
[![Total Downloads](https://img.shields.io/packagist/dt/odan/slim-session.svg)](https://packagist.org/packages/odan/slim-session)


## Installation

```
composer require odan/slim-session
```

## Integration

### Register the middleware

In your `config/container.php` or wherever you add your service factories:

```php
$container[SessionMiddleware::class] = function (Container $container) {
    $settings = $container->get('settings');
    return new \Odan\Slim\Session\SessionMiddleware($settings['session']);
};
```

Add middleware as usual:

```php
$app->add($container->get(SessionMiddleware::class));
```

or without the container like this:

```php
$app->add(new \Odan\Slim\Session\SessionMiddleware(['name' => 'my-session-name']));
```

## Usage

```php
// Get session variable:
$foo = $session->get('foo', 'some-default');

// Set session variable:
$session->set('bar', 'that');

// Delete a session variable
$session->remove('key');

// Clear all session variables
$session->clear();

// Generate a new session ID
$session->regenerateId();

// Clears all session data and regenerates session ID
$session->destroy();

// Get the current session ID
$session->getId();

// Set the session ID
$session->setId('...');

// Get the session name
$session->getName();

// Set the session name
$session->setName('my-app');

// Returns true if the attribute exists
$session->has('foo');

// Sets multiple values at once
$session->replace(['foo' => 'value1', 'bar' => 'value2']);

// Get the number of values.
$session->count();

// Force the session to be saved and closed
$session->save();

// Set session runtime configuration
// Alle supported keys: http://php.net/manual/en/session.configuration.php
$session->setOptions($options);

// Get session runtime configuration
$session->getOptions();

// Set cookie parameters
$session->setCookieParams(4200, '/', '', false, false);

// Get cookie parameters
$session->getCookieParams();
```