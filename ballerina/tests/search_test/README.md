# Running Tests

## Prerequisites

You need an Azure AI Search service and admin key to run live tests.

To set up Azure AI Search, refer to the [Ballerina Azure AI Search Connector](https://github.com/ballerina-platform/module-ballerinax-ai.azure.search/blob/main/ballerina/Module.md).

## Test Environments

There are two test environments for running the `ai.azure.search` connector tests. The default environment is a mock server for the Azure AI Search API. The other environment is the actual Azure AI Search service.

You can run the tests in either of these environments, and each has its own compatible set of tests.

| Test Groups | Environment                                           |
|-------------|-------------------------------------------------------|
| mock_tests  | Mock server for Azure AI Search API (Default Environment) |
| live_tests  | Azure AI Search service                               |

## Running Tests in the Mock Server

To execute the tests on the mock server, ensure that the `isLiveServer` environment variable is either set to `false` or left unset before initiating the tests.

This environment variable can be configured within the `Config.toml` file located in the `tests` directory or specified as an environment variable.

The mock server tests include:
- **testCreateSearchIndex**: Tests creating a search index with multiple field types
- **testListIndexes**: Tests retrieving all available indexes
- **testGetServiceStatistics**: Tests getting Azure AI Search service statistics

### Using a `Config.toml` File

Create a `Config.toml` file in the `tests` directory with the following content:

```toml
isLiveServer = false
```

### Using Environment Variables

Alternatively, you can set the environment variable directly.

For Linux or macOS:

```bash
export IS_LIVE_SERVER=false
```

For Windows:

```bash
setx IS_LIVE_SERVER false
```

Then, run the following command to execute the tests:

```bash
./gradlew clean test
```

## Running Tests Against the Azure AI Search Live Service

### Using a `Config.toml` File

Create a `Config.toml` file in the `tests` directory and add your Azure AI Search service configuration:

```toml
isLiveServer = true
serviceUrl = "https://your-search-service.search.windows.net"
adminKey = "<your-azure-search-admin-key>"
```

### Using Environment Variables for Live Tests

Alternatively, you can set your Azure AI Search service credentials as environment variables.

For Linux or macOS:

```bash
export IS_LIVE_SERVER=true
export AZURE_SEARCH_SERVICE_URL="https://your-search-service.search.windows.net"
export AZURE_SEARCH_ADMIN_KEY="<your-azure-search-admin-key>"
```

For Windows:

```bash
setx IS_LIVE_SERVER true
setx AZURE_SEARCH_SERVICE_URL "https://your-search-service.search.windows.net"
setx AZURE_SEARCH_ADMIN_KEY "<your-azure-search-admin-key>"
```

Then, run the following command to execute the tests:

```bash
./gradlew clean test
```

## Test Details

The test suite includes the following test cases:

### testCreateSearchIndex
- Creates a search index with unique name (using UUID)
- Tests multiple field types: String (id, title, content) and Double (rating)
- Validates field attributes: key, searchable, filterable, sortable
- Verifies the created index name and field count

### testListIndexes
- Retrieves all available search indexes
- Validates that the response contains a list of indexes
- Ensures the API returns a proper `ListIndexesResult` structure

### testGetServiceStatistics
- Fetches Azure AI Search service statistics
- Validates the presence of service counters (document count, index count, storage size)
- Ensures proper `ServiceStatistics` structure in response

## Mock Service Endpoints

The mock service provides the following endpoints for testing:
- `POST /indexes` - Creates a new search index
- `GET /indexes` - Lists all search indexes  
- `GET /servicestats` - Returns service statistics

All mock endpoints return realistic Azure AI Search API responses with proper data structures and validation.
