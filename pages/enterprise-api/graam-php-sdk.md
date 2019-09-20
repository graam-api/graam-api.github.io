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
      "name": "graam.io",
      "license": "MIT",
      "type": "project",
      "description": "The \"Graam SDK\"",
      "autoload": {
        "psr-0": { "GRAAM": "src" }
      },
      "repositories": [
          {
              "type": "vcs",
              "url": "https://github.com/graam-api/graam-sdk-php.git"
          }
      ],
      "require": {
          "graam/sdk-php": "dev-master"
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
$client = new \GRAAM\SDK\Client;
$client->init("api-key");
```

---

## User management
### List users

```
$result = $client->call('user.list_all',
                        array();
```

```
object(stdClass) {
  ["items"]=>
  array() {
    [0]=>
        object(stdClass)#15 (9) {
        ["public_id"]=>
        string(32) "2e14cbabef5101a4b503aadee22596c6"
        ["firstname"]=>
        string(5) "Hải"
        ["lastname"]=>
        string(6) "Phạm"
        ["email"]=>
        string(25) "luckystar171091@gmail.com"
        ["user_type"]=>
        string(5) "agent"
        ["enabled"]=>
        int(1)
        ["voicemail_enabled"]=>
        int(0)
        ["recording_mode"]=>
        int(1)
        ["google_login"]=>
        int(1)
        }
    }
  }
}
```

### Add an user

```
$result = $client->call('user.create',
                        array(
                            'firstname' => 'First name',
                            'lastname' => 'Last name',
                            'email' => 'emailuser@graam.io'
                        );
```

```
object(stdClass)#7 (1) {
  ["item"]=>
  object(stdClass)#8 (8) {
    ["firstname"]=>
    string(5) "first"
    ["lastname"]=>
    string(4) "last"
    ["email"]=>
    string(13) "flc@gmail.com"
    ["user_type"]=>
    string(4) "user"
    ["enabled"]=>
    int(1)
    ["voicemail_enabled"]=>
    int(0)
    ["recording_mode"]=>
    int(0)
    ["google_login"]=>
    int(1)
  }
}
```

### Remove an user

```
$result = $client->call('user.remove',
                        array(
                            'public_id' => 'User-public-id',
                        );
```

```
object(stdClass)#7 (1) {
  ["result"]=>
  string(2) "ok"
}
```

---

## Phone number management
### List numbers

```
$result = $client->call('did.list_all',
                        array();
```

```
object(stdClass)#7 (1) {
  ["items"]=>
  array(7) {
    [0]=>
    object(stdClass)#8 (2) {
      ["number"]=>
      string(10) "8419009000"
      ["routing_data"]=>
      object(stdClass)#9 (2) {
        ["params"]=>
        object(stdClass)#10 (1) {
          ["queue"]=>
          int(1750)
        }
        ["application"]=>
        string(9) "callqueue"
      }
    }
  }
}
```

### Buy a number

```
$result = $client->call('did.buy',
                        array(
                            'country_code' => 'FR',
                            'prefix' => '1'
                        ));
```

```
object(stdClass)#7 (1) {
  ["item"]=>
  object(stdClass)#8 (1) {
    ["number"]=>
    string(12) "152142856444"
  }
}
```


### Config a number

```
$result = $client->call('did.configure',
                        array(
                            'number' => '33339820016',
                            'routing_data' => array(
                                'application' => 'call_phone_number',
                                'params' => array('number'=> '33339820011')
                            ),
                            'name' => 'General call center number',
                            'welcome_message' => 'General number',
                        );
```

```
object(stdClass)#7 (1) {
  ["item"]=>
  object(stdClass)#8 (2) {
    ["number"]=>
    string(12) "152142856444"
    ["routing_data"]=>
    object(stdClass)#9 (2) {
      ["application"]=>
      string(17) "call_phone_number"
      ["params"]=>
      object(stdClass)#10 (1) {
        ["number"]=>
        string(4) "1112"
      }
    }
  }
}
```

### List all the country that provide phone number

```
$result = $client->call('did.zone.list_country',
                        array();
```

```
object(stdClass)#7 (1) {
  ["country_list"]=>
  array(62) {
    [0]=>
    object(stdClass)#8 (2) {
      ["country_name"]=>
      string(10) "LUXEMBOURG"
      ["code"]=>
      string(2) "LU"
    }
    [1]=>
    object(stdClass)#9 (2) {
      ["country_name"]=>
      string(8) "MALAYSIA"
      ["code"]=>
      string(2) "MY"
    }
  }
}
```

### Reserve a number (Add numbers to cart)

```
$result = $client->call('did.reserve',
                        array(
                            'country_code' => 'FR',
                            'city_name' => 'FR',
                            'quantity' => 2,
                            'type' => 'GEOGRAPHIC' // 'GEOGRAPHIC' | 'NATIONAL' | 'MOBILE',
                            'mode' => 'RANDOM', // SEQUENTIAL | RANDOM
                            'class' => 'CLASSIC'
                        );
```

```
object(stdClass)#8 (2) {
    ["token"]=>
    string(12) "a6cab4f9e2aca79092ba772199008192"
    ["expire"]=>
    string(12) "2019-06-06 12:12:00"
    ["items"]=>
    array(2) {
        [0] => string(12) "84976028600"
        [1] => string(12) "84976028610"
    }
  }
```

### Pay money for all items in cart

```
$result = $client->call('did.pay',
                        array(
                            'order_token' => 'a6cab4f9e2aca79092ba772199008192'
                        );
```
### Clear the number in cart

```
$result = $client->call('did.order.clear',
                        array(
                            'order_token' => 'a6cab4f9e2aca79092ba772199008192'
                        );

```

---

## Out call campaign management
### List out call campaigns

```
$result = $client->call('outbound_campaign.list',
                        array();
```

### Create an out call campaign

```
$result = $client->call('outbound_campaign.create',
                        array(
                            'name' => 'Out call campaign name',
                            'alias' => 'Out call campaign alias',
                            'schedule_start_date' => '2019-12-01',
                            'schedule_end_date' => '2019-12-30',
                            'hour_start' => '08:00',
                            'hour_end' => '12:00',
                            'priority' => 5,
                            'result_notification_url' => 'http://url-callback',
                        );
```
### Out call campaign detail

```
$result = $client->call('outbound_campaign.item.detail',
                        array(
                            'campaign_id' => 22131,
                            'campaign_item_id' => 112131,
                        );
```

---

## Send SMS API
[To see the list of SMS sent and received](/pages/sms/overview)
### Send an SMS

```
require 'vendor/autoload.php';
$client = new \GRAAM\SDK\Client;
$client->init("xxxx");

$result = $client->call('sms.send',
                        array(  "sender" => "336111123222",
                                "destination" => "33611111111",
                                "message" => "Hello, how are you?",
                                "language" => "fra"
                             )
                        );
```

---
