# Examples

The `ballerinax/ai.azure.search` connector provides practical examples illustrating usage in various scenarios. Explore these [examples](https://github.com/ballerina-platform/module-ballerinax-ai.azure.search/tree/main/examples), covering use cases like index management, document indexing, search operations, and document querying.

1. [RAG ingestion](https://github.com/ballerina-platform/module-ballerinax-ai.azure.search/tree/main/examples/rag-ingestion) - A comprehensive example demonstrating the complete Azure AI Search workflow including data source creation, index creation, indexer setup, and execution.
2. [Document search](https://github.com/ballerina-platform/module-ballerinax-ai.azure.search/tree/main/examples/document-search) - Demonstrates how to query and search documents in an Azure AI Search index using various search parameters and filters.

## Prerequisites

1. Set up Azure AI Search service as described in the [Setup guide](https://central.ballerina.io/ballerinax/ai.azure.search/latest#setup-guide).

2. For each example, create a `Config.toml` file the related configuration. Here's an example of how your `Config.toml` file should look:

    ```toml
    serviceUrl = "https://your-service.search.windows.net"
    adminKey = "<Admin Key>"
    apiKey = "<API Key>"
    ```

## Running an example

Execute the following commands to build an example from the source:

* To build an example:

    ```bash
    bal build
    ```

* To run an example:

    ```bash
    bal run
    ```

## Building the examples with the local module

**Warning**: Due to the absence of support for reading local repositories for single Ballerina files, the Bala of the module is manually written to the central repository as a workaround. Consequently, the bash script may modify your local Ballerina repositories.

Execute the following commands to build all the examples against the changes you have made to the module locally:

* To build all the examples:

    ```bash
    ./build.sh build
    ```

* To run all the examples:

    ```bash
    ./build.sh run
    ```
