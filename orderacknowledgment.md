
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

More information about fulfill cXML: [Link](https://punchoutcommerce.com/guides/transactions/cxml-confirmation-request/)

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
