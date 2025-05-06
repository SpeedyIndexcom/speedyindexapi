# SpeedyIndex API v2 Documentation

## Introduction

Welcome to the SpeedyIndex API v2. Our service is designed to provide a robust and efficient solution for **accelerated content discovery** by major search engines like Google and Yandex. Whether you need to get new pages indexed quickly, re-index updated content, or perform a **bulk URL index check**, our API offers the tools for seamless integration into your workflows.

SpeedyIndex helps you manage your website's presence in search results programmatically. Utilize our API for **forced indexing tool** capabilities, ensuring your fresh content doesn't wait long to be seen. This documentation provides all the necessary details to interact with our endpoints, manage tasks, and monitor your link indexation status effectively. We support **Yandex index submission API** functionalities alongside Google.

Key benefits of using the SpeedyIndex API:

*   **Rapid Indexing:** Submit URLs for quick processing by Google and Yandex.
*   **Indexation Checks:** Verify the index status of your URLs.
*   **Task Management:** Create, list, and monitor indexing and checking tasks.
*   **Detailed Reporting:** Get comprehensive reports on task progress and outcomes.
*   **Scalability:** From single link submissions to bulk operations for up to 10,000 URLs per request.
*   **Automation:** Perfect for those looking to **automate website re-indexing** processes.

Your API Key must be included in the `Authorization` header for all requests.

---

## Check Balance

To get your current account balance for different services.

*   **Method:** `GET`
*   **Endpoint:** `/v2/account`

**Headers:**
*   `Authorization: <API KEY>` - Your unique API key.

**Response Fields:**
*   `code` (integer): Status code of the response. 0 indicates success.
*   `balance` (object): Contains balance details.
    *   `balance.indexer` (integer): Your balance for Google link indexing service.
    *   `balance.checker` (integer): Your balance for Google link indexation check service.

**Request Example (curl):**
```bash
curl -H "Authorization: <API KEY>" https://api.speedyindex.com/v2/account

{
    "code": 0,
    "balance": {
        "indexer": 10014495,
        "checker": 100732
    }
}

curl -X POST -H 'Authorization: <API KEY>' \
-H 'Content-Type: application/json' \
-d '{"title":"test title","urls":["https://google.com","https://google.ru"]}' \
https://api.speedyindex.com/v2/task/google/indexer/create

{
    "code": 0,
    "task_id": "6609d023a3188540f09fec6c",
    "type": "google/indexer"
}

curl -H "Authorization: <API KEY>" https://api.speedyindex.com/v2/task/google/checker/list/0

{
    "code": 0,
    "page": 0,
    "last_page": 0,
    "result": [
        {
            "id": "65f8c7315752853b9171860a",
            "size": 690,
            "processed_count": 690,
            "indexed_count": 279,
            "title": "index_.txt",
            "type": "google/checker",
            "created_at": "2024-03-18T22:58:56.901Z"
        }
    ]
}

