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
### Add an user

```
$result = $client->call('user.create',
                        array(
                            'firstname' => 'First name',
                            'lastname' => 'Last name',
                            'email' => 'emailuser@graam.io'
                        );
```
### Remove an user

```
$result = $client->call('user.remove',
                        array(
                            'public_id' => 'User-public-id',
                        );
```

---

## Phone number management
### List numbers

```
$result = $client->call('did.list_all',
                        array();
```
### Buy a number

```
$result = $client->call('did.buy',
                        array(
                            'country_code' => 'FR',
                            'prefix' => '1'
                        );
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
### List all the country that provide phone number

```
$result = $client->call('did.zone.list_country',
                        array();
```
### Reserve a number

```
$result = $client->call('did.zone.reserve',
                        array(
                            'country_code' => 'FR',
                            'city_name' => 'FR',
                            'quantity' => 2,
                            'type' => 'GEOGRAPHIC' // 'GEOGRAPHIC' | 'NATIONAL' | 'MOBILE',
                            'mode' => 'RANDOM', // SEQUENTIAL | RANDOM
                            'class' => 'CLASSIC'
                        );
```
### Pay money for a reserved number

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
$client = new \GRAAM\SDK\Client;
$client->init("xxxx");

$result = $client->call('sms.send',
                        array(  "sender" => "336111123222",
                                "destination" => "+33611111111",
                                "message" => "Hello, how are you?",
                                "language" => "fra"
                             )
                        );
```


---
