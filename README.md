


# SpeedyIndex API v2 Documentation

**Quick Links:**
*   [Links Indexing](https://en.speedyindex.com)
*   [Reindex Website](https://en.speedyindex.com/reindex-website/)
*   [Index Checker](https://en.speedyindex.com/google-index-checker/)
*   [Free Sitemap Extractor](https://en.speedyindex.com/free-xml-sitemap-url-extractor/)

## Introduction

Welcome to the SpeedyIndex API v2. Our service is engineered to provide a powerful and streamlined solution for **accelerated content discovery** by major search engines, including Google and Yandex. Whether you need to **get new pages indexed quickly**, re-index updated content after a site migration, or perform a **bulk URL index check** for large websites, our API offers the tools for seamless integration into your existing SEO workflows and scripts. SpeedyIndex is your go-to platform if you're looking for a reliable **alternative to Google Indexing API** that supports a wider range of URLs without the strict limitations.

SpeedyIndex empowers you to programmatically manage your website's presence in search results. Utilize our API for **forced indexing tool** capabilities, ensuring your fresh articles, product pages, or critical updates don't languish unseen. This comprehensive documentation provides all necessary details to interact with our endpoints, manage link submission tasks, and effectively monitor your **link indexation status for Google**. We also provide robust support for **Yandex index submission API** functionalities, making it a versatile tool for international SEO. If you've ever wondered **how to check if a site is indexed by Google programmatically** or need a **fast way to get URLs indexed**, SpeedyIndex API is the answer.

Key benefits of using the SpeedyIndex API:

*   **Rapid Indexing:** Submit URLs for quick processing by Google and Yandex.
*   **Indexation Checks:** Verify the index status of your URLs.
*   **Task Management:** Create, list, and monitor indexing and checking tasks.
*   **Detailed Reporting:** Get comprehensive reports on task progress and outcomes.
*   **Scalability:** From single link submissions to bulk operations for up to 10,000 URLs per request.
*   **Automation:** Perfect for those looking to **automate website re-indexing** processes.

Your API Key must be included in the `Authorization` header for all requests.

---

## Table of Contents

1.  [Check Balance](#check-balance)
2.  [Task Creation](#task-creation)
3.  [Getting the list of tasks](#getting-the-list-of-tasks)
4.  [Getting the status of tasks](#getting-the-status-of-tasks)
5.  [Downloading a task report](#downloading-a-task-report)
6.  [Index a single link](#index-a-single-link)
7.  [Create an invoice for payment](#create-an-invoice-for-payment)
8.  [VIP Queue (google/indexer only)](#vip-queue-googleindexer-only)
9.  [Pricing](#pricing)

---

## 1. Check Balance

To get your current account balance for different services.

*   **Method:** `GET`
*   **Endpoint:** `https://api.speedyindex.com/v2/account`

**Headers:**
*   `Authorization: <API KEY>` - Your unique API key.

**Response Fields:**
*   `code` (integer): Status code of the response. `0` indicates success.
*   `balance` (object): Contains balance details.
    *   `balance.indexer` (integer): Your balance for Google link indexing service.
    *   `balance.checker` (integer): Your balance for Google link indexation check service.

**Request Example (curl):**
```bash
curl -H "Authorization: <API KEY>" https://api.speedyindex.com/v2/account
```

**Response Example (JSON):**
```json
{
    "code": 0,
    "balance": {
        "indexer": 10014495,
        "checker": 100732
    }
}
```

---

## 2. Task Creation

Create a new task for link indexing or index checking. This is a core feature for programmatic Google indexing.

*   **Method:** `POST`
*   **Endpoint:** `https://api.speedyindex.com/v2/task/<SEARCH ENGINE>/<TASK TYPE>/create`

**Path Parameters:**
*   `<SEARCH ENGINE>` (string): The search engine. Possible values: `google`, `yandex`.
*   `<TASK TYPE>` (string): The type of task. Possible values: `indexer` (for link indexing), `checker` (for checking indexation of links).

**Headers:**
*   `Authorization: <API KEY>` - Your unique API key.
*   `Content-Type: application/json`

**Request Body (JSON):**
*   `title` (string, optional): A name for your task.
*   `urls` (array of strings): Links you want to add to the task. **No more than 10,000 links** in a single request.

**Response Codes & Fields:**
*   `code` (number):
    *   `0`: Links successfully added.
    *   `1`: Top up balance.
    *   `-2`: The server is overloaded. Repeat the request later.
*   `task_id` (string): Identifier of the created task (if `code: 0`).
*   `type` (string): Task type (e.g., `google/indexer`).

**Request Example (curl):**
```bash
curl -X POST -H 'Authorization: <API KEY>' \
-H 'Content-Type: application/json' \
-d '{"title":"test title","urls":["https://google.com","https://google.ru"]}' \
https://api.speedyindex.com/v2/task/google/indexer/create
```

**Response Example (JSON):**
```json
{
    "code": 0,
    "task_id": "6609d023a3188540f09fec6c",
    "type": "google/indexer"
}
```

---

## 3. Getting the list of tasks

Retrieve a paginated list of your tasks.

*   **Method:** `GET`
*   **Endpoint:** `https://api.speedyindex.com/v2/task/<SEARCH ENGINE>/<TASK TYPE>/list/<PAGE>`

**Path Parameters:**
*   `<SEARCH ENGINE>` (string): Possible values: `google`, `yandex`.
*   `<TASK TYPE>` (string): Possible values: `indexer`, `checker`.
*   `<PAGE>` (number): Page number. Each page contains 1000 tasks. Numbering starts from `0`. The task list is sorted from new to old.

**Headers:**
*   `Authorization: <API KEY>`

**Response Fields:**
*   `code` (number): Status code.
*   `page` (number): Current page number.
*   `last_page` (number): Last page number.
*   `result` (array of objects): List of tasks. Each task object contains:
    *   `id` (string): Task identifier.
    *   `size` (number): Total number of links in the task.
    *   `processed_count` (number): Number of processed links.
    *   `indexed_count` (number): Number of indexed links.
    *   `type` (string): Task type.
    *   `title` (string): Task title.
    *   `is_completed` (boolean): `true` if the task is completed and the final report is available.
    *   `created_at` (string): Task creation date (ISO 8601 format).

**Request Example (curl):**
```bash
curl -H "Authorization: <API KEY>" https://api.speedyindex.com/v2/task/google/checker/list/0
```

**Response Example (JSON):**
```json
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
```

---

## 4. Getting the status of tasks

Check the status of one or more tasks.

*   **Method:** `POST`
*   **Endpoint:** `https://api.speedyindex.com/v2/task/<SEARCH ENGINE>/<TASK TYPE>/status`

**Path Parameters:**
*   `<SEARCH ENGINE>` (string): Possible values: `google`, `yandex`.
*   `<TASK TYPE>` (string): Possible values: `indexer`, `checker`.

**Headers:**
*   `Authorization: <API KEY>`
*   `Content-Type: application/json`

**Request Body (JSON):**
*   `task_ids` (array of strings): List of task IDs. Limit: no more than **1000** elements.

**Response Fields:**
Same structure as the "List Tasks" response, containing details for the requested task IDs.

**Request Example (curl):**
```bash
curl -X POST -H "Authorization: <API KEY>" \
-H "Content-Type: application/json" \
-d '{"task_ids":["65f8c7305759855b9171860a"]}' \
https://api.speedyindex.com/v2/task/google/indexer/status
```

**Response Example (JSON):**
```json
{
    "code": 0,
    "result": [
        {
            "id": "65f8c7305759855b9171860a",
            "size": 690,
            "processed_count": 690,
            "indexed_count": 279,
            "is_completed": false,
            "title": "index_.txt",
            "type": "google/indexer",
            "created_at": "2024-03-18T22:58:56.901Z"
        }
    ]
}
```

---

## 5. Downloading a task report

Download the full report for a completed task, including lists of indexed and unindexed links.

*   **Method:** `POST`
*   **Endpoint:** `https://api.speedyindex.com/v2/task/<SEARCH ENGINE>/<TASK TYPE>/fullreport`

**Path Parameters:**
*   `<SEARCH ENGINE>` (string): Possible values: `google`, `yandex`.
*   `<TASK TYPE>` (string): Possible values: `indexer`, `checker`.

**Headers:**
*   `Authorization: <API KEY>`
*   `Content-Type: application/json`

**Request Body (JSON):**
*   `task_id` (string): The ID of the task for which to download the report.

**Response Fields:**
*   `code` (number): Status code.
*   `result` (object): Report details.
    *   `id` (string): Task identifier.
    *   `size` (number): Total links in the task.
    *   `processed_count` (number): Processed links.
    *   `indexed_links` (array of objects): List of indexed links. Each object:
        *   `url` (string): Page URL.
        *   `title` (string): Title from search results (**only available for google**).
    *   `unindexed_links` (array of objects): List of unindexed links. Each object:
        *   `url` (string): Page URL.
        *   `error_code` (number): Error codes (**only available for google/indexer tasks**):
            *   `-1`: Meta tag noindex found.
            *   `0`: No errors found.
            *   `404, 502, 410, etc.`: HTTP status code found on the page.
    *   `title` (string): Task title.
    *   `type` (string): Task type.
    *   `created_at` (string): Task creation date.

**Request Example (curl):**
```bash
curl -X POST -H "Authorization: <API KEY>" \
-H "Content-Type: application/json" \
-d '{"task_id":"67f542b1e86b8c3b8ffac1a6"}' \
https://api.speedyindex.com/v2/task/google/indexer/fullreport
```

**Response Example (JSON):**
```json
{
    "code": 0,
    "result": {
        "id": "67f542b1e86b8c3b8ffac1a6",
        "size": 1,
        "processed_count": 1,
        "indexed_links": [
            {
                "url": "https://google.com",
                "title": "Google"
            }
        ],
        "unindexed_links": [],
        "title": "msg-2025-04-08T15:37:22.838Z.txt",
        "type": "google/indexer",
        "created_at": "2025-04-08T15:37:28.013Z"
    }
}
```

---

## 6. Index a single link

Quickly submit a single URL for indexing.

*   **Method:** `POST`
*   **Endpoint:** `https://api.speedyindex.com/v2/<SEARCH ENGINE>/url`

**Path Parameters:**
*   `<SEARCH ENGINE>` (string): Possible values: `google`, `yandex`.

**Headers:**
*   `Authorization: <API KEY>`
*   `Content-Type: application/json`

**Request Body (JSON):**
*   `url` (string): The link you want to index.

**Response Codes:**
*   `code` (number):
    *   `0`: Link successfully added.
    *   `1`: Top up balance.
    *   `-2`: The server is overloaded. Repeat the request later.

**Request Example (curl):**
```bash
curl -X POST -H 'Authorization: <API KEY>' \
-H 'Content-Type: application/json' \
-d '{"url":"https://google.ru"}' \
https://api.speedyindex.com/v2/google/url
```

**Response Example (JSON):**
```json
{"code":0}
```

---

## 7. Create an invoice for payment

Generate an invoice link to top up your account balance.

*   **Method:** `POST`
*   **Endpoint:** `https://api.speedyindex.com/v2/account/invoice/create`

**Headers:**
*   `Authorization: <API KEY>`
*   `Content-Type: application/json`

**Request Body (JSON):**
*   `qty` (number): Number of links to which you need to top up your balance.
*   `type` (string): Service type. Possible values: `indexer`, `checker`, `mix`.
*   `method` (string): Payment method. Possible values: `crypto`, `paypal`, `yookassa`.
*   `email` (string, optional): Required for `Yookassa` only.

**Response Fields:**
*   `code` (number): Status code (`0` for success).
*   `result` (string): Invoice link for payment.

**Request Example (curl):**
```bash
curl -X POST -H "Authorization: <API KEY>" \
-H 'Content-Type: application/json' \
-d '{"qty":10000,"method":"crypto","type":"indexer"}' \
https://api.speedyindex.com/v2/account/invoice/create
```

**Response Example (JSON):**
```json
{
    "code": 0,
    "result": "https://pay.cryptocloud.plus/LJQ18AI1?lang=en"
}
```

---

## 8. VIP Queue (google/indexer only)

Add a task to the VIP queue for expedited Google indexing. This is a paid service where 1 link equals 1 additional credit.

**Note:** This is a paid service (1 link = 1 additional credit). Googlebot typically follows links within 1-10 minutes after activation. Task completion is guaranteed within 5 minutes; otherwise, funds are returned to your balance.

*   **Method:** `POST`
*   **Endpoint:** `https://api.speedyindex.com/v2/task/google/indexer/vip`

**Headers:**
*   `Authorization: <API KEY>`
*   `Content-Type: application/json`

**Request Body (JSON):**
*   `task_id` (string): ID of the task (with no more than 100 links) to add to the VIP queue.

**Response Codes & Fields:**
*   `code` (number):
    *   `0`: Task successfully added to VIP queue.
    *   `1`: Top up balance.
    *   `-2`: Server overloaded. Repeat in 5 sec.
    *   `-3`: Task not found.
    *   `-4`: Already added to VIP queue.
    *   `-5`: More than 100 links found in the task.
*   `message` (string): "`OK`" if successful.

**Request Example (curl):**
```bash
curl -X POST -H "Authorization: <API KEY>" \
-H 'Content-Type: application/json' \
-d '{"task_id":"680222ce0428e10a6b16bf72"}' \
https://api.speedyindex.com/v2/task/google/indexer/vip
```

**Response Example (JSON):**
```json
{"code":0,"message":"OK"}
```

---

## 9. Pricing

Details about our service packages and pricing.

| Package, links | Indexing links | Checking for index | Indexing links + checking for index |
|----------------|----------------|--------------------|---------------------------------------|
| 1 link         | 0.0075 $       | 0.0015 $           | -                                     |
| 5,000          | 30 $           | 6 $                | 35 $                                  |
| 10,000         | 50 $           | 10 $               | 55 $                                  |
| 25,000         | 100 $          | 25 $               | 115 $                                 |
| 50,000         | 170 $          | 45 $               | 200 $                                 |
| 100,000        | 300 $          | 80 $               | 350 $                                 |

---
```
