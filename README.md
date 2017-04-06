# Rinvex Addressable

**Rinvex Addressable** is a polymorphic Laravel package, for addressbook management. You can add addresses to any eloquent model with ease.

[![Packagist](https://img.shields.io/packagist/v/rinvex/addressable.svg?label=Packagist&style=flat-square)](https://packagist.org/packages/rinvex/addressable)
[![VersionEye Dependencies](https://img.shields.io/versioneye/d/php/rinvex:addressable.svg?label=Dependencies&style=flat-square)](https://www.versioneye.com/php/rinvex:addressable/)
[![Scrutinizer Code Quality](https://img.shields.io/scrutinizer/g/rinvex/addressable.svg?label=Scrutinizer&style=flat-square)](https://scrutinizer-ci.com/g/rinvex/addressable/)
[![Code Climate](https://img.shields.io/codeclimate/github/rinvex/addressable.svg?label=CodeClimate&style=flat-square)](https://codeclimate.com/github/rinvex/addressable)
[![Travis](https://img.shields.io/travis/rinvex/addressable.svg?label=TravisCI&style=flat-square)](https://travis-ci.org/rinvex/addressable)
[![SensioLabs Insight](https://img.shields.io/sensiolabs/i/e925718d-bb6a-4cde-a7e4-666528596e9a.svg?label=SensioLabs&style=flat-square)](https://insight.sensiolabs.com/projects/e925718d-bb6a-4cde-a7e4-666528596e9a)
[![StyleCI](https://styleci.io/repos/77295377/shield)](https://styleci.io/repos/77295377)
[![License](https://img.shields.io/packagist/l/rinvex/addressable.svg?label=License&style=flat-square)](https://github.com/rinvex/addressable/blob/develop/LICENSE)


## Installation

1. Install the package via composer:
    ```shell
    composer require rinvex/addressable
    ```

2. Execute migrations via the following command:
    ```
    php artisan migrate --path="vendor/rinvex/addressable/database/migrations"
    ```

3. Add the following service provider to the `'providers'` array inside `app/config/app.php`:
    ```php
    Rinvex\Addressable\AddressableServiceProvider::class
    ```

4. **Optionally** you can publish migration and config files by running the following commands:
    ```shell
    // Publish migrations
    php artisan vendor:publish --tag="migrations" --provider="Rinvex\Addressable\AddressableServiceProvider"

    // Publish config
    php artisan vendor:publish --tag="config" --provider="Rinvex\Addressable\AddressableServiceProvider"
    ```

5. Done!


## Usage

### Create Your Model

Simply create a new eloquent model, and use `Addressable` trait:
``` php
<?php

namespace App;

use Rinvex\Addressable\Addressable;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    use Addressable;
}
```

### Manage Your Addresses

```php
use Rinvex\Addressable\Address;

// Create a new address
Address::create([
    'label' => 'Default Address',
    'name_prefix' => 'Mr.',
    'first_name' => 'Abdelrahman',
    'middle_name' => 'Hossam M. M.',
    'last_name' => 'Omran',
    'name_suffix' => null,
    'country' => 'eg',
    'organization' => 'Rinvex',
    'street' => '56 john doe st.',
    'state' => 'Alexandria',
    'city' => 'Alexandria',
    'useral_code' => '21614',
    'phone' => '01228160181',
    'lat' => '31.2467601',
    'lng' => '29.9020376',
    'is_primary' => true,
    'is_billing' => true,
    'is_shipping' => true,
]);

// Find an existing address
$address = Address::find(1);

// Update an existing address
$address->update([
    'label' => 'Default Work Address',
]);
```

### Alternative Method to Manage Your Addresses

```php
use App\User;
use Rinvex\Addressable\Address;

// Find an existing user
$user = User::find(1);

// Create a new address
$user->createAddress([
    'label' => 'Default Address',
    'name_prefix' => 'Mr.',
    'first_name' => 'Abdelrahman',
    'middle_name' => 'Hossam M. M.',
    'last_name' => 'Omran',
    'name_suffix' => null,
    'country' => 'eg',
    'organization' => 'Rinvex',
    'street' => '56 john doe st.',
    'state' => 'Alexandria',
    'city' => 'Alexandria',
    'useral_code' => '21614',
    'phone' => '01228160181',
    'lat' => '31.2467601',
    'lng' => '29.9020376',
    'is_primary' => true,
    'is_billing' => true,
    'is_shipping' => true,
]);

// Find an existing address
$address = Address::find(1);

// Update an existing address
$user->updateAddress($address, [
    'label' => 'Default Work Address',
]);

// Attach an existing address
$user->attachAddress($address);

// Attach multiple existing addresses
$user->attachAddress([1, 2, 3]);

// Detach an existing address
$user->detachAddress($address);

// Attach multiple existing addresses
$user->detachAddress([1, 2, 3]);

// Alternative method for detaching addresses
$user->removeAddress($address);
$user->removeAddress([1, 2, 3]);
```

### Manage Your Addressable Model

The API is intutive and very straightfarwad, so let's give it a quick look:
```php
// Instantiate your model
$user = new \App\User();

// Get attached addresses collection
$user->addresses;

// Get attached addresses query builder
$user->addresses();
```

### Advanced Usage

```php
// Scope Primary Addresses
Address::isPrimary();

// Scope Billing Addresses
Address::isBilling();

// Scope Shipping Addresses
Address::isShipping();

// Scope Addresses in the given country
Address::InCountry('eg');

// Retrieve All Models Attached To The Address
$address = Address::find(1);
$address->entries(\App\User::class);

// Find all users within 5 kilometers radius from the lat/lng 31.2467601/29.9020376
User::findByDistance(5, 'kilometers', '31.2467601', '29.9020376');

// Alternative method to find users with certain radius
$user = new User();
$users = $location->lat('31.2467601')->lng('29.9020376')->within(5, 'kilometers')->get();
```


## Changelog

Refer to the [Changelog](CHANGELOG.md) for a full history of the project.


## Support

The following support channels are available at your fingertips:

- [Chat on Slack](http://chat.rinvex.com)
- [Help on Email](mailto:help@rinvex.com)
- [Follow on Twitter](https://twitter.com/rinvex)


## Contributing & Protocols

Thank you for considering contributing to this project! The contribution guide can be found in [CONTRIBUTING.md](CONTRIBUTING.md).

Bug reports, feature requests, and pull requests are very welcome.

- [Versioning](CONTRIBUTING.md#versioning)
- [Pull Requests](CONTRIBUTING.md#pull-requests)
- [Coding Standards](CONTRIBUTING.md#coding-standards)
- [Feature Requests](CONTRIBUTING.md#feature-requests)
- [Git Flow](CONTRIBUTING.md#git-flow)


## Security Vulnerabilities

If you discover a security vulnerability within this project, please send an e-mail to [help@rinvex.com](help@rinvex.com). All security vulnerabilities will be promptly addressed.


## About Rinvex

Rinvex is a software solutions startup, specialized in integrated enterprise solutions for SMEs established in Alexandria, Egypt since June 2016. We believe that our drive The Value, The Reach, and The Impact is what differentiates us and unleash the endless possibilities of our philosophy through the power of software. We like to call it Innovation At The Speed Of Life. That’s how we do our share of advancing humanity.


## License

This software is released under [The MIT License (MIT)](LICENSE).

(c) 2016-2017 Rinvex LLC, Some rights reserved.