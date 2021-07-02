<!--

---

layout: template

title: auth

filename: auth.md

--- 

-->

## API Auth Token

Get authorization token for a marketplace account

**Request URL**: [https://punchout-daynite.dnasmarketplace.com/auth/login](https://punchout-daynite.dnasmarketplace.com/auth/login)

**API HTTP request method**: POST  

### Required Headers

Content-Type: application/json

### Required Body
JSON Content

email: marketplace user email address

password: marketplace user password

```
{
  "email": "user@domain.com",
  "password": "password"
}
```

### Required Parameters
None

### PHP Curl Example
```
<?php

  $curl = curl_init();

  $certFileLocation = "cacert.pem";		


  curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://punchout-daynite.dnasmarketplace.com/auth/login',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_VERBOSE => true,    
  CURLOPT_SSL_VERIFYHOST => false,
  CURLOPT_SSL_VERIFYPEER => false,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{ "email": "'.$username.'","password": "'.$password.'" }',
  CURLOPT_HTTPHEADER => array(
      'Content-Type: application/json'
  ),
  ));

  $response = curl_exec($curl);
  $authResponseObject = json_decode($response);
  curl_close($curl);
  //print_r($authResponseObject-> token);

  return $authResponseObject-> token;


```

### API Response Example: JSON Content

```
{
    "user": {
        "_id": "ID",
        "updatedAt": "yyy-mm-ddThh:mm:ssz",
        "createdAt": "yyy-mm-ddThh:mm:ssz",
        "username": "USERNAME",
        "email": "EMAIL,
        "phone_no": "NUMBER,
        "role": "ROLE",
        "image": "",
        "status": "Active",
        "role_id": "ROLE_ID",
        "activationToken": "TOKEN",
        "activationExpires": "yyy-mm-ddThh:mm:ssz",
        "createdBy": "USERNAME",
        "createdById": "ID",
        "vendor_name": "NAME",
        "password": "HASH",
        "__v": 0,
        "passwordResetExpires": "yyy-mm-ddThh:mm:ssz",
        "passwordResetToken": "TOKEN",
        "updatedBy": "ID"
    },
    "token": "TOKEN",
    "isLicensee": boolean
}

```



