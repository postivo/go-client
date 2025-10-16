# Accounts
(*Accounts*)

## Overview

### Available Operations

* [Get](#get) - Retrieve account details
* [GetSubaccount](#getsubaccount) - Get subaccount details

## Get

Retrieve the current account balance and other account details. You can also check the account limit and whether the account is a **main** account. Main accounts have unrestricted privileges and, via the [User Panel](https://panel.postivo.pl), you can create as many subaccounts as needed.

### Example Usage

<!-- UsageSnippet language="go" operationID="getAccountDetails" method="get" path="/account" -->
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

    res, err := s.Accounts.Get(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.AccountResponse != nil {
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

**[*operations.GetAccountDetailsResponse](../../models/operations/getaccountdetailsresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 403, 4XX            | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## GetSubaccount

Check the account balance and other details, such as the subcredit balance of a subaccount. Subaccounts are additional users who can access your account’s services and data. You can restrict access levels and set privileges for subaccounts in the [User Panel](https://panel.postivo.pl).

Provide the full subaccount login to access its data.

### Example Usage

<!-- UsageSnippet language="go" operationID="getSubaccountDetails" method="get" path="/account/{user_login}" -->
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

    res, err := s.Accounts.GetSubaccount(ctx, "some-login")
    if err != nil {
        log.Fatal(err)
    }
    if res.AccountResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                  | Type                                                       | Required                                                   | Description                                                | Example                                                    |
| ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- | ---------------------------------------------------------- |
| `ctx`                                                      | [context.Context](https://pkg.go.dev/context#Context)      | :heavy_check_mark:                                         | The context to use for the request.                        |                                                            |
| `userLogin`                                                | *string*                                                   | :heavy_check_mark:                                         | Login of the subaccount (user) for which to retrieve data. | some-login                                                 |
| `opts`                                                     | [][operations.Option](../../models/operations/option.md)   | :heavy_minus_sign:                                         | The options for this request.                              |                                                            |

### Response

**[*operations.GetSubaccountDetailsResponse](../../models/operations/getsubaccountdetailsresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 403, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |