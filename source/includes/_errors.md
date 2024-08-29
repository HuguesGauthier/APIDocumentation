# Errors

> Single error code returned:

```json
{
    "code": 1234,
    "message": "This is a detailed error message."
}
```

> More than one error code returned:

```json
{
    "code": 1234,
    "message": "This is a detailed error message.",
    "errors": [
        { "code": 2222, "message": "This is a detailed error message 1." },
        { "code": 3333, "message": "This is a detailed error message 2." },
    ]
}
```

For every API endpoint, if an invalid or empty auth token is supplied, the response HTTP code is `401`.

For any other error, the response HTTP code is `500` instead of `200`.

Additionnaly, a JSON object is returned with a detailed error code and message. If more than one error is encountered in the same request, an additionnal `errors` JSON array is returned.

### New in V2 routes
The error response always returns an "errors" array. It is empty if there is a single error.

An error response will have HTTP code `400` (Bad Request).
