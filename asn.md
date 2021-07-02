
<!--

---

title: asn

layout: template

filename: asn.md

--- 

-->




## API Advance Ship Notice

Upload data to process an advance shipping notice for a existing purchase order

**Request URL**: [https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlVendorASNToDatabase](https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlVendorASNToDatabase)

**API HTTP request method**: POST  

### Required Headers

Content-Type: **text/xml**

### Required Body
cXML Content

More information about fulfInvoiceDetailill cXML:
[xml.cxml.org/current/cXMLUsersGuide](http://xml.cxml.org/current/cXMLUsersGuide.pdf)

### Required Parameters
None

### Sample cXML file content
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE cXML SYSTEM "http://xml.cXML.org/schemas/cXML/1.2.020/InvoiceDetail.dtd">
<cXML payloadID="" timestamp="">
	<Header>
		<From>
			<Credential domain="">
				<Identity></Identity>
			</Credential>
		</From>
		<To>
			<Credential domain="">
				<Identity></Identity>
			</Credential>
		</To>
		<Sender>
			<Credential domain="">
				<Identity>user@domain.com/Identity> <!--marketplace email-->
				<SharedSecret>password</SharedSecret> <!--marketplace password-->
			</Credential>
			<UserAgent></UserAgent>
		</Sender>
	</Header>
	<Request>
		<ShipNoticeRequest>
			
            <ShipNoticeHeader  operation="update" noticeDate="2019-04-22T12:00:00" shipmentDate="2019-04-22T12:00:00" deliveryDate="2019-04-23T12:00:00">
				<Contact role="shipFrom">
					<Name xml:lang="en-US">Company Name</Name>
					<PostalAddress>
						<Street>1234 drive Rd</Street>
						<Street/>
						<City>Beverly Hills</City>
						<State>CA</State>
						<PostalCode>90210</PostalCode>
						<Country isoCountryCode="US">US</Country>
					</PostalAddress>
				</Contact>
			</ShipNoticeHeader>
			
            <ShipControl>
				<CarrierIdentifier domain="">UPSN</CarrierIdentifier>
				<CarrierIdentifier domain="companyName">United Parcel Service</CarrierIdentifier>
				<ShipmentIdentifier>1Z123456789</ShipmentIdentifier> 
			</ShipControl>
			
            <ShipNoticePortion>
				
                <OrderReference orderID="123456" orderDate="2019-04-22T12:00:00"> <!--orderID is Sampro PO number-->
					<DocumentReference payloadID=""/>
				</OrderReference>
				
                <ShipNoticeItem quantity="1" lineNumber="1"> <!-- ShipNoticeItem is one item in PO -->
					<ItemID>
						<SupplierPartID>Test1</SupplierPartID> <!-- SupplierPartID is Vendor Part identifier from PO -->
					</ItemID>   
					<UnitOfMeasure>EA</UnitOfMeasure>
					<Packaging>
						<PackagingCode xml:lang="en-US">1Z123456789</PackagingCode> <!-- Line Item tracking number-->
						<Dimension quantity="1" type="weight"/>
						<UnitOfMeasure>EA</UnitOfMeasure>
					</Packaging>
				</ShipNoticeItem>				
               
			</ShipNoticePortion>
		</ShipNoticeRequest>
	</Request>
</cXML>


```
### Minimum required cXML element data

Provide your Marketplace login ID in "Sender Identity" field and Marketplace Password in "Shared Secret" field.

<!-- |Marketplace OA Columns| Manual Upload CSV columns|  API upload cXML Elements&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|--|--|--|
| Vendor Part	|	ns1:vendornumber	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus>\<ItemIn>\<ItemID>\<SupplierPartID>	|
| Quantity	|	ns1:Quantity	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus quantity="" type="">\<ItemIn quantity="1">	|
| U/M	|	ns1:UnitOfMeasure	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus>\<ItemIn>\<ItemDetail>\<UnitOfMeasure>	|
| Price	|	ns1:UnitPrice	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus>\<ItemIn>\<ItemDetail>\<UnitPrice>\<Money currency="">	|
| Date Promised	|	LineItemPromisedDate	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus deliveryDate="">	|
| Long Description	|	ns1:ItemDescription	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus>\<Comments xml:lang="">	| -->

There can be more than one ShipNoticeItem as a line item on the purchase order.

### Node.js AXIOS Example
```
var axios = require('axios');
var fs = require('fs')

fs.readFile('/path/to/file.cXML', 'utf8', function (err,data) {
  if (err) {
    return console.log(err);
  }
  cXMLContent = data;
});


var data = cXMLContent;

var config = {
  method: 'post',
  url: 'https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlVendorASNToDatabase',
  headers: { 
    'Content-Type': 'application/xml'
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

### PHP Curl Example

```
<?php

$curl = curl_init();

$cxmlcontent = file_get_contents('/path/to/file.cXML');

<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlVendorASNToDatabase',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => $cxmlcontent, 
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/xml'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;



```
