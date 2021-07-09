
<!--

---

title: downloadpolistjson

layout: template

filename: downloadpolistjson.md

--- 

-->




## API Download Purchase Orders

Get a list of purchase orders associated with a vendor account from the DNAS marketplace.

**Request URL**: [https://api-daynite.dnasmarketplace.com/v1/po/list](https://api-daynite.dnasmarketplace.com/v1/po/list)

**API HTTP request method**: POST  

### Required Headers

Content-Type: **application/json**

Authorization: **Bearer *TOKEN*** 

- *TOKEN* is retrieved through authorization API call using vendor account username and password
-  [Auth Token Guide](auth.md)
-  [Swagger Auth API Doc](https://punchout-daynite.dnasmarketplace.com/api-docs/)
-  [V1 API Doc](https://api-daynite.dnasmarketplace.com/docs/#!/PO/post_v1_po_list)

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
  CURLOPT_URL => 'https://api-daynite.dnasmarketplace.com/v1/po/list',
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
  url: 'https://api-daynite.dnasmarketplace.com/v1/po/list',
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

### Response Example
```
"success": true,
    "res": [
        {
            "id": 123,
            "sampro_po_number": 123456,
            "job_number": "",
            "work_order_number": "123456",
            "po_description": "Purchase for WO# 123456",
            "po_type": "Purchase",
            "ordered_by_pp": "Marketplace",
            "comment": "",
            "ship_address_street_1": "DAY & NITE REFRIGERATION",
            "ship_address_street_2": "10 CHARLES STREET",
            "ship_address_street_3": "",
            "ship_address_street_4": "",
            "ship_address_city": "NEW HYDE PARK",
            "ship_address_state": "NY",
            "ship_address_postal_code": "11040",
            "ship_to_code": "StockLocation",
            "ship_to_branch": "",
            "wo_id": 675981,
            "client_site_id": "123456",
            "client_site_name": "BRYANT PARK HOTEL",
            "client_site_address": "40 WEST 40TH STREET, New York, NY, 10018",
            "cart_id": 12,
            "cart_version": 2,
            "cart_total": 0,
            "cart_assigned_to_id": null,
            "cart_assigned_to_name": null,
            "cart_created_by_id": "ID",
            "cart_created_by_name": "John Smith",
            "country": "US",
            "buyer_part_number": "ID",
            "seller_part_number": "ID",
            "vendor_id": "",
            "vendor_name": "",
            "vendor_email": "",
            "pp_id": "ID",
            "pp_email": "jsmith@wearetheone.com",
            "pp_name": "Robert Smith",
            "branch": "",
            "po_vendor_id": null,
            "date_requested": "2019-09-16",
            "invoice_status": null,
            "status": "Accepted",
            "reason_for_rejection": null,
            "createdBy": null,
            "is_deleted": 0,
            "ship_notice_id": null,
            "ship_via_id": null,
            "ship_via_description": null,
            "po_oa_reject_count": 0,
            "po_asn_reject_count": 0,
            "po_invoice_reject_count": 0,
            "po_promised_date": null,
            "createdAt": "2019-09-23T10:44:00.000Z",
            "updatedAt": "2021-06-28T18:56:46.000Z"
        },
        .... More PO JSON elements
	]
}

```

