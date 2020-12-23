## Unofficial PHP Package for hesabfa.com

This package makes it easier for php programmers to use the Hesabfa API.

### How to install:
```
composer require amirbagh75`/hesabfa-client
```

### Example
```php
<?php

require __DIR__ . '/../vendor/autoload.php';

use Amirbagh75\HesabfaClient\HesabfaClient;
use GuzzleHttp\Exception\GuzzleException;

$userID = getenv('USER_ID');
$userPassword = getenv('USER_PASSWORD');
$apiKey = getenv('API_KEY');

$hesabfa = new HesabfaClient($userID, $userPassword, $apiKey);


try {
    $res = $hesabfa->getInvoices(1, [
        'SortBy' => 'Date',
        'SortDesc' => true,
        'Take' => 1,
        'Skip' => 0
    ]);
    print_r($res);
} catch (GuzzleException $e) {
    print_r('Problem happened: ' . $e->getMessage());
}
```


### Example in laravel 8 (use Facades)

First add these environment variables in your .env file:

```
SMSIR_API_KEY="xxxx"
SMSIR_SECRET_KEY="xxxx"
SMSIR_LINE_NUMBER="xxxx"
```
Then use it like the following example:

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use HesabfaClient;
use Log;

class Example extends Controller
{
    /**
     * Handle the incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return \Illuminate\Http\Response
     */
    public function __invoke(Request $request)
    {
        // do something ...
        try {
            $res = HesabfaClient::getInvoices(1, [
              'SortBy' => 'Date',
              'SortDesc' => true,
              'Take' => 1,
              'Skip' => 0
            ]);
            dd($res);
        } catch (\GuzzleHttp\Exception\GuzzleException $e) {
            Log::error($e->getMessage());
        }
        // do something ...
    }
}
```


### Current methods:


```php
// Contacts - docs: https://www.hesabfa.com/help/api/Contact
public function getContact(string $contactCode);
public function getContactsList(array $queryInfo);
public function getContactsByID(array $contactsID);

// Invoices - docs: https://www.hesabfa.com/help/api/Invoice
public function getInvoices(string $invoiceType, array $queryInfo);

// Hooks - docs: https://www.hesabfa.com/help/api/Hook
public function setWebHook(string $url, string $hookPassword);

// Items - docs: https://www.hesabfa.com/help/api/Item
public function getItemByID(array $idList);
```

## Versioning

We use [Semantic Versioning](http://semver.org/). [See the available versions](https://github.com/amirbagh75/hesabfa-php-client/releases).

## Authors

- **[Amirhossein Baghaie](https://github.com/amirbagh75)** - _Maintainer_