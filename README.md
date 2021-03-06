WebLab B.V. - cURL Wrapper
==================================

This library is build upon the cURL functionality. It's a programmer friendly way to do cURL requests and mostly to keep things readable while still allowing full control over your request.


Installation
------------

### Install using composer:

    composer require weblabnl/curl


Using the Library
-----------------

#### Make a POST request to a REST API

```php
$params = [
    first_name  => 'Ankie',
    last_name   => 'Visser'
];

$url = 'https://api.weblab.nl/users';

$result = Weblab\CURL\CURL::setBearer('some_access_token')
    ->post($url, $params);
    
if ($result->getStatus() === 201) {
    // User created        
}    
```
    
#### Make a PATCH request to a REST API (without helper functions)

```php
$url = 'https://api.weblab.nl/users/1';

$params = [
    'ankievisser01@test.com'
];

$request = (new Weblab\CURL\Request())
    ->setOption(CURLOPT_URL, $url)
    ->setOption(CURLOPT_POSTFIELDS, http_build_query($params))
    ->setOption(CURLOPT_CUSTOMREQUEST, 'PATCH')
    ->setOption(CURLOPT_POST, true)
$result = $request->run();

if ($result->getStatus() === 200) {
    // user successfully saved            
}
```
    
#### Make a GET request (Content-Type: application/json are automatically decoded)

```php
$result = Weblab\CURL\CURL::get('https://api.weblab.nl/users', ['limit' => '1']);

/**
 * cURL result body:
 * {
 *     data: [
 *         {
 *             id           : 1 ,
 *             first_name   : "Ankie",
 *             last_name    : "Visser"
 *         }
 *     ]
 * }
 */

if ($result->getStatus() === 200) {
    foreach ($result->getResults()->data as $user) {
        // $user object
    }
}
```

#### Check if a file exists
```php
$result = Weblab\CURL\CURL::doesFileExist('https://www.weblab.nl/img/logo.png')
if ($result) {
    // file exists
}
```
