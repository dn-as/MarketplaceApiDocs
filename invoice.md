
<!--

---

title: invoice

layout: template

filename: invoice.md

--- 

-->




## API Invoice

Upload data to process an invoice for a existing purchase order

**Request URL**: [https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlVendorInvoiceToDatabase](https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlVendorInvoiceToDatabase)

**API HTTP request method**: POST  

### Required Headers

Content-Type: **text/xml**

### Required Body
cXML Content

More information about InvoiceDetail cXML:
[http://xml.cxml.org/current/cXMLReferenceGuide.pdf](http://xml.cxml.org/current/cXMLReferenceGuide.pdf)

### Required Parameters
None

### Sample cXML file content
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE cXML SYSTEM "http://xml.cXML.org/schemas/cXML/1.2.020/InvoiceDetail.dtd">
<cXML payloadID="20190318 0942100" timestamp="2019-03-18T09:42:10">
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
				<Identity>user@email.com</Identity>
				<SharedSecret>password</SharedSecret>
			</Credential>
			<UserAgent></UserAgent>
		</Sender>
	</Header>
	<Request>
		<InvoiceDetailRequest>
			<InvoiceDetailRequestHeader invoiceID="21807883" purpose="standard" operation="new" invoiceDate="2018-05-21T12:00:00">
				<InvoiceDetailHeaderIndicator/>
				<InvoiceDetailLineIndicator isTaxInLine="no"/>
				<InvoicePartner>
					<Contact role="remitTo">
						<Name xml:lang="en-US">Company Name</Name>
						<PostalAddress>
							<Street>300 S. Ave</Street>
							<Street>test Street</Street>
							<City>ACME</City>
							<State>IL</State>
							<PostalCode>12345</PostalCode>
							<Country isoCountryCode="US">US</Country>
						</PostalAddress>
					</Contact>
				</InvoicePartner>
				<InvoiceDetailShipping>
					<Contact role="shipFrom">
						<Name xml:lang="en-US"/>
					</Contact>
				</InvoiceDetailShipping>
				<InvoiceDetailPaymentTerm payInNumberOfDays="30"/>
				<PaymentTerm payInNumberOfDays="30"/>
			</InvoiceDetailRequestHeader>
			<InvoiceDetailOrder>
				<InvoiceDetailOrderInfo>
					<OrderReference orderID="246414"/>
				</InvoiceDetailOrderInfo>
				<InvoiceDetailItem invoiceLineNumber="1" quantity="1.000000">
					<UnitOfMeasure>EA</UnitOfMeasure>
					<UnitPrice>
						<Money currency="USD">166.50</Money>
					</UnitPrice>
					<InvoiceDetailItemReference lineNumber="1">
						<ItemID>
							<SupplierPartID>ZMO210507A</SupplierPartID>
						</ItemID>
						<Description xml:lang="en">Z40 BLADE</Description>
					</InvoiceDetailItemReference>
					<SubtotalAmount>
						<Money currency="USD">166.50</Money>
					</SubtotalAmount>
					<Tax/>
				</InvoiceDetailItem>
				<InvoiceDetailItem invoiceLineNumber="1" quantity="1.000000">
					<UnitOfMeasure>EA</UnitOfMeasure>
					<UnitPrice>
						<Money currency="USD">132.50</Money>
					</UnitPrice>
					<InvoiceDetailItemReference lineNumber="1">
						<ItemID>
							<SupplierPartID>ZMO210507A</SupplierPartID>
						</ItemID>
						<Description xml:lang="en">Z40 BLADE</Description>
					</InvoiceDetailItemReference>
					<SubtotalAmount>
						<Money currency="USD">132.50</Money>
					</SubtotalAmount>
					<Tax/>
				</InvoiceDetailItem>
			</InvoiceDetailOrder>
			<InvoiceDetailSummary>
				<SubtotalAmount>
					<Money currency="USD">166.50</Money>
				</SubtotalAmount>
				<SpecialHandlingAmount>
					<Money currency="USD">0</Money>
				</SpecialHandlingAmount>
				<GrossAmount>
					<Money currency="USD">166.5</Money>
				</GrossAmount>
				<InvoiceDetailDiscount>
					<Money currency="USD">0</Money>
				</InvoiceDetailDiscount>
				<NetAmount>
					<Money currency="USD">166.5</Money>
				</NetAmount>
			</InvoiceDetailSummary>
		</InvoiceDetailRequest>
	</Request>
</cXML>

```
### Minimum required cXML element data

Provide your Marketplace login ID in "Sender Identity" field and Marketplace Password in "Shared Secret" field.


| Description            | Manual Upload Invoice Columns              | cXML Element                                                                                                                          | Required |
|------------------------|--------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|----------|
| invoice number         | invoiceID                                  | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader invoiceID="276798">                                                        | N        |
| Billing Address        | InvoicePartner:Name                        | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader>\<InvoicePartner>\<Contact role="remitTo">\<Name xml:lang="en-US">            | N        |
|                        | InvoicePartner:Street1                     | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader>\<InvoicePartner>\<Contact role="remitTo">\<PostalAddress>\<Street>            | N        |
|                        | InvoicePartner:Street2                     | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader>\<InvoicePartner>\<Contact role="remitTo">\<PostalAddress>\<Street>            | N        |
|                        | InvoicePartner:City                        | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader>\<InvoicePartner>\<Contact role="remitTo">\<PostalAddress>\<City>              | N        |
|                        | InvoicePartner:State                       | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader>\<InvoicePartner>\<Contact role="remitTo">\<PostalAddress>\<State>             | N        |
|                        | InvoicePartner:PostalCode                  | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader>\<InvoicePartner>\<Contact role="remitTo">\<PostalAddress>\<PostalCode>        | N        |
|                        | InvoicePartner:Country                     | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader>\<InvoicePartner>\<Contact role="remitTo">\<PostalAddress>\<Country>           | N        |
| invoice date           | invoiceDate                                | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailRequestHeader invoiceDate="2018-05-21T12:00:00">                                         | N        |
| Day and Nite PO Number | PONumber                                   | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailOrderInfo>\<OrderReference orderID="246414"/>                                             | Y        |
| part number            | SellerPartNumber                           | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailOrder>\<InvoiceDetailItem>\<InvoiceDetailItemReference>\<ItemID>\<SupplierPartID>            | Y        |
| description            | ItemDescription                            | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailOrder>\<InvoiceDetailItem>\<InvoiceDetailItemReference>\<ItemID>\<Description xml:lang="en"> | N        |
| WH                     | InvoiceDetailItem:UnitOfMeasure            | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailOrder>\<InvoiceDetailItem>\<UnitOfMeasure>                                                 | N        |
| Ship quantity          | InvoiceDetailItem:quantity                 | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailOrder>\<InvoiceDetailItem quantity="1.000000">                                            | N        |
| unit price             | InvoiceDetailItem:UnitPrice                | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailOrder>\<InvoiceDetailItem>\<UnitPrice>\<Money currency="USD">                               | Y        |
| Total gross            | InvoiceDetailSummary:GrossAmount           | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailSummary>\<GrossAmount>                                                                    | N        |
| Total freight          | InvoiceDetailSummary:SpecialHandlingAmount | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailSummary>\<SpecialHandlingAmount>                                                          | N        |
| Total amount           | InvoiceDetailSummary:NetAmount             | \<Request>\<InvoiceDetailRequest>\<InvoiceDetailSummary>\<NetAmount>                                                                      | Y        |

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
  url: 'https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlVendorInvoiceToDatabase',
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
  CURLOPT_URL => 'https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlVendorInvoiceToDatabase',
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

### Response Example
```
{
    "success": true,
    "message": "Invoice mapped successfully",
    "response": {
        "status": 200,
        "message": "Invoice items added from Invoice cXML",
        "data": [
            {
                "success": true,
                "res": {
                    "id": 3551,
                    "InvoiceDetailItem:invoiceLineNumber": "1",
                    "InvoiceDetailItem:quantity": "1",
                    "InvoiceDetailItem:UnitOfMeasure": "EA",
                    "InvoiceDetailItem:UnitPrice": "166.50",
                    "InvoiceDetailItem:Currency": "USD",
                    "ItemDescription": "Z40 BLADE",
                    "SellerPartNumber": "ZMO210507A",
                    "InvoiceDetailItem:SubtotalAmount": "166.50",
                    "InvoiceDetailItem:Tax": "",
                    "invoiceID": "21807883",
                    "purpose": "standard",
                    "operation": "new",
                    "invoiceDate": "2018-05-21T12:00:00",
                    "InvoiceDetailHeaderIndicator": "",
                    "isTaxInLine": "no",
                    "InvoicePartner:Role": "remitTo",
                    "InvoicePartner:Name": "Company Name",
                    "InvoicePartner:Lang": "en-US",
                    "InvoicePartner:Street1": "300 S. Ave",
                    "InvoicePartner:Street2": "test Street",
                    "InvoicePartner:City": "ACME",
                    "InvoicePartner:State": "IL",
                    "InvoicePartner:PostalCode": "12345",
                    "InvoicePartner:Country": "US",
                    "InvoicePartner:isoCountryCode": "US",
                    "InvoiceDetailShipping:Role": "shipFrom",
                    "InvoiceDetailShipping:Name": "en-US",
                    "InvoiceDetailPaymentTerm:payInNumberOfDays": "30",
                    "PaymentTerm:payInNumberOfDays": "30",
                    "PONumber": "246414",
                    "InvoiceDetailSummary:SubtotalAmount": "166.50",
                    "InvoiceDetailSummary:SpecialHandlingAmount": "0",
                    "InvoiceDetailSummary:GrossAmount": "166.5",
                    "InvoiceDetailSummary:InvoiceDetailDiscount": "0",
                    "InvoiceDetailSummary:NetAmount": "166.5",
                    "po_id": 510,
                    "is_latest": 1,
                    "version": 7,
                    "is_approved": 0,
                    "updatedAt": "2021-07-09T20:00:35.000Z",
                    "createdAt": "2021-07-09T20:00:35.000Z"
                }
            },
            {
                "success": true,
                "res": {
                    "id": 3552,
                    "InvoiceDetailItem:invoiceLineNumber": "1",
                    "InvoiceDetailItem:quantity": "1",
                    "InvoiceDetailItem:UnitOfMeasure": "EA",
                    "InvoiceDetailItem:UnitPrice": "132.50",
                    "InvoiceDetailItem:Currency": "USD",
                    "ItemDescription": "Z40 BLADE",
                    "SellerPartNumber": "ZMO210507A",
                    "InvoiceDetailItem:SubtotalAmount": "132.50",
                    "InvoiceDetailItem:Tax": "",
                    "invoiceID": "21807883",
                    "purpose": "standard",
                    "operation": "new",
                    "invoiceDate": "2018-05-21T12:00:00",
                    "InvoiceDetailHeaderIndicator": "",
                    "isTaxInLine": "no",
                    "InvoicePartner:Role": "remitTo",
                    "InvoicePartner:Name": "Company Name",
                    "InvoicePartner:Lang": "en-US",
                    "InvoicePartner:Street1": "300 S. Ave",
                    "InvoicePartner:Street2": "test Street",
                    "InvoicePartner:City": "ACME",
                    "InvoicePartner:State": "IL",
                    "InvoicePartner:PostalCode": "12345",
                    "InvoicePartner:Country": "US",
                    "InvoicePartner:isoCountryCode": "US",
                    "InvoiceDetailShipping:Role": "shipFrom",
                    "InvoiceDetailShipping:Name": "en-US",
                    "InvoiceDetailPaymentTerm:payInNumberOfDays": "30",
                    "PaymentTerm:payInNumberOfDays": "30",
                    "PONumber": "246414",
                    "InvoiceDetailSummary:SubtotalAmount": "166.50",
                    "InvoiceDetailSummary:SpecialHandlingAmount": "0",
                    "InvoiceDetailSummary:GrossAmount": "166.5",
                    "InvoiceDetailSummary:InvoiceDetailDiscount": "0",
                    "InvoiceDetailSummary:NetAmount": "166.5",
                    "po_id": 510,
                    "is_latest": 1,
                    "version": 7,
                    "is_approved": 0,
                    "updatedAt": "2021-07-09T20:00:35.000Z",
                    "createdAt": "2021-07-09T20:00:35.000Z"
                }
            }
        ]
    }
}
```
