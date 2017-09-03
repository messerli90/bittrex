Bittrex
=========

[![Build Status](https://travis-ci.org/messerli90/bittrex.svg?branch=master)](https://travis-ci.org/messerli90/igdb)
[![Built For Laravel](https://img.shields.io/badge/built%20for-laravel-blue.svg)](http://laravel.com)
[![License](https://poser.pugx.org/messerli90/igdb/license)](https://packagist.org/packages/messerli90/igdb)
[![Total Downloads](https://poser.pugx.org/messerli90/bittrex/downloads)](https://packagist.org/packages/messerli90/bittrex)

## Introduction
This packages provides a nice and easy wrapper around the [Bittrex API](https://bittrex.com/) for use in your Laravel application.

In order to use the Bittrex API, you must have an account and API keys. 

## Example

Retrieve your balance statements for all coins

```php
use Messerli90\Bittrex\Bittrex;

$bittrex = new Bittrex(config('services.bittrex.key'), config('services.bittrex.secret'));

$balances = $bittrex->getBalances();

return $balances;
```

```json
{
  "success": true,
  "message": "",
  "result": [
    {
      "Currency": "BTC",
      "Balance": 2.20529678,
      "Available": 2.20529678,
      "Pending": 0,
      "CryptoAddress": null
    },
    {
      "Currency": "LTC",
      "Balance": 12.96782052,
      "Available": 12.96782052,
      "Pending": 0,
      "CryptoAddress": null
    }
  ]
}
```

## Installation

Add `messerli90/bittrex` to your `composer.json`.
```
"messerli90/bittrex": "~1.0"
```
or 
```bash
composer require messerli90/bittrex
```

Run `composer update` to pull down the latest version of the package.

Now open up `app/config/app.php` and add the service provider to your `providers` array.

```php
'providers' => array(
    Messerli90\Bittrex\BittrexServiceProvider::class,
)
```

Optionally, add the facade to your `aliases` array
```php
'Bittrex' => \Messerli90\Bittrex\Facades\Bittrex::class,
```

## Configuration

Add the `bittrex` to your `config/services.php` array
```php
'bittrex' => [
    'key' => 'YOUR_API_KEY',
    'secret' => 'YOUR_API_SECRET
]
```

## Usage
```php
use Messerli90\Bittrex\Bittrex;

$bittrex = new Bittrex(config('services.bittrex.key'), config('services.bittrex.secret'));
```

### Public API

```php
// Used to get the open and available trading markets at Bittrex along with other meta data.
$bittrex->getMarkets();

// Used to get all supported currencies at Bittrex along with other meta data.
$bittrex->getCurrencies();

// Used to get the current tick values for a market.
$bittrex->getTicker('BTC-LTC');

// Used to get the last 24 hour summary of all active exchanges
$bittrex->getMarketSummaries();

// Used to get the last 24 hour summary of all active exchanges
$bittrex->getMarketSummary('BTC-LTC');

// Used to get retrieve the orderbook for a given market
$bittrex->getOrderBook('BTC-LTC', 'both');

// Used to retrieve the latest trades that have occured for a specific market.
$bittrex->getMarketHistory('BTC-LTC');
```

### Market
```php
// Used to place a buy order in a specific market. Use buylimit to place limit orders. Make sure you have the proper permissions set on your API keys for this call to work
$bittrex->buyLimit('BTC-LTC', 1.2, 1.3);

// Used to place an sell order in a specific market. Use selllimit to place limit orders.
$bittrex->sellLimit('BTC-LTC', 1.2, 1.3);

// Used to cancel a buy or sell order.
$bittrex->cancel('ORDER_UUID');

// Get all orders that you currently have opened. A specific market can be requested
$bittrex->getOpenOrders('BTC-LTC');
```

### Account
```php
// Used to retrieve all balances from your account
$bittrex->getBalances();

// Used to retrieve the balance from your account for a specific currency.
$bittrex->getBalance('BTC');

// Used to retrieve or generate an address for a specific currency. If one does not exist, the call will fail and return ADDRESS_GENERATING until one is available.
$bittrex->getDepositAddress('BTC');

// Used to withdraw funds from your account. note: please account for txfee.
$bittrex->withdraw('BTC', 1, 'BTC-ADDRESS');

// Used to retrieve all balances from your account
$bittrex->getBalances();

// Used to retrieve a single order by uuid.
$bittrex->getOrder('0cb4c4e4-bdc7-4e13-8c13-430e587d2cc1');

// Used to retrieve your order history.
$bittrex->getOrderHistory('BTC-LTC');

// Used to retrieve your withdrawal history.
$bittrex->getWithdrawalHistory('BTC');

// Used to retrieve your deposit history.
$bittrex->getDepositHistory('BTC');
```

## Format of returned data

The returned JSON data is decoded as a PHP object.

## Run Unit Test

If you have PHPUnit installed in your environment, run:

```bash
$ phpunit
```

## IGDB API

- [Bittrex API Docs](https://bittrex.com/Home/Api)


## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Credits

- [Michael Messerli](https://twitter.com/michaelmesserli)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
