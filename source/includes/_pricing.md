# Pricing

## Get Pricing

<aside class="notice">
Get Pricing v2 not released yet
</aside>

```shell
curl "https://api.transitinc.com/v1/pricing?warehouse=001&type=FULL&format=JSON"
  -H "Authorization: Basic YourAuthTokenBase64"
```

> The above command returns JSON structured like this:

```json
{
  "version": "Full-201902130145",
  "pricing": [
    ["K8T-102429","EACH","Transit Auto","827098402437",104.12],
    ["K8T-102430","EACH","Transit Auto","827098402444",104.05]
  ]
}
```

This endpoint retrieves the pricing for a specific Transit warehouse, all products.

### HTTP Request

`GET https://api.transitinc.com/v1/pricing`

### Query Parameters

Parameter | Required | Description
--------- | -------- | -----------
warehouse | yes | Transit warehouse code. Example: 001 is Levis Warehouse.
type | yes | FULL: for the full list of products refreshed each week.
format | yes | JSON for json output. CSV for csv output.

### Result Column

ColumnName | Description
--------- | -----------
ProductKey | Transit warehouse product name
UnitStock | The stocking unit is the basis for all quantity transactions
WebBrandName | Web brand name
UPC | UPC
Price | Price

### Error codes

See the [Errors](#errors) section to know how to read error codes.

Error Code | Message
---------- | -------
6001 | Invalid warehouse, or access not allowed for this warehouse.
6002 | Invalid type.
6003 | Invalid format.
6004 | Information not available at this time.
