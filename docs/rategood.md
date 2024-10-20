# POST - /quality/rateresult/good
`https://api.novasearch.xyz/quality/rateresult/good`

Rates a search result as good.  This endpoint helps Nova Search learn which search results are most relevant to users.

## ⚠️ Warning: Likely to change soon

This endpoint's usage is likely to change soon to use search result IDs instead of URLs to help combat search ranking manipulation.

## Usage

This endpoint should be called whenever a user rates a search result returned by the Nova Search API as good.  The `url` parameter should contain the URL of the rated search result.

## Request Body Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `url` | String | Yes | The full URL of the rated search result. |


## Responses

| Status Code | Description |
|---|---|
| 200 OK | Success. The click data was received. |
| 400 Bad Request | The request was malformed (e.g., missing required parameters). |
| 403 Forbidden | You are not authorized to use this endpoint. |
| 429 Too Many Requests | You have exceeded the rate limit.  Your client should fail silently. |
| 5xx Server Error |  An error occurred on the server. Please try again later. |


## Rate Limits

This endpoint, along with all other Search Quality endpoints, has a combined rate limit of **5 requests per minute**. Your client should not throw an error, but instead fail silently if a 429 error is returned.

## API Tester
Example using JavaScript's `fetch` API:

```javascript
fetch('https://api.novasearch.xyz/quality/rateresult/good', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    url: 'https://example.com/rated-result'
  })
})
.then(response => {
  if (!response.ok) {
    // Handle error (e.g., 429 Too Many Requests) silently
    console.warn('Page click request failed:', response.status);
    return;
  }
  console.log('Page click registered successfully');
})
.catch(error => {
  console.error('Error sending page click request:', error);
});

```



Example using cURL:

```bash
curl -X POST "https://api.novasearch.xyz/quality/rateresult/good" \
-H "Content-Type: application/json" \
-d '{
  "url": "https://example.com/rated-result"
}'
```