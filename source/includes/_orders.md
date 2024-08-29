# Orders

## Submit Order

<aside class="warning">
Please use v2 for any new implementation
</aside>

```shell
curl "https://api.transitinc.com/v1/orders"
  -X POST
  -H "Authorization: Basic YourAuthTokenBase64"
  -H "Content-Type: application/json"
  -d '{
    "purchaseOrder": "123456",
    "isPickup": false,
    "shipTo": {
      "LanguageNo": "EN",
      "Name": "John Doe",
      "Phone": "(514) 432-4323",
      "Email": "johndoe@hotmail.com",
      "AddressLine1": "123, Fake street",
      "AddressLine2": null,
      "City": "Montreal",
      "State": "QC",
      "Zip": "D6G 9J4",
      "Country": "CA",
      "Note": "LAISSER SUR PLACE SI PERSONNE"
    },
    "details": [
        { "product": "8-56140", "qty": 2 },
        { "product": "LOP-LP5", "qty": 1 }
    ]
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint submits a new order to Transit.

### HTTP Request

`POST https://api.transitinc.com/v1/orders`

### Query Parameters

Parameter | Required | Description
--------- | -------- | -----------
purchaseOrder | yes | Unique alphanumeric order number, will be set as the PO on the Transit Invoice for this order. Max 10 characters.
isPickup | yes | false if you want Transit to ship the order. true for a customer pickup at Transit Warehouse.
shippingService | no | For shipped orders, the desired shipping service.
shipTo | no | Don't specify the shipTo object for pickup orders or if you want to keep the default shipto configured in the linked Transit Customer Zone account.
shipTo.LanguageNo | yes | Packing Slip Language. Must be EN, or FR.
shipTo.Name | yes | Ship to name, on carrier label, packing slip
shipTo.Phone | yes |	Ship to phone, for carrier
shipTo.Email | no	| Ship to email, for carrier
shipTo.AddressLine1 | yes |	Ship to address line 1
shipTo.AddressLine2 | no | Ship to address line 2
shipTo.City | yes | Ship to city
shipTo.State | yes	|	Ship to state (2 char)
shipTo.Zip | yes	|	Ship to zip/postal code
shipTo.Country | yes	|	Ship to country must be CA or US.
shipTo.Note | yes |	Ship to note (for carrier/customer) max 100 caracters.
details.product | yes	|	Transit part number
details.qty | yes	| Order Qty

### Error codes

