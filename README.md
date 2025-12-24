# KetSafe

![Packagist Version](https://img.shields.io/packagist/v/ket-php/utils-truth)
![Packagist Downloads](https://img.shields.io/packagist/dt/ket-php/utils-truth?logo=packagist&logoColor=white)
![Static Badge](https://img.shields.io/badge/PHP-8.1-777BB4?logo=php&logoColor=white)



## Installation
Install via Composer:
```
composer require ket-php/utils-truth
```

## Usage

```php
use KetPHP\Utils\Truth;

// Non-strict mode (default)
var_dump(Truth::of(1)); // true
var_dump(Truth::of('on')); // true
var_dump(Truth::of('no')); // false
var_dump(Truth::of(null)); // false

// Strict mode
//
// In strict mode, any truthy list is ignored (both global and per-call custom lists). The ONLY values considered true are: 1, '1', true, 'true'
var_dump(Truth::of('true', true)); // true
var_dump(Truth::of('on', true)); // false
var_dump(Truth::of(1, true)); // true
var_dump(Truth::of(0, true)); // false

// Using a callable
var_dump(Truth::of(fn() => 'yes')); // true
var_dump(Truth::of(fn() => 'no')); // false

// Custom truthy list for a single call
$custom = ['foo', 'bar', 123];

var_dump(Truth::of('foo', false, $custom)); // true
var_dump(Truth::of('baz', false, $custom)); // false

// Configure global truthy values
Truth::configure(['sure', 'ok']);

var_dump(Truth::of('ok')); // true
var_dump(Truth::of('yes')); // false (old default removed)
```
