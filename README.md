# CinetPay Laravel Package

## Introduction

Ce package permet d'intégrer facilement l'SDK CinetPay dans un projet Laravel. Il fournit une interface simple pour initier et gérer les paiements via CinetPay.

(This package makes it easy to integrate the CinetPay SDK into a Laravel project. It provides a simple interface for initiating and managing payments via CinetPay.)


We invest a lot of resources into creating [best in class open source packages](https://spatie.be/open-source). You can support us by [buying one of our paid products](https://spatie.be/open-source/support-us).

We highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using. You'll find our address on [our contact page](https://spatie.be/about-us). We publish all received postcards on [our virtual postcard wall](https://spatie.be/open-source/postcards).

## Installation

You can install the package via composer:

```bash
composer require TaariamTechnologie/lara-cenetpay
```

You can publish and run the migrations with:

```bash
php artisan vendor:publish --tag=":package_slug-migrations"
php artisan migrate
```

You can publish the config file with:

```bash
php artisan vendor:publish --tag="cinetpay"
```

This is the contents of the published config file:

```php
return [
];
```

Optionally, you can publish the views using

```bash
php artisan vendor:publish --tag=":package_slug-views"
```

## Usage controller

```php
namespace App\Http\Controllers;

use VotreNom\Cinetpay\Cinetpay;

class PaymentController extends Controller
{
    public function initiatePayment()
    {
        $cinetpay = app('cinetpay');

        // Configurer le paiement
        $paymentData = [
            'amount' => 1000,
            'transaction_id' => '123456789',
            'currency' => 'XOF',
            'description' => 'Payment description',
            'return_url' => route('payment.success'),
            'notify_url' => route('payment.notify')
        ];

        // Initier le paiement
        $response = $cinetpay->makePayment($paymentData);

        return redirect($response['payment_url']);
    }
}

```

## Usage route

```php
use App\Http\Controllers\PaymentController;

Route::get('initiate-payment', [PaymentController::class, 'initiatePayment'])->name('payment.initiate');
Route::get('payment-success', function () {
    return 'Payment was successful!';
})->name('payment.success');
Route::post('payment-notify', function () {
    // Logique pour gérer la notification de paiement
})->name('payment.notify');

```

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [:author_name](https://github.com/:author_username)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