See the [Errors](#errors) section to know how to read error codes.

Error Code | Message
---------- | -------
2000 | Order not created because the request contains error(s).
2001 | purchaseOrder must be unique.
2002 | shipTo LanguageNo must be EN or FR.
2003 | product XXX is invalid.
2004 | product XXX qty XXX is not available.
2005 | product XXX qty XXX must be greater than 0.
2006 | purchaseOrder must be alphanumeric only.
2007 | purchaseOrder must be less than 11 characters.
2008 | product XXX Qty XXX must be a factor of XXX.
2009 | shipTo State must be 2 letters.
2010 | shipTo Country must be CA or US.
2101 | purchaseOrder is required.
2102 | shipTo LanguageNo is required.
2103 | shipTo Name is required.
2104 | shipTo Phone is required.
2105 | shipTo AddressLine1 is required.
2106 | shipTo City is required.
2107 | shipTo State is required.
2108 | shipTo Zip is required.
2109 | shipToCountry is required.
2110 | A product is required.
2112 | shipTo address is invalid.

## Submit Order V2

```shell
curl "https://api.transitinc.com/v2/orders"
  -X POST
  -H "Authorization: Basic YourAuthTokenBase64"
  -H "Content-Type: application/json"
  -d '{
	"whse": "001",
	"whsePickup": "001",
	"purchaseOrder": "123456",
	"shippingService": "UPSGround",
	"transitNote": "transit note",
	"documentNote": "document note",
	"shipTo": {
		"languageNo": "EN",
		"name": "John Doe",
		"phone": "(514) 432-4323",
		"email": "johndoe@hotmail.com",
		"addressLine1": "123, Fake street",
		"addressLine2": null,
		"addressLine3": null,
		"city": "Montreal",
		"state": "QC",
		"zip": "D6G 9J4",
		"country": "CA",
		"note": "LAISSER SUR PLACE SI PERSONNE"
	},
	"details": [
		{
			"product": "8-56140",
			"crossReference": "ref#"
			"qty": 2,
			"keepBo": true,
			"declaredValue": 9.99
		},
		{
			"product": "LOP-LP5",
			"crossReference": "ref#"
			"qty": 1,
			"keepBo": true,
			"declaredValue": 9.99
		}
	]
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "warnings": []
}
```

This endpoint submits a new order to Transit.

### HTTP Request

`POST https://api.transitinc.com/v2/orders`

### HTTP Response
`Status code: 201`  
`Location header: /v1/orders/purchase-order`

### Query Parameters

Parameter | Required | Description
--------- | -------- | -----------
whse | no |  Warehouse at which you wish to submit your order, will default to your default warehouse.
whsePickup | no | For pickup orders, Warehouse at which you wish to pickup your order. If not set, the order will be shipped using *shippingService* or the default shipping method registered to your account.
purchaseOrder | yes | Unique alphanumeric order number, will be set as the PO on the Transit Invoice for this order.
shippingService | no | For shipped orders, the desired shipping service. **If set, prevails over whsePickup, making the order a shipped order.**
transitNote | no | Transit **will** take note of this. This note will not be printed on any document. The nature of this note may cause delays.
documentNote | no | Transit **will not** take note of this. This note will be printed on the documents related to this order.
shipTo | no | Don't specify the shipTo object for pickup orders or if you want to keep the default shipto configured in the linked Transit Customer Zone account.
shipTo.languageNo | no | Language used for notifications. Defaults to token's language no.
shipTo.name | yes | Ship to name, on carrier label
shipTo.phone | yes | Ship to phone, for carrier
shipTo.email | no	| Ship to email, for carrier
shipTo.addressLine1 | yes | Ship to address line 1
shipTo.addressLine2 | no | Ship to address line 2
shipTo.addressLine3 | no | Ship to address line 3
shipTo.city | yes | Ship to city
shipTo.state | yes | Ship to state
shipTo.zip | yes | Ship to zip/postal code
shipTo.country | yes | Ship to country.
shipTo.note | yes | Ship to note (for carrier/customer).
details | yes | List of products you wish to order.
details.product | yes | Transit part number
details.qty | yes | Order Qty (unit is used, no altUnit are supported)
details.crossReference | no | Your reference number for the product.
details.keepBo | no | Keep back order if there is not enough stock to fullfill your order.
details.declaredValue | no | Declared valued of the product. Required for international orders.

### Error codes

See the [Errors](#errors) section to know how to read error codes.

Error Code | Message
---------- | -------
2000 | Order not created because the request contains error(s).
2001 | Purchase Order must be unique.
2002 | Ship To LanguageNo must be EN or FR.
2003 | product XXX is invalid.
2005 | Quantity must be greater than zero for product XXX.
2006 | Purchase Order's characters allowed are alphanumeric, dash and underscore.
2007 | Purchase Order must not exceed 22 characters..
2010 | Ship To Country Code must be CA or US.
2011 | Product XXX not found in Warehouse XXX.
2018 | Back Order is not allowed for XXX, this product will be discontinued.
2019 | Invalid pickup warehouse.
2020 | Shipping Service must not exceed 100 characters.
2021 | Invalid Shipping Service.
2023 | Oups! Qty XX exceeds our availability of XX for product XXX.
2024 | Declared value must be greater than zero. (Product XXX)
2101 | purchaseOrder is required.
2103 | Ship To Name is required.
2104 | Ship To Phone is required.
2105 | Ship To Address Line 1 is required.
2106 | Ship To City is required.
2107 | Ship To State is required.
2108 | Ship To Zip is required.
2109 | Ship To Country Code is required.
2110 | A product is required.
2113 | Ship To Name must not exceed 30 characters.
2114 | Concatenated Ship To Address Lines must not exceed 90 characters.
2115 | ShipTo City must not exceed 20 characters.
2116 | Ship To State Code must not exceed 2 characters.
2117 | Ship To Zip must not exceed 10 characters.
2119 | Ship To Phone must not exceed 20 characters.
2120 | Ship To Email must not exceed 60 characters.
2121 | Note must not exceed 30 characters.
2122 | Document Note must not exceed 960 characters.
2125 | Transit Note must not exceed 960 characters.
2126 | Cross reference must not exceed 24 characters for product XXX.
2128 | Invalid state for Country XX.
2129 | Declared value is required for international sales. (Product XXX)
6001 | Invalid warehouse, or access not allowed for this warehouse.

### Warnings
Product XXX, XX units ordered, XX units kept BO.

## Get Order

<aside class="notice">
Get Order v2 not released yet
</aside>

```shell
curl "https://api.transitinc.com/v1/orders/123456"
  -H "Authorization: Basic YourAuthTokenBase64"
```

> The above command returns JSON structured like this:

```json
{
   "purchaseOrder": "123456",
   "status": "Shipped",
   "carrier": "Nationex", 
   "carrierService": null,
   "carrierTrackingNo": "123456789",
   "shipToName": "John Doe",
   "shipToPhone": "(514) 432-4323",
   "shipToEmail": "johndoe@hotmail.com",
   "shipToAddressLine1": "123, Fake street",
   "shipToAddressLine2": null,
   "shipToCity": "Montreal",
   "shipToState": "QC",
   "shipToZip": "D6G 9J4",
   "shipToCountry": "CA",
   "details": [
        { "product": "8-56140", "orderQty": 2, "shipQty": 2 },
        { "product": "LOP-LP5", "orderQty": 1, "shipQty": 0 }
    ]
}
```

This endpoint retrieves an order.

### HTTP Request

`GET https://api.transitinc.com/v1/orders/<purchaseOrder>`

### Query Parameters

Parameter | Required | Description
--------- | -------- | -----------
purchaseOrder | yes | Supplied purchaseOrder when the order was submitted.

### Error codes

See the [Errors](#errors) section to know how to read error codes.

Error Code | Message
---------- | -------
5001 | Order not found.
5002 | Order details not found.
