---
Title: Graam Call Center Javascript Library
---

## The library

Graam call center library is a javascript library hosted on Graam's website. Just include it in your pages before making use of its api.

```javascript
<script src="https://admin.graam.io/a/{enterprise-domain}/public/libs/1.0/Graam_callcenter_1.1.0.js"></script>
```

## The GraamCallCenter object

The library above export a global object GraamCallCenter with the following methods.


# Make an outbound call

GraamCallCenter.**make_call**(called_number, calling_number, queue_id, queue_name, custom_data, success_cb, error_cb);

The arguments:
- called_number: The number to be called
- calling_number: One of your Graam numbers. This number is displayed on the callee's phone as the calling number.
- queue_id: Do not use this value (Always set to null)
- queue_name: The name or alias of a call queue. If this parameter is set, the call is accounted as an outbound call from the call queue.
- custom_data: An object that contain custom information to be associated with the call. This data can be later retrieved back from Graam. For exemple, you can get this date from Graam if you set a webhook to get the "call end" event.
- success_cb: The function to be called on success.
- error_cb: The function to be called in case of error.

Example:
```javascript
GraamCallCenter.transfer_call('0611111111', null, null, 'Queue 1', '{"client_id": "12131"}');
```

# Transfer the current call to a phone number

GraamCallCenter.**transfer_call**(destination_number, assisted_transfer);


The arguments:
- destination_number: The number to transfer call to
- assisted_transfer: This parameter can be 0 or 1. 1: Assisted transfer. 0: Blind transfer.

Example:
```javascript
GraamCallCenter.transfer_call('0622222222', 1);
```
