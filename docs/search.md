# GET - /search 
`https://api.novasearch.xyz/search`

Performs a search and returns results in JSON format.

## ⚠️ Warning: Likely to change soon

This endpoint's usage is likely to change soon to include proper pagination and to return IDs for search results, which will increase performance client-side and decrease the time taken to load results along with allowing /quality endpoints to be used easier.

## Usage

This endpoint allows you to query the Nova Search index.  The required `query` parameter specifies the search terms.  Append this parameter to the base URL like so: `/search?query=your+search+terms`.

## Request Parameters


| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | String | Yes | The search terms. |


## Responses

| Status Code | Description | Response Body Example |
|---|---|---|
| 200 OK | Success. The search results are returned. |  ```[ { "url": "https://example.com", "title": "Example", "description": "This is an example description", "keywords": "example, website, html", "favicon_id": "1234567890ABCDEF" }, ... ] ``` |
| 400 Bad Request | The request was malformed |  N/A |
| 403 Forbidden | You are not authorized to use this endpoint. This may be due to a network block. Please contact us if you frequently get this error. | N/A |
| 410 Gone | No results were found for the given query. | ```{"detail":"No results found."} ``` |
| 422 Unprocessable Entity | The query parameter is missing or empty. | ```{"detail":[{"type":"missing","loc":["query","query"],"msg":"Field required","input":null}]} ``` |
| 429 Too Many Requests | You have exceeded the rate limit. | N/A |
| 5xx Server Error | An error occurred on the server. Please try again later. | N/A |


## Response Body (200 OK)

The successful response (200 OK) returns a JSON array of search result objects.  Each object has the following properties:

| Property | Type | Description |
|---|---|---|
| `url` | String | The URL of the search result. |
| `title` | String | The title of the search result. |
| `description` | String | A brief description of the search result. |
| `keywords` | String | Keywords associated with the search result. |
| `favicon_id` | String | A unique identifier for the favicon of the website. (This may be used with a separate favicon retrieval endpoint if needed.) |
| `last_crawled` | String | Timestamp for the last time the URL shown in the search result was crawled by us. |


## Rate Limits

This endpoint has a rate limit of **15 requests per minute**.

## API Tester
Example using JavaScript's `fetch` API:

```javascript
const query = 'example';  // Replace with user's search query
fetch(`https://api.novasearch.xyz/search?query=${query}`)
.then(response => {
    if (!response.ok) {
        // Check for specific error codes (e.g., 410)
        if (response.status === 410) {
            console.log("No results found.");
        } else {
            console.error("Search request failed:", response.status);
        }
        return; // Or throw an error for more structured error handling
    }
    return response.json(); // Parse JSON response
})
.then(data => {
    console.log("Search results:", data);
    // Process the search results
})
.catch(error => {
    console.error("Error fetching search results:", error);
});

```


Example using cURL:

```bash
curl -X GET "https://api.novasearch.xyz/search?query=example"
```