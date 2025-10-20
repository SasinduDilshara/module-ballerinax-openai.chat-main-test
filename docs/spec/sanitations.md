_Authors_: @SasinduDilshara \
_Created_: 2025/10/20 \
_Edition_: Swan Lake

# Sanitation for OpenAPI specification

This document records the sanitation done on top of the official OpenAPI specification from Azure AI Search Service.
The OpenAPI specification is obtained from the [Azure REST API Specifications repository](https://github.com/Azure/azure-rest-api-specs/blob/main/specification/search/data-plane/Azure.Search/stable/2025-09-01/searchservice.json).
These changes are done in order to improve the overall usability, and as workarounds for some known language limitations.

1. **Replaced external references to Azure common types with inline definitions**:

   - **Changed References**: All `"$ref": "../../../../../common-types/data-plane/v1/types.json#/definitions/ErrorResponse"` references

   - **Original**:

      ```json
      "$ref": "../../../../../common-types/data-plane/v1/types.json#/definitions/ErrorResponse"
      ```

   - **Updated**:

      ```json
      "$ref": "#/definitions/ErrorResponse"
      ```

   - **Reason**: External references to Azure common types were replaced with inline definitions to create a self-contained OpenAPI specification that doesn't require external dependencies. This improves portability and ensures the specification can be processed independently.

2. **Added inline ErrorResponse, ErrorDetail, and ErrorAdditionalInfo schema definitions**:

   - **Added Schemas**: `ErrorResponse`, `ErrorDetail`, `ErrorAdditionalInfo`

   - **New Definitions**:
      - `ErrorResponse`: Common error response for all Azure Resource Manager APIs
      - `ErrorDetail`: The error detail with code, message, target, and nested details
      - `ErrorAdditionalInfo`: The resource management error additional info

   - **Reason**: These schema definitions were added to replace the external references and provide complete error response structures within the specification itself.

3. **Removed x-ms-examples from all operations**:

   - **Changed Operations**: All API operations that previously contained `x-ms-examples`

   - **Original**:

      ```json
      "x-ms-examples": {
        "SearchServiceCreateOrUpdateDataSource": {
          "$ref": "./examples/SearchServiceCreateOrUpdateDataSource.json"
        }
      }
      ```

   - **Updated**:
      - Removed the entire `x-ms-examples` property

   - **Reason**: External example references can cause issues during client generation and may not be necessary for basic API functionality. Removing these references makes the specification cleaner and more portable.

4. **Changed externalDocs to x-externalDocs**:

   - **Changed Property**: `externalDocs` → `x-externalDocs`

   - **Original**:

      ```json
      "externalDocs": {
        "url": "https://learn.microsoft.com/rest/api/searchservice/..."
      }
      ```

   - **Updated**:

      ```json
      "x-externalDocs": {
        "url": "https://learn.microsoft.com/rest/api/searchservice/..."
      }
      ```

   - **Reason**: Changed to use vendor extension format to avoid potential conflicts with OpenAPI specification processing tools that may have strict requirements for the standard `externalDocs` property.

## OpenAPI cli command

The following command was used to generate the Ballerina client from the OpenAPI specification. The command should be executed from the repository root directory.

```bash
bal openapi -i docs/spec/openapi.json --mode client --license docs/license.txt -o ballerina
```
