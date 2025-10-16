# Common
(*Common*)

## Overview

Common

### Available Operations

* [Ping](#ping) - Check API availability and version

## Ping

Check the API connection and current availability status. The response also includes the current API version.

### Example Usage

<!-- UsageSnippet language="go" operationID="ping" method="get" path="/ping" -->
```go
package main

import(
	"context"
	postivo "github.com/postivo/go-client"
	"log"
)

func main() {
    ctx := context.Background()

    s := postivo.New()

    res, err := s.Common.Ping(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.PingResponse != nil {
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

**[*operations.PingResponse](../../models/operations/pingresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 4XX                 | application/problem+json |
| apierrors.ErrorResponse  | 503, 5XX                 | application/problem+json |