Bitstamp API (PHP)
==================

A PHP implementation for accessing the [Bitstamp API](https://www.bitstamp.net/api/).

WARNING: The Bitstamp API allows you to perform live transactions. This library is provided as-is, to use free of
charge, and I will aim to keep it up-to-date with API changes. However, please remember that I will take no
responsibility for the integrity or reliability of this library and will not be responsible for any damage or loss of
earnings caused by the use of this library. Use at your own will.

Requirements
------------

 * PHP >= 5.4
 * ext-curl
 * ext-json (PHP >= 5.5)
 * ext-mcrypt

Installation
------------

### Composer ###

Add the following dependency to your `composer.json` file:

    "require": {
        "apancutt/bitstamp-api": "1.0.*"
    }

Note that **this library is currently under development** so you will also need to add:

    "minimum-stability": "dev"

Example Usage
-------------

    <?php
    // Path to the autoloader generated by Composer
    require_once __DIR__ . "/../vendor/autoload.php";

    // The HTTP request client, provided by panadas/module-httpclient
    $request = new \Panadas\Module\HttpClient\Request($logger);

    /*
    // Alternatively, you can provide an instance of Panadas\Module\LoggerAbstract for log messages
    $logger = new \Panadas\Module\Logger\Unbuffered();
    $request = new \Panadas\Module\HttpClient\Request($logger);
    */

    // Your Bitstamp client/customer ID
    $client_id = 0;

    // You will need to generate API keys with the required access level using your
    // account control panel: https://www.bitstamp.net/account/security/api/
    $api_secret = "";
    $api_key = "";

    try {

        $client = new \Bitstamp\Api\Client($request, $client_id, $api_secret, $api_key);

        // Display your account balance
        print_r((new \Bitstamp\Api\Endpoint\Balance($client))->execute());

    } catch (\Exception $exception) {

        $logger->error($exception->getMessage());
        exit(1);

    }

More information can be found at: https://www.bitstamp.net/api/
