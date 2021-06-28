
<!--

---

title: downloadpolist

layout: template

filename: downloadpolist.md

--- 

-->




## API Download Purchase Orders

Get a list of purchase orders associated with a vendor account from the DNAS marketplace.

**Request URL**: [https://api-daynite.dnasmarketplace.com/v1/cart/downloadpolist](https://api-daynite.dnasmarketplace.com/v1/cart/downloadpolist)

**API HTTP request method**: POST  

### Required Headers

Content-Type: **application/json**

Authorization: **Bearer *TOKEN*** 

- *TOKEN* is retrieved through authorization API call using vendor account username and password
-  [Auth API Doc](https://punchout-daynite.dnasmarketplace.com/api-docs/)

### Required Body
JSON Content

```
{
    "status":"",
    "created_on":""
}
```
### Required Parameters
None

### PHP Curl Example
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://api-daynite.dnasmarketplace.com/v1/cart/downloadpolist',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "status":"",
    "created_on":""
}',
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/json',
    'Authorization: Bearer TOKEN'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```
### Node.js AXIOS Example
```
var axios = require('axios');
var data = JSON.stringify({
  "status": "",
  "created_on": ""
});

var config = {
  method: 'post',
  url: 'https://api-daynite.dnasmarketplace.com/v1/cart/downloadpolist',
  headers: { 
    'Content-Type': 'application/json', 
    'Authorization': 'Bearer TOKEN'
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});

```

