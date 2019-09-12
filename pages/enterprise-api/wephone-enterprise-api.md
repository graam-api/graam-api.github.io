---
Title: Graam Enterprise API
---

## Phone Number API
### Get the list of enterprise DID

Function: did.list_all

```
$result = $client->call('did.list_all', array());
```

### Add a phone number to the currently active order

Function: did.reserve

Parameters:
- contry_code: Two letter country code
- city_name: The name of the city
- quantity: The quantity of number to buy
- type: Number type. Can be one of (GEOGRAPHIC|NATIONAL|MOBILE)

```
$result = $client->call('did.reserve', 
	array('country_code' => 'FR', 
			'city_name' => 'Paris',
			'quantity' => 1,
			'type' => 'GEOGRAPHIC'
	)
);
```


### Proceed to pay the active order

Function: did.order.pay

Parameters:
- order_token (optional): The token of the order to pay. Default to the currently active order if not provide.

```
$result = $client->call('did.order.pay', array('order_token' => $orderToken));
```


### Clear the current order

```
$result = $client->call('did.order.clear', array('order_token' => $orderToken));  // Parameter order_token is optional
```

### Return a phone number


```
$result = $client->call('did.return', array('returned_number'));
```

### Define call routing for a phone number


```
$routingData = array(
    "application"=> "call_phone_number", 
    "params"=> array("number"=> "111")
);
$result = $client->call('did.configure', array('routed_number', $routingData));
```

********************************************************************************

### Call queue
### Get the list of all call queues

```
$result = $client->call('queue.list_all', array());
```

