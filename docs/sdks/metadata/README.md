# Metadata
(*Metadata*)

## Overview

### Available Operations

* [List](#list) - List metadata
* [GetPredefinedConfigs](#getpredefinedconfigs) - List predefined configs

## List

Retrieve a complete list of all types for shipments and their possible values. The method has no body and takes no parameters. The response includes metadata such as carrier types, service types, and more.

### Example Usage

<!-- UsageSnippet language="go" operationID="listMetadata" method="get" path="/metadata" -->
```go
package main

import(
	"context"
	postivo "github.com/postivo/go-client"
	"log"
)

func main() {
    ctx := context.Background()

    s := postivo.New(
        postivo.WithSecurity("<YOUR API ACCESS TOKEN>"),
    )

    res, err := s.Metadata.List(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.MetadataResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ListMetadataResponse](../../models/operations/listmetadataresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## GetPredefinedConfigs

Retrieve a complete list of predefined shipment configurations. The method has no body and takes no parameters. The response includes all stored configuration options.

### Example Usage

<!-- UsageSnippet language="go" operationID="listPredefinedConfigs" method="get" path="/metadata/predefined-configs" -->
```go
package main

import(
	"context"
	postivo "github.com/postivo/go-client"
	"log"
)

func main() {
    ctx := context.Background()

    s := postivo.New(
        postivo.WithSecurity("<YOUR API ACCESS TOKEN>"),
    )

    res, err := s.Metadata.GetPredefinedConfigs(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.PredefinedConfigs != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.ListPredefinedConfigsResponse](../../models/operations/listpredefinedconfigsresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |