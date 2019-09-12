---
title: Graam PHP SDK
---

# Graam PHP SDK (*Beta  non-stable)

Graam PHP SDK is a PHP library that allow you to quickly call Graam APIs. 
To use the Graam PHP SDK, you need to get the API key for your enterpise. To get API key, first login to Graam site with your admin account. Then, click on Settings --> API Integration at the botton of the left menu. You will then be able to copy your enterprise's existing API key or create a new one.

![alt text](/images/get-api-key.png)
 
1. Setting up the library using composer

Get PHP Composer from this page (https://getcomposer.org/).
Create a composer.json file as bellow, then run composer update:

Here is the content of composer.json::

```JSON
  {
      "name": "TestSMS",
      "repositories": [
          {
              "type": "vcs",
              "url": "https://github.com/Graam-saas/sdk-php.git"
          }
      ],
      "require": {
          "Graam/sdk-php": "dev-master"
      }
  }
```

Add more library dependency to your `composer.json` as needed. Remember to run `composer update` each time composer.json is updated.

Add the next lines to your PHP source file so that it knows how to find Graam SDK:

```
<?php

require 'vendor/autoload.php';
```

1.2 Usage example


### Init

```
$client = new \Graam\SDK\Client;
$client->init("api-key", "https://admin.graam.io");
```

---

## Send SMS API
[To see the list of SMS sent and received](/pages/sms/overview)
### Send an SMS

```
$client = new \Graam\SDK\Client;
$client->init("xxxx", "https://admin.graam.io");

$result = $client->call('sms.send',
                        array(  "sender" => "MySenderName",
                                "destination" => "+33611111111",
                                "message" => "Hello, how are you?"
                             )
                        );
```


---
