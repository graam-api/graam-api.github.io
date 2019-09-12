---
Title: Click To Call from your own back office
---

## Introduction

You can add click to call function to your enterprise's back-office pages so that your back-office users can make outbound call just by clicking on a phone number.

## Configuration

1. Add Graam callcenter library to your back-office
    Add this code to the header of your back-offices pages

```javascript
<script src="https://admin.graam.io/a/{enterprise-domain}/public/libs/1.0/Graam_callcenter_1.1.0.js"></script>
```

Where {enterprise-domain} is the your Graam's enterprise domain. For example, if your Graam enterprise domain is "myenterprise", then the URL to use is:

```javascript
<script src="https://admin.graam.io/a/myenterprise/public/libs/1.0/Graam_callcenter_1.1.0.js"></script>
```


2. Call make_call function to make call with Graam

    The javascript library above provide the global object GraamCallCenter. To make call from your javascript code, you should call the [GraamCallCenter.make_call](callcenter-js-library#make_call) function.

