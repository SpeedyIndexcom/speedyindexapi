# SpeedyIndex API v2 Documentation HTML

This repository contains the HTML source code for the SpeedyIndex API v2 documentation. The documentation is designed to provide developers with a comprehensive guide to integrating with the SpeedyIndex service for programmatic URL indexing and index checking.

## About SpeedyIndex

SpeedyIndex offers a robust and efficient solution for:

*   **Accelerated Content Discovery:** Get your new or updated content indexed quickly by major search engines like Google and Yandex.
*   **Bulk URL Index Checking:** Programmatically verify the indexation status of multiple URLs.
*   **Website Re-indexing:** Automate the process of re-submitting your website's pages after updates.
*   **Forced Indexing Capabilities:** Ensure your fresh content doesn't wait long to be discovered.

The API supports both Google and Yandex, providing a versatile tool for managing your website's search engine presence.

## Documentation Features

The HTML documentation page includes:

*   **Clear Navigation:** A fixed sidebar allows for easy navigation between different API endpoint descriptions.
*   **Semantic Structure:** Well-organized content using appropriate HTML tags for better readability and accessibility.
*   **Detailed Endpoint Descriptions:** Each API endpoint is documented with:
    *   HTTP Method (GET/POST)
    *   Endpoint URL
    *   Required Headers
    *   Request Parameters/Body
    *   Response Fields and Codes
    *   `curl` Request Examples
    *   JSON Response Examples
*   **Usability Focused Design:**
    *   Responsive layout for various screen sizes.
    *   Distinct styling for code blocks, parameters, and important notes.
    *   A clear pricing table.
*   **Quick Links:** Prominent links to key SpeedyIndex service pages:
    *   [Links Indexing](https://en.speedyindex.com)
    *   [Reindex Website](https://en.speedyindex.com/reindex-website/)
    *   [Index Checker](https://en.speedyindex.com/google-index-checker/)
    *   [Free Sitemap Extractor](https://en.speedyindex.com/free-xml-sitemap-url-extractor/)
*   **SEO Considerations:** Incorporates relevant low-frequency keywords to describe the service's capabilities naturally.

## API Endpoints Covered

The documentation details the following SpeedyIndex API v2 endpoints:

*   **Introduction:** Overview of the API and its benefits.
*   **Check Balance:** (`GET /v2/account`) Retrieve your current account balance.
*   **Task Creation:** (`POST /v2/task/<SEARCH_ENGINE>/<TASK_TYPE>/create`) Create new indexing or checking tasks.
*   **List Tasks:** (`GET /v2/task/<SEARCH_ENGINE>/<TASK_TYPE>/list/<PAGE>`) Get a paginated list of your tasks.
*   **Task Status:** (`POST /v2/task/<SEARCH_ENGINE>/<TASK_TYPE>/status`) Check the status of specific tasks.
*   **Download Report:** (`POST /v2/task/<SEARCH_ENGINE>/<TASK_TYPE>/fullreport`) Download a detailed report for a completed task.
*   **Index Single Link:** (`POST /v2/<SEARCH_ENGINE>/url`) Submit a single URL for quick indexing.
*   **Create Invoice:** (`POST /v2/account/invoice/create`) Generate a payment invoice to top up your balance.
*   **VIP Queue:** (`POST /v2/task/google/indexer/vip`) Add a task to the high-priority VIP queue (Google Indexer only).
*   **Pricing:** Information on service packages and costs.

## How to Use

1.  **Open the HTML File:** Simply open the `[your_html_filename].html` file in any modern web browser to view the documentation.
2.  **Navigate:** Use the sidebar navigation to jump to specific sections of the API documentation.
3.  **Review Endpoints:** Read through the details for each endpoint relevant to your integration needs.
4.  **Use Examples:** Refer to the `curl` and JSON examples as a guide for making your API requests.

## Technologies Used

*   HTML5
*   CSS3 (with CSS Variables for theming)
*   JavaScript (for basic smooth scrolling)

## Contributing

While this is primarily a static documentation page, suggestions for improving clarity, accuracy, or usability are welcome. Please open an issue or submit a pull request.

## License

This documentation is provided for use with the SpeedyIndex API. Please refer to the SpeedyIndex terms of service for API usage guidelines.
