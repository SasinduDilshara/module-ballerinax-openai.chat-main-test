# RAG ingestion AI Search Workflow

This example demonstrates a RAG Azure AI Search workflow including:

1. **Data Source Creation** - Setting up Azure Blob Storage as a data source
2. **Index Creation** - Creating a comprehensive search index with multiple field types
3. **Indexer Creation** - Setting up an automated indexer with scheduling and field mappings
4. **Indexer Execution** - Running the indexer and monitoring its status

## Prerequisites

Before running this example, you need:

1. **Azure AI Search Service** - A provisioned Azure AI Search service
2. **Azure Storage Account** - A storage account with a blob container
3. **Documents** - Sample documents uploaded to your blob container

## Configuration

Create a `Config.toml` file with your Azure services configuration:

```toml
serviceUrl = "https://your-search-service.search.windows.net"
adminKey = "your-admin-key"
storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=yourstorageaccount;AccountKey=yourkey;EndpointSuffix=core.windows.net"
storageContainerName = "documents"
```

## Document Upload

To upload documents to Azure Blob Storage, you can use the Azure Storage Service connector:
**Repository**: https://central.ballerina.io/ballerinax/azure_storage_service/4.3.3

Example usage:
```ballerina
import ballerinax/azure_storage_service.blobs as azblobs;

azblobs:Client blobClient = check new (storageConnectionString);
check blobClient->uploadBlob(containerName, "documents/sample.pdf", fileContent);
```

## Supported File Types

This example is configured to index the following file types:
- PDF documents (`.pdf`)
- Microsoft Word documents (`.docx`)
- Plain text files (`.txt`)
- HTML files (`.html`)
- XML files (`.xml`)
- JSON files (`.json`)

## Features Demonstrated

### Advanced Index Configuration
- Multiple field types (String, Int64, DateTimeOffset)
- Field attributes (searchable, filterable, sortable, facetable)
- CORS configuration for web applications

### Intelligent Indexing
- Automatic content extraction from various document formats
- Metadata preservation (file name, size, modification date, content type)
- Custom field mappings and transformations
- Built-in cognitive skills for language detection and sentiment analysis

### Scheduled Processing
- Automatic indexer scheduling (every 2 hours)
- Batch processing configuration
- Error handling and retry logic
- Execution history tracking

## Running the Example

```bash
bal run
```

## Expected Output

The example will:
1. Create a data source connected to your Azure Blob Storage
2. Create a search index with document and metadata fields
3. Create an indexer with scheduling and field mappings
4. Execute the indexer to process existing documents
5. Display the indexer status and execution history

## Next Steps

After running this example:
1. Upload documents to your Azure Blob Storage container
2. The indexer will automatically process new documents every 2 hours
3. Use search queries to find and retrieve indexed content
4. Monitor indexer performance through the Azure portal

## Monitoring and Maintenance

- Check indexer status regularly using `indexersGetStatus`
- Monitor execution history for errors or performance issues
- Adjust batch size and scheduling based on your data volume
- Update field mappings as your document structure evolves
