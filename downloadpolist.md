
<!--

---

title: downloadpolist

layout: template

filename: downloadpolist.md

--- 

-->




## API Download Purchase Orders

Get a list of purchase orders associated with a vendor account from the DNAS marketplace.

**Request URL**: [https://api-daynite.dnasmarketplace.com/v1/cart/downloadpolist](https://api-daynite.dnasmarketplace.com/v1/cart/downloadpolist)

**API HTTP request method**: POST  

### Required Headers

Content-Type: **application/json**

Authorization: **Bearer *TOKEN*** 

- *TOKEN* is retrieved through authorization API call using vendor account username and password
-  [Auth Token Guide](auth.md)
-  [Swagger Auth API Doc](https://punchout-daynite.dnasmarketplace.com/api-docs/)

### Required Body
JSON Content

status: A string value from allowed statuses list for vendors to filter by, case sensitive.

| Status <img width=200/>| Description |
|--|--|
| Pending  | When a PO is received from our ERP, it is in pending status. Vendors cannot see the ending POs until Procurement team forwards the POs to them. |
| Pending Confirmation | When the PO sent to Vendor by Procurement team it becomes Pending Confirmation and vendor can see the PO in web portal |
| Retrieved | Vendor has set the status to retrieved via API |
| Accepted  | Vendor has the option in web portal to Accept the PO. He can also accept by uploading OA. |
| Rejected  | If a vendor rejects the PO the status changes to Rejected. |
| Exported  | When the procurement team sends the OA to the our ERP, PO becomes Exported |


```
{
    "status":"Retrieved"
}
```
### Required Parameters
None

### PHP Curl Example
```
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://api-daynite.dnasmarketplace.com/v1/cart/downloadpolist',
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

### Response Example
```
<PoList>
	<ns1:purchaseOrder DateRequested="2019-10-07" Branch="Y">
		<ns1:PONumber>1234567</ns1:PONumber>
		<ns1:jobnumber />
		<ns1:workordernumber>123456</ns1:workordernumber>
		<ns1:PODescription>Purchase for WO# 123456</ns1:PODescription>
		<ns1:PurchaseOrderType>Purchase</ns1:PurchaseOrderType>
		<ns1:OrderedBy>Marketplace</ns1:OrderedBy>
		<ns1:comment />
		<ns1:AdditionalInfo>
			<ns1:PrcorementPersonnelName> </ns1:PrcorementPersonnelName>
			<ns1:PrcorementPersonnelEmail> </ns1:PrcorementPersonnelEmail>
			<ns1:ShipNoticeId> </ns1:ShipNoticeId>
			<ns1:ShipViaId> </ns1:ShipViaId>
			<ns1:ShipViaDescription> </ns1: ShipViaDescription >
		</ns1: AdditionalInfo >
		<ns1:shipTo country="US">
			<ns1:ShipAddressStreet1>DAY &amp; NITE REFRIGERATION</ns1:ShipAddressStreet1>
			<ns1:ShipAddressStreet2>10 CHARLES STREET</ns1:ShipAddressStreet2>
			<ns1:ShipAddressStreet3 />
			<ns1:ShipAddressStreet4 />
			<ns1:ShipAddressCity>NEW HYDE PARK</ns1:ShipAddressCity>
			<ns1:ShipAddressState>NY</ns1:ShipAddressState>
			<ns1:ShipAddressPostalCode>11040</ns1:ShipAddressPostalCode>
			<ns1:ShipToCode>StockLocation</ns1:ShipToCode>
			<ns1:ShipToBranch />
		</ns1:shipTo>
		<ns1:items>
			<item>
				<ns1:Quantity>2</ns1:Quantity>
				<ns1:UnitOfMeasure>EA</ns1:UnitOfMeasure>
				<ns1:UnitPrice>2.000</ns1:UnitPrice>
				<ns1:BuyerPartNumber>ABCC</ns1:BuyerPartNumber>
				<ns1:SellerPartNumber>ABCC2</ns1:SellerPartNumber>
				<ns1:ItemDescription>1702457</ns1:ItemDescription>
				<ns1:JobId />
				<ns1:WorkOrder />
				<ns1:CostCode />
				<ns1:CostCategory />
				<ns1:BillingItem />
			</item>
			<item>
				<ns1:Quantity>1</ns1:Quantity>
				<ns1:UnitOfMeasure>AE</ns1:UnitOfMeasure>
				<ns1:UnitPrice>1.000</ns1:UnitPrice>
				<ns1:BuyerPartNumber>YYYX4</ns1:BuyerPartNumber>
				<ns1:SellerPartNumber>YYYX4</ns1:SellerPartNumber>
				<ns1:ItemDescription>LAMP-40W 130V CTD</ns1:ItemDescription>
				<ns1:JobId />
				<ns1:WorkOrder />
				<ns1:CostCode />
				<ns1:CostCategory />
				<ns1:BillingItem />
			</item>
		</ns1:items>
	</ns1:purchaseOrder>
	<ns1:purchaseOrder DateRequested="2019-10-07" Branch="Y">
		<ns1:PONumber>1234568</ns1:PONumber>
		<ns1:jobnumber />
		<ns1:workordernumber>123457</ns1:workordernumber>
		<ns1:PODescription>Purchase for WO# 692420</ns1:PODescription>
		<ns1:PurchaseOrderType>Purchase</ns1:PurchaseOrderType>
		<ns1:OrderedBy>Marketplace</ns1:OrderedBy>
		<ns1:comment />
		<ns1:shipTo country="US">
			<ns1:ShipAddressStreet1>DAY &amp; NITE REFRIGERATION</ns1:ShipAddressStreet1>
			<ns1:ShipAddressStreet2>10 CHARLES STREET</ns1:ShipAddressStreet2>
			<ns1:ShipAddressStreet3 />
			<ns1:ShipAddressStreet4 />
			<ns1:ShipAddressCity>NEW HYDE PARK</ns1:ShipAddressCity>
			<ns1:ShipAddressState>NY</ns1:ShipAddressState>
			<ns1:ShipAddressPostalCode>11040</ns1:ShipAddressPostalCode>
			<ns1:ShipToCode>StockLocation</ns1:ShipToCode>
			<ns1:ShipToBranch />
		</ns1:shipTo>
		<ns1:items>
			<item>
				<ns1:Quantity>3</ns1:Quantity>
				<ns1:UnitOfMeasure>UA</ns1:UnitOfMeasure>
				<ns1:UnitPrice>3.000</ns1:UnitPrice>
				<ns1:BuyerPartNumber>AAA2</ns1:BuyerPartNumber>
				<ns1:SellerPartNumber>AAA21</ns1:SellerPartNumber>
				<ns1:ItemDescription>EMP-40W 0V CTD</ns1:ItemDescription>
				<ns1:JobId />
				<ns1:WorkOrder />
				<ns1:CostCode />
				<ns1:CostCategory />
				<ns1:BillingItem />
			</item>
		</ns1:items>
	</ns1:purchaseOrder>
</PoList>

```

