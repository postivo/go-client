# Shipments
(*Shipments*)

## Overview

### Available Operations

* [Status](#status) - Retrieve shipment details with status events
* [Cancel](#cancel) - Cancel shipments
* [Dispatch](#dispatch) - Dispatch a new shipment
* [Documents](#documents) - Retrieve documents related to a shipment
* [Price](#price) - Check the shipment price

## Status

Retrieve the current status and details for one or more shipments by their `ids`. Pass the unique shipment IDs (returned when the shipments were created) as a path parameter. To query provide a list (up to **50** IDs per call). For larger batches, split the requests.

### Example Usage

<!-- UsageSnippet language="go" operationID="getStatus" method="get" path="/shipment/{ids}" -->
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

    res, err := s.Shipments.Status(ctx, []string{
        "A0043456",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.StatusDetails != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                           | Type                                                                                                                | Required                                                                                                            | Description                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                               | [context.Context](https://pkg.go.dev/context#Context)                                                               | :heavy_check_mark:                                                                                                  | The context to use for the request.                                                                                 |
| `ids`                                                                                                               | []*string*                                                                                                          | :heavy_check_mark:                                                                                                  | Shipment IDs assigned by the system (comma-separated). The system accepts a maximum of **50** identifiers per call. |
| `opts`                                                                                                              | [][operations.Option](../../models/operations/option.md)                                                            | :heavy_minus_sign:                                                                                                  | The options for this request.                                                                                       |

### Response

**[*operations.GetStatusResponse](../../models/operations/getstatusresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 404, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Cancel

Cancel shipments that have not yet been processed by their `ids`. Pass the unique shipment IDs (returned when the shipment was created) as a parameter. To cancel multiple shipments at once, provide a list of IDs (up to **50** per call). For larger volumes, split the operation into multiple requests. Only shipments with status `ACCEPTED` can be cancelled.

If duplicate shipment IDs are provided in a single call, the API processes each unique ID only once.

### Example Usage

<!-- UsageSnippet language="go" operationID="cancelShipment" method="delete" path="/shipment/{ids}" -->
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

    res, err := s.Shipments.Cancel(ctx, []string{
        "A0043456",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ShipmentCancellations != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                                           | Type                                                                                                                | Required                                                                                                            | Description                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `ctx`                                                                                                               | [context.Context](https://pkg.go.dev/context#Context)                                                               | :heavy_check_mark:                                                                                                  | The context to use for the request.                                                                                 |
| `ids`                                                                                                               | []*string*                                                                                                          | :heavy_check_mark:                                                                                                  | Shipment IDs assigned by the system (comma-separated). The system accepts a maximum of **50** identifiers per call. |
| `opts`                                                                                                              | [][operations.Option](../../models/operations/option.md)                                                            | :heavy_minus_sign:                                                                                                  | The options for this request.                                                                                       |

### Response

**[*operations.CancelShipmentResponse](../../models/operations/cancelshipmentresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 404, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Dispatch

Send a shipment to one or multiple recipients in a single request. Provide a `Shipment` object. The object includes properties that define the shipment (recipient details, included documents, and optional settings). Some fields are required.

The system accepts up to **50** recipients per call. For larger volumes, split the operation into multiple requests.

### Example Usage

<!-- UsageSnippet language="go" operationID="shipmentDispatch" method="post" path="/shipment" -->
```go
package main

import(
	"context"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/optionalnullable"
	"github.com/postivo/go-client/models/components"
	"log"
)

func main() {
    ctx := context.Background()

    s := postivo.New(
        postivo.WithSecurity("<YOUR API ACCESS TOKEN>"),
    )

    res, err := s.Shipments.Dispatch(ctx, components.Shipment{
        Recipients: components.CreateShipmentRecipientsRecipients(
            components.CreateRecipientsRecipientInline(
                components.RecipientInline{
                    Name: postivo.Pointer("Jan Nowak"),
                    Name2: optionalnullable.From(postivo.Pointer("Firma testowa Sp. z o.o.")),
                    Address: postivo.Pointer("ul. Testowa"),
                    HomeNumber: optionalnullable.From(postivo.Pointer("23")),
                    FlatNumber: optionalnullable.From(postivo.Pointer("2")),
                    PostCode: postivo.Pointer("00-999"),
                    City: postivo.Pointer("Warszawa"),
                    PhoneNumber: optionalnullable.From(postivo.Pointer("+48666666666")),
                    Postscript: optionalnullable.From(postivo.Pointer("Komunikat")),
                    CustomID: optionalnullable.From(postivo.Pointer("1234567890")),
                },
            ),
        ),
        Documents: components.CreateShipmentDocumentsArrayOfDocuments(
            []components.Documents{
                components.CreateDocumentsDocumentPdf(
                    components.DocumentPdf{
                        FileStream: "<document_1 content encoded to base64>",
                        FileName: optionalnullable.From(postivo.Pointer("document1.pdf")),
                    },
                ),
                components.CreateDocumentsDocumentPdf(
                    components.DocumentPdf{
                        FileStream: "<document_2 content encoded to base64>",
                        FileName: optionalnullable.From(postivo.Pointer("document2.pdf")),
                    },
                ),
            },
        ),
        Options: optionalnullable.From(postivo.Pointer(components.CreateOptionsObjShipmentOptions(
            components.ShipmentOptions{
                PredefinedConfigID: optionalnullable.From(postivo.Pointer[int64](2670)),
            },
        ))),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ShipmentDetails != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                  | Type                                                       | Required                                                   | Description                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `ctx`                                                      | [context.Context](https://pkg.go.dev/context#Context)      | :heavy_check_mark:                                         | The context to use for the request.                        |
| `request`                                                  | [components.Shipment](../../models/components/shipment.md) | :heavy_check_mark:                                         | The request object to use for the request.                 |
| `opts`                                                     | [][operations.Option](../../models/operations/option.md)   | :heavy_minus_sign:                                         | The options for this request.                              |

### Response

**[*operations.ShipmentDispatchResponse](../../models/operations/shipmentdispatchresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Documents

Download documents related to a shipment by its `id`. Pass the unique shipment `id` (returned when the shipment was created) as a parameter. The second parameter is the document type to download. Supported document types include: dispatch certificate, envelope template, and EPO (in PDF or XML formats).

### Example Usage

<!-- UsageSnippet language="go" operationID="getDocuments" method="get" path="/shipment/{id}/document/{type}" -->
```go
package main

import(
	"context"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/models/operations"
	"log"
)

func main() {
    ctx := context.Background()

    s := postivo.New(
        postivo.WithSecurity("<YOUR API ACCESS TOKEN>"),
    )

    res, err := s.Shipments.Documents(ctx, "A0043456", operations.DocumentTypeDispatchCert)
    if err != nil {
        log.Fatal(err)
    }
    if res.DocumentResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                | Type                                                                     | Required                                                                 | Description                                                              | Example                                                                  |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `ctx`                                                                    | [context.Context](https://pkg.go.dev/context#Context)                    | :heavy_check_mark:                                                       | The context to use for the request.                                      |                                                                          |
| `id`                                                                     | *string*                                                                 | :heavy_check_mark:                                                       | Single shipment ID assigned by the system when the shipment was created. | A0043456                                                                 |
| `type_`                                                                  | [operations.DocumentType](../../models/operations/documenttype.md)       | :heavy_check_mark:                                                       | Type of document/certificate to generate.                                | dispatch_cert                                                            |
| `opts`                                                                   | [][operations.Option](../../models/operations/option.md)                 | :heavy_minus_sign:                                                       | The options for this request.                                            |                                                                          |

### Response

**[*operations.GetDocumentsResponse](../../models/operations/getdocumentsresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 404, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Price

Check the price of a shipment for one or multiple recipients. Provide a `Shipment` object in the request. Each object includes properties such as recipient details, included documents, and optional settings. Some fields are required.

The system accepts up to **50** recipients per call. For larger volumes, split the operation into multiple requests.

### Example Usage

<!-- UsageSnippet language="go" operationID="shipmentPrice" method="post" path="/shipment/price" -->
```go
package main

import(
	"context"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/optionalnullable"
	"github.com/postivo/go-client/models/components"
	"log"
)

func main() {
    ctx := context.Background()

    s := postivo.New(
        postivo.WithSecurity("<YOUR API ACCESS TOKEN>"),
    )

    res, err := s.Shipments.Price(ctx, components.Shipment{
        Recipients: components.CreateShipmentRecipientsRecipients(
            components.CreateRecipientsRecipientInline(
                components.RecipientInline{
                    Name: postivo.Pointer("Jan Nowak"),
                    Name2: optionalnullable.From(postivo.Pointer("Firma testowa Sp. z o.o.")),
                    Address: postivo.Pointer("ul. Testowa"),
                    HomeNumber: optionalnullable.From(postivo.Pointer("23")),
                    FlatNumber: optionalnullable.From(postivo.Pointer("2")),
                    PostCode: postivo.Pointer("00-999"),
                    City: postivo.Pointer("Warszawa"),
                    PhoneNumber: optionalnullable.From(postivo.Pointer("+48666666666")),
                    Postscript: optionalnullable.From(postivo.Pointer("Komunikat")),
                    CustomID: optionalnullable.From(postivo.Pointer("1234567890")),
                },
            ),
        ),
        Documents: components.CreateShipmentDocumentsArrayOfDocuments(
            []components.Documents{
                components.CreateDocumentsDocumentPdf(
                    components.DocumentPdf{
                        FileStream: "<document_1 content encoded to base64>",
                        FileName: optionalnullable.From(postivo.Pointer("document1.pdf")),
                    },
                ),
                components.CreateDocumentsDocumentPdf(
                    components.DocumentPdf{
                        FileStream: "<document_2 content encoded to base64>",
                        FileName: optionalnullable.From(postivo.Pointer("document2.pdf")),
                    },
                ),
            },
        ),
        Options: optionalnullable.From(postivo.Pointer(components.CreateOptionsObjShipmentOptions(
            components.ShipmentOptions{
                PredefinedConfigID: optionalnullable.From(postivo.Pointer[int64](2670)),
            },
        ))),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ShipmentPrices != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                  | Type                                                       | Required                                                   | Description                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `ctx`                                                      | [context.Context](https://pkg.go.dev/context#Context)      | :heavy_check_mark:                                         | The context to use for the request.                        |
| `request`                                                  | [components.Shipment](../../models/components/shipment.md) | :heavy_check_mark:                                         | The request object to use for the request.                 |
| `opts`                                                     | [][operations.Option](../../models/operations/option.md)   | :heavy_minus_sign:                                         | The options for this request.                              |

### Response

**[*operations.ShipmentPriceResponse](../../models/operations/shipmentpriceresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |