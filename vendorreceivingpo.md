
# Vendor PO Receiving API

Vendors can setup to receiving purchase order (PO) data via API to their designated API endpoint. Below is information on how to configure your account and what the data will look like when receiving a PO.

### Vendor Account Configuration to send to API endpoint
![alt text](https://raw.githubusercontent.com/dn-as/MarketplaceApiDocs/c7562a0c9dd3ba6b6703b1a240c6c2f376784ce4/vendor%20po%20receiving%20api%20config.png  "Logo Title Text 1")

| Field  | Description | Required |
| ------------ | ------------ | ------------ |
| Vendor name  |  Marketplace records vendor name  | N  |
| Vendor type  | Marketplace records vendor type  |  N |
| IP Address to be Whitelisted  |  I.P. of server that will receive PO data | Y  |
| From Domain  |  | N  |
| To Domain  |   | N  |
| From Identity  | credential id required to send data  | Y  |
|  To Identity | purchaser identifier in PO receiving system  | Y  |
| Sender Domain  | Currently unused    | N  |
| Sender Identity  |  Currently unused | N  |
| Shared Secret  | credential secret required to send data   |  Y |
| UOM  | Currently unused    | N  |
| UNSPC  | Currently unused  | N  |
| PO Receiving API Endpoint  | Address of API endpoint that will receive data  | Y  |
| Additional Details | Currently unused  |  N |

### Sample XML data sent

```xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
    <header>
        <from>
            <credential domain="[From Domain From vendor E-doc configuration]">
                <identity>[From Identity From vendor E-doc configuration]</identity>
            </credential>
        </from>
        <to>
            <credential domain="To Domain From vendor E-doc configuration]">
                <identity>[To Identity From vendor E-doc configuration]</identity>
            </credential>
        </to>
        <sender domain="ToDomainTEST">
            <credential>
                <identity>[From Identity From vendor E-doc configuration]</identity>
                <sharedsecret>[Shared Secret From vendor E-doc configuration]</sharedsecret>
            </credential>
            <useragent>User Agent String</useragent>
        </sender>
    </header>
    <request deploymentMode="test">
        <orderrequest>
            <orderrequestheader orderDate="2024-01-30" orderID="336653" orderType="Purchase" type="new">
                <total currency="USD">
                    <money>1.5</money>
                </total>
                <shipto>
                    <address addressID="4" isoCountryCode="US">
                        <name xml:lang="en">testcxmluser</name>
                        <postaladdress name="default">
                            <deliverto>Store Manager</deliverto>
                            <street>DAY &amp; NITE/ALL SERVICE 10 CHARLES STREET</street>
                            <city>NEW HYDE PARK</city>
                            <state>NY</state>
                            <postalcode>11040</postalcode>
                            <country isoCountryCode="US">US</country>
                        </postaladdress>
                        <email name="default">some@email.com</email>
                    </address>
                </shipto>
                <billto addressID="4" isoCountryCode="US">
                    <address>
                        <name xml:lang="en">testcxmluser</name>
                        <postaladdress name="default">
                            <deliverto>Store Manager</deliverto>
                            <street>DAY &amp; NITE/ALL SERVICE 10 CHARLES STREET</street>
                            <city>NEW HYDE PARK</city>
                            <state>NY</state>
                            <postalcode>11040</postalcode>
                            <country isoCountryCode="US">US</country>
                        </postaladdress>
                        <email name="default">some@email.com</email>
                    </address>
                </billto>
                <shipping>
                    <money currency="USD">0.0</money>
                    <description xml:lang="en-US">Ground Shipping</description>
                </shipping>
                <paymentterm payInNumberOfDays="30" />
                <contact role="endUser">
                    <name xml:lang="en">Test Test</name>
                    <email name="default" />
                </contact>
                <extrinsic name="can_number" />
            </orderrequestheader>
            <additionalinformation>
                <procurementpersonnelname />
                <procurementpersonnelemail />
                <shipnoticeid />
                <shipviaid>GRND</shipviaid>
                <shipviadescription>Ground Shipping</shipviadescription>
            </additionalinformation>
            <itemout lineNumber="1" quantity="1.000000" requestedDeliveryDate="">
                <itemid>
                    <supplierpartid>12345</supplierpartid>
                    <supplierpartauxiliaryid>TEST12345</supplierpartauxiliaryid>
                </itemid>
                <itemdetail>
                    <unitprice>
                        <money currency="USD">1.500</money>
                    </unitprice>
                    <description xml:lang="en">LAMP-40W 130V CTD1</description>
                    <unitofmeasure />
                    <classification domain="UNSPSC">unknown</classification>
                    <extrinsic name="LineType">Quantity</extrinsic>
                </itemdetail>
            </itemout>
        </orderrequest>
    </request>
</root>
</xml>

```





