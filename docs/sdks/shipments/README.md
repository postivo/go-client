# Shipments

## Overview

### Available Operations

* [Status](#status) - Retrieve shipment details with status events
* [Cancel](#cancel) - Cancel shipments
* [Dispatch](#dispatch) - Dispatch a new shipment
* [Documents](#documents) - Retrieve documents related to a shipment
* [Price](#price) - Check the shipment price

## Status

Retrieve the current status and details for up to **50 shipments** using the IDs assigned when they were created. Separate multiple IDs with commas. Duplicate IDs are processed once.

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

| Parameter                                                                                                                                                                                                                                                                            | Type                                                                                                                                                                                                                                                                                 | Required                                                                                                                                                                                                                                                                             | Description                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                                                                                                                                                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                                                                                                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                                                                                   | The context to use for the request.                                                                                                                                                                                                                                                  |
| `ids`                                                                                                                                                                                                                                                                                | []`string`                                                                                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                                                                   | Shipment IDs assigned by the system (comma-separated). The system accepts a maximum of **50** identifiers per call. Empty items, including leading, trailing or repeated commas, are rejected with HTTP 400. Surrounding whitespace is ignored and duplicate IDs are processed once. |
| `opts`                                                                                                                                                                                                                                                                               | [][operations.Option](../../models/operations/option.md)                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                   | The options for this request.                                                                                                                                                                                                                                                        |

### Response

**[*operations.GetStatusResponse](../../models/operations/getstatusresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Cancel

Cancel up to **50 shipments** using the IDs assigned when they were created. Separate multiple IDs with commas. Only shipments with status `ACCEPTED` can be cancelled; duplicate IDs are processed once.

Check the result for each shipment, as individual cancellations can succeed or fail independently. If processing is interrupted, earlier cancellations may already have completed; check shipment status before retrying.

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

| Parameter                                                                                                                                                                                                                                                                            | Type                                                                                                                                                                                                                                                                                 | Required                                                                                                                                                                                                                                                                             | Description                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `ctx`                                                                                                                                                                                                                                                                                | [context.Context](https://pkg.go.dev/context#Context)                                                                                                                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                                                                                   | The context to use for the request.                                                                                                                                                                                                                                                  |
| `ids`                                                                                                                                                                                                                                                                                | []`string`                                                                                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                                                                   | Shipment IDs assigned by the system (comma-separated). The system accepts a maximum of **50** identifiers per call. Empty items, including leading, trailing or repeated commas, are rejected with HTTP 400. Surrounding whitespace is ignored and duplicate IDs are processed once. |
| `opts`                                                                                                                                                                                                                                                                               | [][operations.Option](../../models/operations/option.md)                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                   | The options for this request.                                                                                                                                                                                                                                                        |

### Response

**[*operations.CancelShipmentResponse](../../models/operations/cancelshipmentresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Dispatch

Submit shipments for up to **50 recipients** using their addresses or Address Book identifiers, documents and optional shipment settings. For larger batches, split the operation into multiple calls. Check each recipient result, as individual shipments can succeed or fail independently.

### Example Usage: advanced_config

<!-- UsageSnippet language="go" operationID="shipmentDispatch" method="post" path="/shipment" example="advanced_config" -->
```go
package main

import(
	"context"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/optionalnullable"
	"github.com/postivo/go-client/models/components"
	"github.com/postivo/go-client/types"
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
        Documents: components.CreateShipmentDocumentsDocuments(
            components.CreateDocumentsDocumentPdf(
                components.DocumentPdf{
                    FileStream: "<document content encoded to base64>",
                    FileName: optionalnullable.From(postivo.Pointer("document.pdf")),
                },
            ),
        ),
        Options: optionalnullable.From(postivo.Pointer(components.CreateOptionsObjShipmentOptions(
            components.ShipmentOptions{
                PredefinedConfigID: optionalnullable.From(postivo.Pointer[int64](2670)),
                InlineConfig: optionalnullable.From(postivo.Pointer(components.CreateInlineConfigUnionInlineConfig(
                    components.InlineConfig{
                        CarrierID: 4,
                        ServiceID: 16,
                        PaperID: postivo.Pointer[int64](1),
                        ColorPrint: postivo.Pointer(true),
                        DuplexPrint: postivo.Pointer(false),
                        EnvelopeID: postivo.Pointer[int64](454),
                        EnvelopeColorPrint: postivo.Pointer(true),
                    },
                ))),
                SenderID: optionalnullable.From(postivo.Pointer[int64](1)),
                DispatchDate: types.MustNewDateFromString("2025-10-21"),
                Callback: optionalnullable.From(postivo.Pointer(components.CreateCallbackUnionCallback(
                    components.Callback{
                        URL: "https://example.com/test",
                        UserToken: optionalnullable.From(postivo.Pointer("75gh28hugjy8gfv6...")),
                    },
                ))),
                MiscInfo: optionalnullable.From(postivo.Pointer(components.CreateMiscInfoUnionMiscInfo(
                    components.MiscInfo{
                        Mpk: optionalnullable.From(postivo.Pointer("dział sprzedaży")),
                        OrderName: optionalnullable.From(postivo.Pointer("Wysyłka zaproszeń do Klientów")),
                    },
                ))),
                RotateDocuments: postivo.Pointer(true),
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
### Example Usage: multi

<!-- UsageSnippet language="go" operationID="shipmentDispatch" method="post" path="/shipment" example="multi" -->
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
        Recipients: components.CreateShipmentRecipientsArrayOfRecipients(
            []components.Recipients{
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
                components.CreateRecipientsRecipientInline(
                    components.RecipientInline{
                        Name: postivo.Pointer("Andrzej Kowalski"),
                        Address: postivo.Pointer("ul. Przykładowa 45/321"),
                        PostCode: postivo.Pointer("34-001"),
                        City: postivo.Pointer("Kraków"),
                        PhoneNumber: optionalnullable.From(postivo.Pointer("+48999888777")),
                        CustomID: optionalnullable.From(postivo.Pointer("my-id-1113")),
                    },
                ),
            },
        ),
        Documents: components.CreateShipmentDocumentsDocuments(
            components.CreateDocumentsDocumentPdf(
                components.DocumentPdf{
                    FileStream: "<document content encoded to base64>",
                    FileName: optionalnullable.From(postivo.Pointer("document.pdf")),
                },
            ),
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
### Example Usage: single

<!-- UsageSnippet language="go" operationID="shipmentDispatch" method="post" path="/shipment" example="single" -->
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
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 415, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Documents

Retrieve a shipment document using the shipment ID and document type. Available documents include dispatch confirmations, envelope previews, EPO certificate visualizations in PDF format and EPO certificates in XML format. Availability depends on the document type and shipment state.

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
| `id`                                                                     | `string`                                                                 | :heavy_check_mark:                                                       | Single shipment ID assigned by the system when the shipment was created. | A0043456                                                                 |
| `type_`                                                                  | [operations.DocumentType](../../models/operations/documenttype.md)       | :heavy_check_mark:                                                       | Type of document/certificate to generate.                                | dispatch_cert                                                            |
| `opts`                                                                   | [][operations.Option](../../models/operations/option.md)                 | :heavy_minus_sign:                                                       | The options for this request.                                            |                                                                          |

### Response

**[*operations.GetDocumentsResponse](../../models/operations/getdocumentsresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Price

Calculate shipment prices for up to **50 recipients** using their addresses or Address Book identifiers, documents and optional shipment settings. For larger batches, split the operation into multiple calls. Check each recipient result to determine whether pricing succeeded.

### Example Usage: advanced_config

<!-- UsageSnippet language="go" operationID="shipmentPrice" method="post" path="/shipment/price" example="advanced_config" -->
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
        Documents: components.CreateShipmentDocumentsDocuments(
            components.CreateDocumentsDocumentPdf(
                components.DocumentPdf{
                    FileStream: "<document content encoded to base64>",
                    FileName: optionalnullable.From(postivo.Pointer("document.pdf")),
                },
            ),
        ),
        Options: optionalnullable.From(postivo.Pointer(components.CreateOptionsObjShipmentOptions(
            components.ShipmentOptions{
                PredefinedConfigID: optionalnullable.From(postivo.Pointer[int64](2670)),
                InlineConfig: optionalnullable.From(postivo.Pointer(components.CreateInlineConfigUnionInlineConfig(
                    components.InlineConfig{
                        CarrierID: 4,
                        ServiceID: 16,
                        PaperID: postivo.Pointer[int64](1),
                        ColorPrint: postivo.Pointer(true),
                        DuplexPrint: postivo.Pointer(false),
                        EnvelopeID: postivo.Pointer[int64](454),
                        EnvelopeColorPrint: postivo.Pointer(true),
                    },
                ))),
                SenderID: optionalnullable.From(postivo.Pointer[int64](1)),
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
### Example Usage: multi

<!-- UsageSnippet language="go" operationID="shipmentPrice" method="post" path="/shipment/price" example="multi" -->
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
        Recipients: components.CreateShipmentRecipientsArrayOfRecipients(
            []components.Recipients{
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
                components.CreateRecipientsRecipientInline(
                    components.RecipientInline{
                        Name: postivo.Pointer("Andrzej Kowalski"),
                        Address: postivo.Pointer("ul. Przykładowa 45/321"),
                        PostCode: postivo.Pointer("34-001"),
                        City: postivo.Pointer("Kraków"),
                        PhoneNumber: optionalnullable.From(postivo.Pointer("+48999888777")),
                        CustomID: optionalnullable.From(postivo.Pointer("my-id-1113")),
                    },
                ),
            },
        ),
        Documents: components.CreateShipmentDocumentsDocuments(
            components.CreateDocumentsDocumentPdf(
                components.DocumentPdf{
                    FileStream: "<document content encoded to base64>",
                    FileName: optionalnullable.From(postivo.Pointer("document.pdf")),
                },
            ),
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
### Example Usage: single

<!-- UsageSnippet language="go" operationID="shipmentPrice" method="post" path="/shipment/price" example="single" -->
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
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 415, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |