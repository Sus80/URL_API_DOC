# API RefBucket

Created by: Susan 
Created time: May 7, 2025 7:44 PM
Category: API Docs
Last edited by: Susan 
Last updated time: May 7, 2025 9:28 PM

## Description

This API allows users to capture and categorize URLs from a Chrome extension, saving them into specific categories like Article, Video, and more.

## **Base URL**

The base URL for all API requests is:

`https://sheets.googleapis.com`

## Endpoints

**Description**: Returns the values from a specified range in your Google Sheet.
GET /spreadsheets/1q40f6djrhHSStT9FhT6ODuQ0WuaOG3fwrpzd99huXOQ/values/Sheet1!A1:D10

### Parameters

- `range` (required): The range of cells to fetch, e.g., `Sheet1!A1:D10`.
- `majorDimension` (optional): Specifies the dimension of the data (ROWS or COLUMNS). Default is `ROWS`.
- `category` (required): The category to filter URLs by (e.g., Article, Website, Video, Report, Blog)

### **Response**

Returns a JSON object with the following properties:

- `count`: The total number of URLs saved.
- `metrics`: An object containing the following metrics:
    - `total_urls_saved`: Total URLs saved in the sheet.
    - `average_urls_per_day`: Average number of URLs saved per day.
    - `citation_ready_count`: Number of URLs that are citation-ready.
    - `estimated_saved_time`: Estimated time saved by using the extension.
- `results`: An array of URL objects, each with the following properties:
    - `id`: The unique identifier of the URL entry.
    - `category`: The category of the URL (e.g., Article, Website).
    - `url`: The actual URL saved.
    - `timestamp`: The date and time the URL was saved.
    - `user_id`: The ID of the user who saved the URL.

### Example

Request:

```
GET /spreadsheets/1q40f6djrhHSStT9FhT6ODuQ0WuaOG3fwrpzd99huXOQ/values/Sheet1!A1:D10
```

Response:

```json
{
  "count": 100,
  "metrics": {
    "total_urls_saved": 100,
    "average_urls_per_day": 5,
    "citation_ready_count": 85,
    "estimated_saved_time": "2 hours"
  },
  "results": [
    {
      "id": 1,
      "category": "Article",
      "url": "https://example.com/article1",
      "timestamp": "2025-05-07T12:00:00Z",
      "user_id": "User123"
    },
    {
      "id": 2,
      "category": "Video",
      "url": "https://example.com/video1",
      "timestamp": "2025-05-07T13:00:00Z",
      "user_id": "User456"
    },
    ...
  ]

```

### **Errors**

This API uses the following error codes:

- **`400 Bad Request`**: The request was malformed or missing required parameters.
- **`401 Unauthorized`**: The API key was invalid or missing.
- **`404 Not Found`**: The specified sheet or range does not exist.
- **`500 Internal Server Error`**: An unexpected error occurred on the server.
