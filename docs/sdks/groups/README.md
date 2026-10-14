# AddressBook.Groups

## Overview

### Available Operations

* [List](#list) - List groups
* [Add](#add) - Add a new group
* [Get](#get) - Retrieve group details
* [Update](#update) - Update a group
* [Delete](#delete) - Delete a group

## List

Retrieve all contact groups defined in your account's Address Book. An Address Book without groups returns an empty list.

### Example Usage

<!-- UsageSnippet language="go" operationID="listGroups" method="get" path="/groups" -->
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

    res, err := s.AddressBook.Groups.List(ctx)
    if err != nil {
        log.Fatal(err)
    }
    if res.GroupResponses != nil {
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

**[*operations.ListGroupsResponse](../../models/operations/listgroupsresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 4XX            | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Add

Create a new contact group in your account's Address Book.

### Example Usage

<!-- UsageSnippet language="go" operationID="addGroup" method="post" path="/groups" -->
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

    res, err := s.AddressBook.Groups.Add(ctx, components.Group{
        Name: "my-group",
        Description: optionalnullable.From(postivo.Pointer("This is a group for school contacts")),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.GroupResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `request`                                                | [components.Group](../../models/components/group.md)     | :heavy_check_mark:                                       | The request object to use for the request.               |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.AddGroupResponse](../../models/operations/addgroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 415, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Get

Get the details of an Address Book group using the system ID assigned when the group was created.

### Example Usage

<!-- UsageSnippet language="go" operationID="getGroupById" method="get" path="/groups/{id}" -->
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

    res, err := s.AddressBook.Groups.Get(ctx, 194)
    if err != nil {
        log.Fatal(err)
    }
    if res.GroupResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | `int64`                                                  | :heavy_check_mark:                                       | Group id to fetch                                        | 194                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.GetGroupByIDResponse](../../models/operations/getgroupbyidresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 404, 4XX            | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Update

Update an Address Book group using its system ID. Submitting unchanged details leaves the group unchanged.

### Example Usage

<!-- UsageSnippet language="go" operationID="updateGroup" method="put" path="/groups/{id}" -->
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

    res, err := s.AddressBook.Groups.Update(ctx, 14, components.Group{
        Name: "my-group",
        Description: optionalnullable.From(postivo.Pointer("This is a group for school contacts")),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.GroupResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | `int64`                                                  | :heavy_check_mark:                                       | Group `id` to update.                                    | 14                                                       |
| `group`                                                  | [components.Group](../../models/components/group.md)     | :heavy_check_mark:                                       | Updated contact group details.                           |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.UpdateGroupResponse](../../models/operations/updategroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 415, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Delete

Remove an Address Book group using its system ID. By default, its contacts remain in the Address Book and their membership in the removed group is cleared. You can also choose to delete the contacts belonging to the group.

### Example Usage

<!-- UsageSnippet language="go" operationID="deleteGroup" method="delete" path="/groups/{id}" -->
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

    res, err := s.AddressBook.Groups.Delete(ctx, 876, operations.ContactHandlingDetach.ToPointer())
    if err != nil {
        log.Fatal(err)
    }
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                 | Type                                                                      | Required                                                                  | Description                                                               | Example                                                                   |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `ctx`                                                                     | [context.Context](https://pkg.go.dev/context#Context)                     | :heavy_check_mark:                                                        | The context to use for the request.                                       |                                                                           |
| `id`                                                                      | `int64`                                                                   | :heavy_check_mark:                                                        | Group `id` to remove.                                                     | 876                                                                       |
| `contacts`                                                                | [*operations.ContactHandling](../../models/operations/contacthandling.md) | :heavy_minus_sign:                                                        | How to handle contacts that belong to the group.                          |                                                                           |
| `opts`                                                                    | [][operations.Option](../../models/operations/option.md)                  | :heavy_minus_sign:                                                        | The options for this request.                                             |                                                                           |

### Response

**[*operations.DeleteGroupResponse](../../models/operations/deletegroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |