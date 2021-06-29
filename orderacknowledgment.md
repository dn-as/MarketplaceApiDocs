
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
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE cXML SYSTEM "http://xml.cXML.org/schemas/cXML/1.2.046/Fulfill.dtd">
<cXML payloadID="" xml:lang="en-CA" timestamp="">
    <Header>
        <From>
            <Credential domain="">
                <Identity></Identity>
            </Credential>
        </From>
        <To>
            <!-- The buying marketplace and member organization. -->
            <Credential domain="" type="">
                <Identity></Identity>
            </Credential>
        </To>
        <Sender>
            <!-- The supplier -->
            <Credential domain="">
                <Identity> </Identity>
                <SharedSecret> </SharedSecret>
            </Credential>
            <UserAgent></UserAgent>
        </Sender>
    </Header>
    <Request deploymentMode="">
        <ConfirmationRequest>
            <ConfirmationHeader type="" noticeDate="" invoiceID="">
                <Total>
                    <Money currency=""></Money>
                </Total>
                <Shipping>
                    <Money currency=""></Money>
                    <Description xml:lang=""></Description>
                </Shipping>
                <Tax>
                    <Money currency=""></Money>
                    <Description xml:lang=""></Description>
                </Tax>
                <Contact role="">
                    <Name xml:lang=""></Name>
                    <PostalAddress>
                        <Street></Street>
                        <City></City>
                        <State></State>
                        <PostalCode></PostalCode>
                        <Country isoCountryCode=""></Country>
                    </PostalAddress>
                    <Phone>
                        <TelephoneNumber>
                            <CountryCode isoCountryCode=""></CountryCode>
                            <AreaOrCityCode></AreaOrCityCode>
                            <Number></Number>
                        </TelephoneNumber>
                    </Phone>
                </Contact>
                <Comments xml:lang=""></Comments>
            </ConfirmationHeader>
            <!-- The orderID and orderDate attributes are not required in the OrderReference element. -->
            <OrderReference orderID="" orderDate="">
                <DocumentReference payloadID=""/>
            </OrderReference>
            <ConfirmationItem lineNumber="1" quantity="">
                <UnitOfMeasure> </UnitOfMeasure>
                <ConfirmationStatus quantity="" type="" shipmentDate="" deliveryDate="">
                    <UnitOfMeasure> </UnitOfMeasure>
                    <ItemIn quantity="" lineNumber="">
                        <ItemID>
                            <SupplierPartID>YYYX4</SupplierPartID>
                        </ItemID>
                        <ItemDetail>
                            <UnitPrice>
                                <Money currency="USD"></Money>
                            </UnitPrice>
                            <Description xml:lang="en"></Description>
                            <UnitOfMeasure> </UnitOfMeasure>
                            <Classification domain=""></Classification>
                            <ManufacturerPartID></ManufacturerPartID>
                            <ManufacturerName></ManufacturerName>
                            <URL></URL>
                        </ItemDetail>
                    </ItemIn>
                    <Comments xml:lang="en-CA"></Comments>
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