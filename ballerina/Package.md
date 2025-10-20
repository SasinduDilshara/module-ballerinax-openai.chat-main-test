## Overview

[Azure AI Search](https://azure.microsoft.com/products/ai-services/ai-search/) (formerly known as Azure Cognitive Search) is a cloud search service that gives developers infrastructure, APIs, and tools for building a rich search experience over private, heterogeneous content in web, mobile, and enterprise applications.

The `ballarinax/ai.azure.search` package offers functionality to connect and interact with [Azure AI Search REST API](https://docs.microsoft.com/en-us/rest/api/searchservice/) enabling seamless integration with Azure's powerful search and indexing capabilities for building comprehensive search solutions.

## Setup guide

To use the Azure AI Search Connector, you must have an Azure subscription and an Azure AI Search service. If you do not have an Azure account, you can sign up for one at the [Azure portal](https://azure.microsoft.com/free/).

### Create an Azure AI Search service

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Click on "Create a resource" and search for "Azure AI Search".

3. Select "Azure AI Search" and click "Create".

4. Fill in the required details:
   - Resource group: Select or create a new resource group
   - Service name: Choose a unique name for your search service
   - Location: Select a region close to your application
   - Pricing tier: Choose the appropriate tier based on your needs

5. Click "Review + create" and then "Create" to provision the service.

### Get the service URL and admin key

1. Once the service is created, navigate to your Azure AI Search service in the Azure portal.

2. In the "Overview" section, note the URL (e.g., `https://your-service.search.windows.net`).

3. Navigate to "Keys" in the left menu to find your admin keys.

4. Copy either the primary or secondary admin key to use in your application.

## Quickstart

To use the `Azure AI Search` connector in your Ballerina application, update the `.bal` file as follows:

### Step 1: Import the module

Import the `ballerinax/ai.azure.search` module.

```ballerina
import ballerinax/ai.azure.search as azureSearch;
```

### Step 2: Create a new connector instance

Create an `azureSearch:Client` with your Azure AI Search service URL and admin key.

```ballerina
configurable string serviceUrl = ?;
configurable string adminKey = ?;

final azureSearch:Client searchClient = check new(serviceUrl, {
    auth: {
        apiKey: adminKey
    }
});
```

### Step 3: Invoke the connector operation

Now, you can utilize available connector operations.

#### Create a search index

```ballerina
public function main() returns error? {

    // Define a simple search index
    azureSearch:SearchIndex searchIndex = {
        name: "hotels",
        fields: [
            {
                name: "id",
                'type: "Edm.String",
                'key: true,
                searchable: false
            },
            {
                name: "name",
                'type: "Edm.String",
                searchable: true,
                filterable: true
            }
        ]
    };

    azureSearch:SearchIndex response = check searchClient->indexesCreate(searchIndex);
}
```

### Step 4: Run the Ballerina application

```bash
bal run
```

## Examples

The `Azure AI Search` connector provides practical examples illustrating usage in various scenarios. Explore these [examples](https://github.com/ballerina-platform/module-ballerinax-ai.azure.search/tree/main/examples/), covering the following use cases:

1. [RAG ingestion](https://github.com/ballerina-platform/module-ballerinax-ai.azure.search/tree/main/examples/rag-ingestion) - A comprehensive example demonstrating the complete Azure AI Search workflow including data source creation, index creation, indexer setup, and execution.
