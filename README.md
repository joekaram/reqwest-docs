# Reqwest

Reqwest is a simple request handler built over [Guzzle HTTP](https://github.com/guzzle/guzzle).<br>
The main purpose behind Reqwest is to simplify the code for making http requests.

## Getting Started

### Prerequisites

The recommended way to install Reqwest is using [Composer](https://getcomposer.org).<br>

```
# Install Composer
curl -sS https://getcomposer.org/installer | php
```

### Installation

Run the composer command to install the latest version of Reqwest.

```
php composer.phar require karam/reqwest
// or
composer require karam/reqwest
```

# Requests

## Headers

When making requests, you can add, update, or remove headers.<br>

### Adding Headers

You can add multiple headers by chaining the `addHeader($key, $value)` method, but there is another way to do so using the `addHeaders()` method.

```
// Method chaining:
$request->addHeader('Content-Type', 'application/json')
    ->addHeader('Auhtorization', 'Bearer ' . $token);

// Using arrays:
$request->addHeaders([
    'Content-Type' => 'application/json',
    'Authorization' => 'Bearer ' . $token
])
```

### Updating Headers

You can update an existing header using the following method:

```
$request->updateHeader('Content-Type', 'application/json');
```

### Deleting Headers

You can remove an added header using the `deleteHeader($key)` method.

```
$request->deleteHeader('Content-Type');
```

## JSON Requests

JSON Requests are regular requests with Content-Type header automatically set to application/json.

!> You must first include the JSON Request class.<br>`use Reqwest\Requests\JSONRequest;`

### GET & DELETE

To perform a get or delete request, you only need to pass the `$url`.

```
$url = "http://example.com/api/json";

// GET Request
$response = $json_request->get($url);

// DELETE Request
$response = $json_request->delete($url);
```

### POST, PUT & PATCH

To perform a post, put, or patch request, you will need to pass the `$url` and an optional `$body` array.

```
// POST Request
$response = $json_request->post($url, [
    'field1' => 'value1',
    'field2' => 'value2',
    'field3' => 'value3'
]);

// PUT Request
$response = $json_request->put($url, [
    'field1' => 'value1',
    'field2' => 'value2',
    'field3' => 'value3'
]);

// PATCH Request
$response = $json_request->patch($url, [
    'field1' => 'value1',
    'field2' => 'value2',
    'field3' => 'value3'
]);
```
