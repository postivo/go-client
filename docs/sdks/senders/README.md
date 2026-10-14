# Senders

## Overview

### Available Operations

* [List](#list) - List senders
* [Add](#add) - Add a new sender
* [Delete](#delete) - Delete a sender
* [Verify](#verify) - Verify sender

## List

Retrieve the senders defined in your account. Active, verified senders can be used for shipments. Inactive senders are also included in the list.

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
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 4XX            | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Add

Create a sender using its address details. Additional senders are verified by mailing a verification code to the sender's address. Complete verification with the received code to activate the sender.

The sender can be created before the verification letter is sent. If sending the letter fails, retrieve the sender list before retrying creation.

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
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 409, 415, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Delete

Remove a sender using its system ID. The account's default sender must be retained.

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
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | `int64`                                                  | :heavy_check_mark:                                       | Sender `id` to remove.                                   | 14                                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.DeleteSenderResponse](../../models/operations/deletesenderresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 409, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Verify

Activate a sender using the verification code received by mail. The code must match the current verification request, and the sender must still be awaiting verification.

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
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              | Example                                                                                  |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `ctx`                                                                                    | [context.Context](https://pkg.go.dev/context#Context)                                    | :heavy_check_mark:                                                                       | The context to use for the request.                                                      |                                                                                          |
| `id`                                                                                     | `int64`                                                                                  | :heavy_check_mark:                                                                       | ID of the sender to verify.                                                              | 443                                                                                      |
| `requestBody`                                                                            | [operations.VerifySenderRequestBody](../../models/operations/verifysenderrequestbody.md) | :heavy_check_mark:                                                                       | Verification code received in the letter.                                                |                                                                                          |
| `opts`                                                                                   | [][operations.Option](../../models/operations/option.md)                                 | :heavy_minus_sign:                                                                       | The options for this request.                                                            |                                                                                          |

### Response

**[*operations.VerifySenderResponse](../../models/operations/verifysenderresponse.md), error**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| apierrors.ErrorResponse      | 401, 405                     | application/problem+json     |
| apierrors.ErrorResponse      | 400, 403, 404, 409, 415, 4XX | application/problem+json     |
| apierrors.ErrorResponse      | 5XX                          | application/problem+json     |