# GET - /search
Endpoint: `https://api.novasearch.xyz/search?query=`

Returns search results in JSON format

## Endpoint Responses
200 - Success

410 - No Results

403 - Forbidden

429 - Too Many Requests

5xx - Server Error

## Example Endpoint Response

Response code: 200
```json
[
  {
    "url": "https://example.com",
    "title": "Example",
    "description": "This is an example description",
    "keywords": "example, website, html",
    "favicon_id": "1234567890ABCDEF"
  },
  {
    "url": "https://example.com",
    "title": "Example",
    "description": "This is an example description",
    "keywords": "example, website, html",
    "favicon_id": "1234567890ABCDEF"
  },
  {
    "url": "https://example.com",
    "title": "Example",
    "description": "This is an example description",
    "keywords": "example, website, html",
    "favicon_id": "1234567890ABCDEF"
  }
]
```

Response code: 410
```json
{"detail":"No results found."}
```

## Try the API Request

You can try the API request by opening this URL in your web browser:

```
https://api.novasearch.xyz/search?query=example
```

Or by using the following cURL command:

```sh
curl -X GET "https://api.novasearch.xyz/search?query=example"
```