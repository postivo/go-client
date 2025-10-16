# Senders
(*Senders*)

## Overview

### Available Operations

* [List](#list) - List senders
* [Add](#add) - Add a new sender
* [Delete](#delete) - Delete a sender
* [Verify](#verify) - Verify sender

## List

Retrieve the list of allowed senders defined in your account. Senders are registered in your account and must be verified and activated before use. Activated senders have `active: true` property and can be used to send shipments. Inactive senders are also returned (`active: false`), but cannot be used until activated.

### Example Usage

<!-- UsageSnippet language="go" operationID="listSenders" method="get" path="/senders" -->
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

    res, err := s.Senders.List(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.SenderDetails != nil {
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

**[*operations.ListSendersResponse](../../models/operations/listsendersresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Add

Create a new sender on your account. The request must contain a `Sender` object. To prevent fraud, all additional senders are verified by mailing a verification code to the sender’s address. Complete the verification using the `verifySender` method. Verified senders have `active: true` and can be used to send shipments. Inactive senders are also returned (`active: false`), but cannot be used until verification is completed.

### Example Usage

<!-- UsageSnippet language="go" operationID="addSender" method="post" path="/senders" -->
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

    res, err := s.Senders.Add(ctx, components.Sender{
        Name: postivo.Pointer("Jan Nowak"),
        Name2: optionalnullable.From(postivo.Pointer("Firma Testowa Sp. z o.o.")),
        Address: postivo.Pointer("ul. Aleje Jerozolimskie"),
        HomeNumber: optionalnullable.From(postivo.Pointer("31")),
        FlatNumber: optionalnullable.From(postivo.Pointer("2")),
        PostCode: postivo.Pointer("00-999"),
        City: postivo.Pointer("Warszawa"),
        Country: optionalnullable.From(postivo.Pointer("PL")),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.SenderDetails != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `request`                                                | [components.Sender](../../models/components/sender.md)   | :heavy_check_mark:                                       | The request object to use for the request.               |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.AddSenderResponse](../../models/operations/addsenderresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Delete

Remove a sender from your account by `id`. Pass the sender’s `id` parameter to remove it. The sender is deleted immediately.

### Example Usage

<!-- UsageSnippet language="go" operationID="deleteSender" method="delete" path="/senders/{id}" -->
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

    res, err := s.Senders.Delete(ctx, 14)
    if err != nil {
        log.Fatal(err)
    }
    if res.ErrorResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | *int64*                                                  | :heavy_check_mark:                                       | Sender `id` to remove.                                   | 14                                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.DeleteSenderResponse](../../models/operations/deletesenderresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 404, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Verify

Verify a sender to activate it. After adding a new sender, a letter containing a verification code is mailed to the sender’s address. Provide this code to complete verification.

### Example Usage

<!-- UsageSnippet language="go" operationID="verifySender" method="patch" path="/senders/{id}" -->
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

    res, err := s.Senders.Verify(ctx, 443, operations.VerifySenderRequestBody{
        VerificationCode: "A345FP73",
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ErrorResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              | Example                                                                                  |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `ctx`                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                    | :heavy_check_mark:                                                                       | The context to use for the request.                                                      |                                                                                          |
| `id`                                                                                     | *int64*                                                                                  | :heavy_check_mark:                                                                       | ID of the sender to verify.                                                              | 443                                                                                      |
| `requestBody`                                                                            | [operations.VerifySenderRequestBody](../../models/operations/verifysenderrequestbody.md) | :heavy_check_mark:                                                                       | Verification code received in the letter.                                                |                                                                                          |
| `opts`                                                                                   | [][operations.Option](../../models/operations/option.md)                                 | :heavy_minus_sign:                                                                       | The options for this request.                                                            |                                                                                          |

### Response

**[*operations.VerifySenderResponse](../../models/operations/verifysenderresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 404                      | application/json         |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |