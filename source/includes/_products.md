# Products

## Get Products

<aside class="warning">
Please use v2 for any new implementation
</aside>

```shell
curl "https://api.transitinc.com/v1/products?products=8-56140,LOP-LP5"
  -H "Authorization: Basic YourAuthTokenBase64"
```

> The above command returns JSON structured like this:

```json
{
  "products": [
    {
      "product": "8-56140",
      "name": "(5580) ROTOR (TOP QUALITY)",
      "price": 9.57,
      "prices": [],
      "available": 71
    },
    {
      "product": "LOP-LP5",
      "name": "OIL FILTER (LOOP)",
      "price": 3.57,
      "prices": [
        { "qty": 10, "price": 3.25 }
      ],
      "available": 12
    }
  ]
}
```

This endpoint retrieves a list of products.

### HTTP Request

`GET https://api.transitinc.com/v1/products`

### Query Parameters

Parameter | Required | Description
--------- | -------- | -----------
products | yes | Comma separated list of Transit part numbers

<aside class="notice">
  Remember — The request must be authenticated.
</aside>

<aside class="notice">
  <a href="/v1/products?products=8-56140,LOP-LP5">Try now in your browser</a>
</aside>

### Error codes

See the [Errors](#errors) section to know how to read error codes.

Error Code | Message
---------- | -------
4001 | At least one product number is required.

## Get Products V2

```shell
curl "https://api.transitinc.com/v2/products?whse=001&products=8-56140,LOP-LP5,PPC-D741&ignoreProductError=true"
  -H "Authorization: Basic YourAuthTokenBase64"
```

> The above command returns JSON structured like this:

```json
{
    "products": [
        {
            "product": "8-56140",
            "name": "ROTOR (TOP QUALITY)",
            "weight": 5.30000,
            "price": 12.64,
            "unit": "each",
            "altPrice": 12.64,
            "altUnit": "each",
            "prices": [],
            "available": 74
        },
        {
            "product": "18-ATO10",
            "name": "STD BLADE FUSES 10 AMPS (TOP QUALITY)",
            "weight": 0.0200,
            "price": 0.60,
            "unit": "P10",
            "altPrice": 0.06,
            "altUnit": "Un",
            "prices": [],
            "available": 88
        },
        {
            "product": "AQL-47101",
            "name": "AQUAPEL GLASS TREATMENT (AQUAPEL)",
            "weight": 0.10400,
            "price": 6.95,
            "unit": "each",
            "altPrice": 6.95,
            "altUnit": "each",
            "prices": [
                {
                    "qty": 6,
                    "price": 6.59,
                    "altPrice": 6.59
                },
                {
                    "qty": 24,
                    "price": 6.19,
                    "altPrice": 6.19
                },
                {
                    "qty": 120,
                    "price": 5.89,
                    "altPrice": 5.89
                }
            ],
            "available": 494
        }
    ],
    "errors": {
        "code": 2011,
        "message": "Product PPC-D741 not found in Warehouse 001.",
        "errors": []
    }
}
```

This endpoint retrieves a list of products.

### HTTP Request

`GET https://api.transitinc.com/v2/products`

### Query Parameters

Parameter | Required | Description
--------- | -------- | -----------
products | yes | Comma separated list of Transit part numbers
whse | no | Transit warehouse to get results from
ignoreProductError | no | true / false - When true products will be returned even if an error is encountered. Defaults to false.

<aside class="notice">
  Remember — The request must be authenticated.
</aside>

<aside class="notice">
  <a href="/v2/products?whse=001&products=8-56140,LOP-LP5">Try now in your browser</a>
</aside>

### Error codes

See the [Errors](#errors) section to know how to read error codes.

Error Code | Message
---------- | -------
2003 | Product XXX is invalid.
2011 | Product XXX not found in Warehouse XXX.
4001 | At least one product number is required.
6001 | Invalid warehouse, or access not allowed for this warehouse.
