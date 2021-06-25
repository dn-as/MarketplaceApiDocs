## API Catalogue Uploads

Used to upload bulk data about vendor products to the DNAS marketplace.

**Request URL**: [https://products-daynite.dnasmarketplace.com/bulkUpload/catlog-upload](https://products-daynite.dnasmarketplace.com/bulkUpload/catlog-upload)

**API HTTP request method**: POST

### Required Headers

Content-Type: **multipart/form-data**

Authorization: **Bearer *TOKEN***

- *TOKEN* is retrieved through authorization API call using vendor account username and password

### Required Body
**file_type**: values 0, 1, 2

 0. Remove all existing products and add new products
 1. Update existing product records
 2. Insert new products without replacing existing products




**csv_file**: /path/to/csv/file.csv

### Required Parameters
None

### PHP Curl Example
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://products-daynite.dnasmarketplace.com/bulkUpload/catlog-upload',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => array('file_type' => '0',
							  'csv_file'=> new CURLFILE('/path/to/csv/file.csv')),
  CURLOPT_HTTPHEADER => array('Authorization: Bearer TOKEN'),
));

$response = curl_exec($curl);
curl_close($curl);

echo  $response;
```
### Node.js AXIOS Example
```
var axios = require('axios');
var FormData = require('form-data');
var fs = require('fs');
var data = new FormData();
data.append('file_type', '0');
data.append('csv_file', fs.createReadStream('/path/to/file.csv'));

var config = {
  method: 'post',
  url: 'https://products-daynite.dnasmarketplace.com/bulkUpload/catlog-upload',
  headers: { 
    'Authorization': 'Bearer TOKEN', 
    ...data.getHeaders()
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
### CSV File Columns and sample file

[Sample File](https://dn-as.github.io/MarketplaceApiDocs/product_sample_file.csv)

| Column name 	|
|--						|
|	product_name							|
|	manufacturer_name					|
|	manufacturer_part_number		|
|	vendor_part_number				|
|	quantity_on_hand						|
|	list_price		|
|	discounted_price		|
|	lead_time		|
|	fits_models		|
|	specifications		|
|	long_description		|
|	uom_name		|
|	uom_quantity		|
|	web_link		|
|	url_image		|
|	minimum_ship_quantity		|
|	coo		|
|	coo_name		|
|	segment		|
|	family		|
|	unspsc		|
|	in_stock		|
|	product_images		|

