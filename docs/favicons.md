# GET - /favicon/{favicon_id}
Endpoint: `https://api.novasearch.xyz/favicon/{favicon_id}`

Returns favicon for a website based on `favicon_id`. To find `favicon_id`, see [GET - /search](/docs/search.md)

# Endpoint Responses
200 - Success

403 - Forbidden

404 - Favicon not found

5xx - Server Error

## Try the API Request

You can try the API request by opening this URL in your web browser:

```
https://api.novasearch.xyz/favicon/07f023d35787e5ed9cbb5f638e490f8b
```

Or by using the following cURL command:

```sh
curl -X GET "https://api.novasearch.xyz/favicon/07f023d35787e5ed9cbb5f638e490f8b"
```