# Laravel URI Translator

[![Laravel](https://img.shields.io/badge/laravel-13-red?style=flat-square&logo=laravel&logoColor=white)](https://laravel.com)
[![License](https://img.shields.io/packagist/l/opgginc/codezero-laravel-uri-translator.svg?style=flat-square)](LICENSE.md)
[![Total Downloads](https://img.shields.io/packagist/dt/opgginc/codezero-laravel-uri-translator.svg?style=flat-square)](https://packagist.org/packages/opgginc/codezero-laravel-uri-translator)

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/R6R3UQ8V)

This package registers a macro for the Laravel `Translator` class.
This will allow you to translate individual URI slugs, while ignoring parameter placeholders.

Parameters will not be translated by this macro. That remains the responsibility of your code.

## ✅ Requirements

- PHP >= 8.1 
- Laravel >= 10.0 (supports up to 13.0)

## 📦 Install

Install this package with Composer:

```bash
composer require opgginc/codezero-laravel-uri-translator
```

Laravel will automatically register the ServiceProvider.

In your app's `lang` folder, create subdirectories for every locale you want to have translations for.

Next create a `routes.php` file in each of those directories.

```
lang/
  ├── en/
  │    └── routes.php
  └── nl/
       └── routes.php
```

Return an array of translations from the `routes.php` files.

### 🚀 Usage

Use the `Lang::uri()` macro when registering routes:

```php
Route::get(Lang::uri('hello/world'), [Controller::class, 'index']);
```

The URI macro accepts 2 additional parameters:

1. A locale, in case you need translations to a locale other than the current app locale.
2. A namespace, in case your translation files reside in a package.

```php
Lang::uri('hello/world', 'fr', 'my-package');
```

You can also use `trans()->uri('hello/world')` instead of `Lang::uri('hello/world')`.

### 🔌 Example

Using these example translations:

```php
// lang/nl/routes.php
return [
    'hello' => 'hallo',
    'world' => 'wereld',
    'override/hello/world' => 'something/very/different',
    'hello/world/{parameter}' => 'uri/with/{parameter}',
];
```

These are possible translation results:

```php
// Translate every slug individually
// Translates to: 'hallo/wereld'
Lang::uri('hello/world');

// Keep original slug when missing translation
// Translates to: 'hallo/big/wereld'
Lang::uri('hello/big/world');

// Translate slugs, but not parameter placeholders
// Translates to: 'hallo/{world}'
Lang::uri('hello/{world}');

// Translate full URIs if an exact translation exists
// Translates to: 'something/very/different'
Lang::uri('override/hello/world');

// Translate full URIs if an exact translation exists (with placeholder)
// Translates to: 'uri/with/{parameter}'
Lang::uri('hello/world/{parameter}');
```

## 🚧 Testing

```bash
composer test
```
## ☕️ Credits

- [Ivan Vermeyen](https://github.com/ivanvermeyen) (Original Author) - Rest in Peace
- [OPGG Inc. Team](https://github.com/opgginc)
- [All contributors](https://github.com/opgginc/codezero-laravel-uri-translator/contributors)

> This package is a fork of the original work by Ivan Vermeyen. We are deeply saddened to share that Ivan has passed away. In memory of his excellent contribution to the Laravel community, we have forked this package to maintain and extend its functionality for newer Laravel versions. We extend our condolences to Ivan's family and friends.

## 🔒 Security

This project is maintained by OP.GG Inc. If you discover any security related issues, please use the issue tracker.

## 📑 Changelog

This package is a fork of [codezero/laravel-uri-translator](https://github.com/codezero-be/laravel-uri-translator), updated to support Laravel 12 and PHP 8.4.

## 📜 License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
