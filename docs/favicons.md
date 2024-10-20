# GET - /favicon/{favicon_id} 
`https://api.novasearch.xyz/favicon/{favicon_id}`

Retrieves a favicon based on its `favicon_id`.

## Usage

This endpoint allows you to retrieve a favicon image. The `{favicon_id}` is a unique identifier obtained from the search results returned by the [`/search`](/docs/search.md) endpoint. Replace `{favicon_id}` in the URL with the actual ID.


## Request Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `favicon_id` | String | Yes | The unique identifier for the favicon (found in search results).  This should be placed directly in the URL path as shown above. |



## Responses

| Status Code | Description |
|---|---|
| 200 OK | Success. The favicon image is returned (typically in ICO, PNG, GIF or SVG format). |
| 400 Bad Request | The request was malformed (e.g., invalid `favicon_id` format). |
| 403 Forbidden | You are not authorized to use this endpoint. This may be due to a network block. Please contact us if you frequently get this error. |
| 404 Not Found | The favicon with the specified `favicon_id` was not found or a `favicon_id` was not specified. |
| 429 Too Many Requests | You have exceeded the rate limit. |
| 5xx Server Error | An error occurred on the server. Please try again later. |


## Rate Limits

This endpoint does not have a ratelimit, please use responsibly.


## API Tester
Example using JavaScript's `fetch` API:

```javascript
const faviconId = '07f023d35787e5ed9cbb5f638e490f8b'; // Replace with the actual favicon_id

fetch(`https://api.novasearch.xyz/favicon/${faviconId}`)
.then(response => {
    if (!response.ok) {
        if (response.status === 404) {
           console.error("Favicon not found.");
        } else {
            console.error(`Error fetching favicon: ${response.status}`);
        }
        return; // Or throw an error as needed
    }
    return response.blob(); // Get the image blob
})
.then(blob => {
    const imageUrl = URL.createObjectURL(blob);
    const imgElement = document.createElement('img'); // Or use an existing img element
    imgElement.src = imageUrl;
    document.body.appendChild(imgElement); // Or append to your desired container
})
.catch(error => console.error('Error:', error));

```

Example using cURL:

```bash
curl -X GET "https://api.novasearch.xyz/favicon/07f023d35787e5ed9cbb5f638e490f8b" -o
```