
<!--

---

title: orderacknowledgment

layout: template

filename: orderacknowledgment.md

--- 

-->




## API Order Acknowledgment

Upload data to process a order acknowledgment for a existing purchase order

**Request URL**: [https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlOAToDatabase](https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlOAToDatabase)

**API HTTP request method**: POST  

### Required Headers

Content-Type: **text/xml**

### Required Body
cXML Content

cXML file must follow [fulfill.dtd](http://xml.cxml.org/current/Fulfill.zip) standards

More information about fulfill cXML:
[https://punchoutcommerce.com/guides/transactions/cxml-confirmation-request/](https://punchoutcommerce.com/guides/transactions/cxml-confirmation-request/)
[xml.cxml.org/current/cXMLUsersGuide](http://xml.cxml.org/current/cXMLUsersGuide.pdf)

### Required Parameters
None

### Sample cXML file content
```
<?xml version="1.0"?>
<!DOCTYPE cXML SYSTEM "http://xml.cxml.org/schemas/cXML/1.2.014/Fulfill.dtd">
<cXML payloadID="" timestamp="2021-02-23T09:15:50-0600" xml:lang="en-US">
  <Header>
    <From>
      <Credential domain="DUNS">
        <Identity>802661173</Identity>
      </Credential>
    </From>
    <To>
      <Credential domain="NetworkID">
        <Identity>daynite</Identity>
      </Credential>
    </To>
    <Sender>
      <Credential domain="DUNS">
        <Identity>user@email.com</Identity>
        <SharedSecret>password123</SharedSecret>
      </Credential>
      <UserAgent/>
    </Sender>
  </Header>
  <Request>
    <ConfirmationRequest>
      <ConfirmationHeader type="detail" noticeDate="2021-02-23T09:15:50" invoiceID="269765">
        <Total>
          <Money currency="USD">1.22</Money>
        </Total>
        <Shipping>
          <Money currency="USD">0.00</Money>
          <Description xml:lang="en-US">UPS GROUND</Description>
        </Shipping>
        <Tax>
          <Money currency="USD">0.1</Money>
          <Description xml:lang=""/>
        </Tax>
        <Contact role="shipFrom">
          <Name xml:lang="en-US">NEW JERSEY</Name>
          <PostalAddress>
            <Street></Street>
            <City>Lumberton</City>
            <State>NJ</State>
            <PostalCode>08048</PostalCode>
            <Country isoCountryCode="US">USA</Country>
          </PostalAddress>
          <Phone>
            <TelephoneNumber>
              <CountryCode isoCountryCode=""/>
              <AreaOrCityCode/>
              <Number>800-332-2500</Number>
            </TelephoneNumber>
          </Phone>
        </Contact>
      </ConfirmationHeader>
      <OrderReference orderID="269765" orderDate="0021-02-01">
        <DocumentReference payloadID="user@email.com"/>
      </OrderReference>
      <ConfirmationItem quantity="2" lineNumber="1">
        <UnitOfMeasure>EA</UnitOfMeasure>
        <ConfirmationStatus quantity="2" type="accept">
          <UnitOfMeasure>EA</UnitOfMeasure>
          <ItemIn quantity="2">
            <ItemID>
              <SupplierPartID>261950</SupplierPartID>
            </ItemID>
            <ItemDetail>
              <UnitPrice>
                <Money currency="USD">0.5</Money>
              </UnitPrice>
              <Description xml:lang="en-US">NUT</Description>
              <UnitOfMeasure>EA</UnitOfMeasure>
              <Classification domain=""/>
              <ManufacturerPartID>261950</ManufacturerPartID>
              <ManufacturerName></ManufacturerName>
              <URL></URL>
            </ItemDetail>
          </ItemIn>
        </ConfirmationStatus>
      </ConfirmationItem>
      <ConfirmationItem quantity="2" lineNumber="2">
        <UnitOfMeasure>EA</UnitOfMeasure>
        <ConfirmationStatus quantity="2" type="accept">
          <UnitOfMeasure>EA</UnitOfMeasure>
          <ItemIn quantity="2">
            <ItemID>
              <SupplierPartID>2271092</SupplierPartID>
            </ItemID>
            <ItemDetail>
              <UnitPrice>
                <Money currency="USD">0.12</Money>
              </UnitPrice>
              <Description xml:lang="en-US">SCREW  DOOR HINGE THREAD</Description>
              <UnitOfMeasure>EA</UnitOfMeasure>
              <Classification domain=""/>
              <ManufacturerPartID>2271092</ManufacturerPartID>
              <ManufacturerName></ManufacturerName>
              <URL></URL>
            </ItemDetail>
          </ItemIn>
        </ConfirmationStatus>
      </ConfirmationItem>
    </ConfirmationRequest>
  </Request>
</cXML>

```
### Minimum required cXML element data

Provide your Marketplace login ID in "Sender Identity" field and Marketplace Password in "Shared Secret" field.

|Marketplace OA Columns| Manual Upload CSV columns|  API upload cXML Elements&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;|
|--|--|--|
| Vendor Part	|	ns1:vendornumber	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus>\<ItemIn>\<ItemID>\<SupplierPartID>	|
| Quantity	|	ns1:Quantity	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus quantity="" type="">\<ItemIn quantity="1">	|
| U/M	|	ns1:UnitOfMeasure	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus>\<ItemIn>\<ItemDetail>\<UnitOfMeasure>	|
| Price	|	ns1:UnitPrice	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus>\<ItemIn>\<ItemDetail>\<UnitPrice>\<Money currency="">	|
| Date Promised	|	LineItemPromisedDate	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus deliveryDate="">	|
| Long Description	|	ns1:ItemDescription	|	\<cXML>\<Request>\<ConfirmationRequest>\<ConfirmationItem>\<ConfirmationStatus>\<Comments xml:lang="">	|

There can be more than one ConfirmationItem as a line item on the purchase order.

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
  url: 'https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlOAToDatabase',
  headers: { 
    'Content-Type': 'text/xml'
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

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://api-daynite.dnasmarketplace.com/v1/xmlParser/xmlOAToDatabase',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => $cxmlcontent,
  CURLOPT_HTTPHEADER => array(
    'Content-Type: text/xml'
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
    "message": "OA cXML mapped successfully into DB",
    "response": {
        "status": 200,
        "message": "OA items mapped successfully from OA cXML",
        "data": [
            {
                "success": true,
                "message": "Po status and Acknowledgement updated",
                "res": {
                    "id": 4201,
                    "ns1:UnitOfMeasure": "EA",
                    "ns1:BuyerPartNumber": "261950",
                    "ns1:SellerPartNumber": "261950",
                    "ns1:PODescription": "NUT",
                    "ns1:Quantity": "2",
                    "DatePromised": "",
                    "LineItemPromisedDate": "",
                    "ns1:UnitPrice": "0.5",
                    "ns1:comment": "",
                    "ns1:PONumber": "269765",
                    "ns1:PurchaseOrderType": "detail",
                    "ns1:OrderedBy": "NEW JERSEY",
                    "ns1:ShipAddressStreet1": "NEW JERSEY",
                    "ns1:ShipAddressStreet2": "",
                    "country": "USA",
                    "ns1:ShipAddressCity": "Lumberton",
                    "ns1:ShipAddressState": "NJ",
                    "ns1:ShipAddressPostalCode": "08048",
                    "DateRequested": "0021-02-01",
                    "po_id": 755,
                    "is_latest": 1,
                    "is_approved": 0,
                    "version": 20,
                    "updatedAt": "2021-07-07T18:26:45.000Z",
                    "createdAt": "2021-07-07T18:26:45.000Z"
                }
            },
            {
                "success": true,
                "message": "Po status and Acknowledgement updated",
                "res": {
                    "id": 4202,
                    "ns1:UnitOfMeasure": "EA",
                    "ns1:BuyerPartNumber": "2271092",
                    "ns1:SellerPartNumber": "2271092",
                    "ns1:PODescription": "SCREW  DOOR HINGE THREAD",
                    "ns1:Quantity": "2",
                    "DatePromised": "",
                    "LineItemPromisedDate": "",
                    "ns1:UnitPrice": "0.12",
                    "ns1:comment": "",
                    "ns1:PONumber": "269765",
                    "ns1:PurchaseOrderType": "detail",
                    "ns1:OrderedBy": "NEW JERSEY",
                    "ns1:ShipAddressStreet1": "NEW JERSEY",
                    "ns1:ShipAddressStreet2": "",
                    "country": "USA",
                    "ns1:ShipAddressCity": "Lumberton",
                    "ns1:ShipAddressState": "NJ",
                    "ns1:ShipAddressPostalCode": "08048",
                    "DateRequested": "0021-02-01",
                    "po_id": 755,
                    "is_latest": 1,
                    "is_approved": 0,
                    "version": 20,
                    "updatedAt": "2021-07-07T18:26:45.000Z",
                    "createdAt": "2021-07-07T18:26:45.000Z"
                }
            }
        ]
    }
}
```