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

!> You must first include the JSON Request class: `use Reqwest\Requests\JSONRequest;`

Create a new request instance.
```
$request = new JSONRequest;
```

### GET & DELETE

To perform a get or delete request, you only need to pass the `$url`.

```
$url = "http://example.com/api/json";

// GET Request
$response = $request->get($url);

// DELETE Request
$response = $request->delete($url);
```

### POST, PUT & PATCH

To perform a post, put, or patch request, you will need to pass the `$url` and an optional `$body` array.

```
// POST Request
$response = $request->post($url, [
    'field1' => 'value1',
    'field2' => 'value2',
    'field3' => 'value3'
]);

// PUT Request
$response = $request->put($url, [
    'field1' => 'value1',
    'field2' => 'value2',
    'field3' => 'value3'
]);

// PATCH Request
$response = $request->patch($url, [
    'field1' => 'value1',
    'field2' => 'value2',
    'field3' => 'value3'
]);
```

# Responses

All requests return a response object.

!> Instead of returning `null`, a failed request will return a response with a status code equal to `0` and a body with a `message` field.

## Status Code

You can get the status code of the response using the following method:

```
$response->getStatusCode();
```

## Headers

### Checking Headers

To check if a response has a certain header, use the `hasHeader($key)` method.

```
$response->hasHeader('Content-Type');
```

To get a single header, use the header($key) method.

### Getting Headers

You can get all headers from the response as a key-value array.

```
$response->headers();
```

To get a single header, use the `header($key)` method.

```
$response->header('Content-Type');
```

!> If the specified header doesn't exist, `null` will be returned.

## JSON Response

JSON Responses are returned from JSON Requests.

To get the body of a JSON response as a key-value array:
```
$json_response->all();
```

To check if the body of the JSON Response has a certain field:
```
$json_response->has('field_name');
```

Use the `get($field)` method to get a certain field from the JSON Response.
```
$json_response->get('field_name');
```

!> If the field doesn't exist, `null` will be returned.


