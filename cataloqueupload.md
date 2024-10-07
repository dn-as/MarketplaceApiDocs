<!--

---

layout: template

title: cataloqueupload

filename: cataloqueupload.md

--- 

-->

## API Catalogue Uploads

Used to upload bulk data about vendor products to the DNAS marketplace.

**Request URL**: [https://products-daynite.dnasmarketplace.com/bulkUpload/catlog-upload](https://products-daynite.dnasmarketplace.com/bulkUpload/catlog-upload)

**API HTTP request method**: POST  

### Required Headers

Content-Type: **multipart/form-data**

Authorization: **Bearer *TOKEN*** 

- *TOKEN* is retrieved through authorization API call using vendor account username and password
- [Auth Token Guide](auth.md)
-  [Swagger Auth API Doc](https://punchout-daynite.dnasmarketplace.com/api-docs/)

### Required Body
**file_type**: values 0, 1, 2

 0 - Remove all existing products and add new products

 1 - Update existing product records

 2 - Insert new products without replacing existing products




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
 
| Column Name                | Description                                                                 | Mandatory | Max Length | Business Rules/Validations                       |
|---------------------------|-----------------------------------------------------------------------------|-----------|------------|-------------------------------------------------|
| Product Name              | Name                                                                       | Yes       | 100        | Alpha Numeric                                   |
| Manufacturer Name         | Original Equipment Manufacturer (Standard Special Characters Set not allowed.)| Yes       | 100        | Alpha Numeric                                   |
| Manufacturer Part Number  | OEM Part #                                                                 | Yes       | 30         | Alpha Numeric                                   |
| Vendor Part Number        | Vendor Material Part Number                                                | Yes       | 30         | Alpha Numeric                                   |
| Quantity on Hand          | Total number of quantity available                                         | No        | 10         | Number                                          |
| List Price                | Original List Price                                                        | No        | 20         | Number                                          |
| Discounted Price          | Contract Price                                                             | No        | 20         | Number                                          |
| Lead Time                 | Number of Days required to Pack and Ship the product                       | No        | 2          | Number                                          |
| Product Images            | Product Image URL. (Multiple Image URL can be uploaded with a ';' in between)| No        | NA         | Max 4 images will be allowed                    |
| Fits Models               | Fits which model(s)                                                        | Yes       | NA         | Alpha Numeric                                   |
| Specifications            | Short Description                                                          | No        | NA         | Alpha Numeric                                   |
| Long Description          | Long Description                                                           | No        | NA         | Alpha Numeric                                   |
| UOM Name                  | Unit of measurement name                                                   | No        | NA         | Alpha Numeric                                   |
| UOM Quantity              | Unit of measurement quantity                                               | No        | NA         | Number                                          |
| Web link                  | URL link to Vendor Web Page                                                | No        | NA         | Alpha Numeric                                   |
| URL Image                 | Thumbnail URL                                                              | No        | NA         | Alpha Numeric                                   |
| Minimum Ship Quantity     | Minimum Ship Quantity                                                      | No        | NA         | Number                                          |
| COO                       | Country of Origin                                                          | No        | NA         | Alpha Numeric                                   |
| COO Name                  | Country of Origin Name                                                     | No        | NA         | Alpha Numeric                                   |
| Segment                   | Product Segment Name                                                       | No        | NA         | Alpha Numeric                                   |
| Family                    | Product Family Name                                                        | No        | NA         | Alpha Numeric                                   |
| UNSPSC                    | United Nations Standard Products and Services Code (UNSPSC) for use in eCommerce| No     | NA         | Number                                          |
| In Stock                  | In Stock                                                                   | No        | NA         | Number                                          |
| Missing Field             | Missing Description                                                        | No        | NA         | Number                                          |


### Example Response on successful upload
```
{
    "msg": "File successfuly uploaded.",
    "result": {
        "__v": 0,
        "updatedAt": "2021-07-07T18:22:05.242Z",
        "createdAt": "2021-07-07T18:22:05.242Z",
        "vendor_id": "10000-NY",
        "file_path": "https://marketplacednuat.s3.amazonaws.com/product_files/uploaded_filename.csv",
        "isImported": 0,
        "records_uploaded": 1,
        "isPartialUpload": 0,
        "created_on": "2021-07-07T18:22:05.241Z",
        "created_by": "5d0a15938271f823b41f43e9",
        "modified_on": "2021-07-07T18:22:05.241Z",
        "modified_by": "5d0a15938271f823b41f43e9",
        "created_by_name": "username",
        "vendor_name": "3 WIRE Northern",
        "_id": "",
        "id": ""
    },
    "status": 200
}
```
