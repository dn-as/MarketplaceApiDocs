<!--

---

layout: template

title: auth

filename: setpostatus.md

--- 

-->

## API set purchase order status

This api will be called by vendors to update the status of a Purchase Order to “Retrieved”. First the vendors needs to call the login api for authentication. They will get an authentication token in login api response. This token will be used in the update PO status API.

**Request URL**: [https://api-daynite.dnasmarketplace.com/v1/vendor/updatepostatus](https://api-daynite.dnasmarketplace.com/v1/vendor/updatepostatus)

**API HTTP request method**: POST  

### Required Headers

Content-Type: application/json

### Required Body
JSON Content

po_number: Sampro PO number from purchase order record

status: A string value from allowed statuses list for vendors to set, case sensitive


| Current Allowed Status 	|
|--						|
|	Retrieved							|

```
{
    "po_number" : "1234567",
    "status": "Retrieved"
}
```

### Required Parameters

Content-Type: **application/json**

Authorization: **Bearer *TOKEN*** 

- *TOKEN* is retrieved through authorization API call using vendor account username and password
-  [Auth Token Guide](auth.md)
-  [Swagger Auth API Doc](https://punchout-daynite.dnasmarketplace.com/api-docs/)

### PHP Curl Example
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://api-daynite.dnasmarketplace.com/v1/vendor/updatepostatus',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "po_number" : "1234567",
    "status": "Retrieved"
}',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer TOKEN',
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;

```

### API Response Example: JSON Content

```
{
    "success": true,
    "message": "Purchase Order #1234567 updated successfully."
}
```



