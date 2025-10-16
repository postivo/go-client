# Contacts
(*AddressBook.Contacts*)

## Overview

### Available Operations

* [List](#list) - List contacts
* [Add](#add) - Add a new contact
* [Get](#get) - Retrieve contact details
* [Update](#update) - Update a contact
* [Delete](#delete) - Delete a contact
* [RemoveFromGroup](#removefromgroup) - Remove a contact from a group
* [AddToGroup](#addtogroup) - Add a contact to a group

## List

Retrieve a paginated list of all contacts defined in your account’s **Address Book**.

### Example Usage

<!-- UsageSnippet language="go" operationID="listContacts" method="get" path="/contacts" -->
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

    res, err := s.AddressBook.Contacts.List(ctx, postivo.Pointer[int64](1), postivo.Pointer[int64](10))
    if err != nil {
        log.Fatal(err)
    }
    if res.ContactResponses != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `page`                                                   | **int64*                                                 | :heavy_minus_sign:                                       | Page number of results                                   | 1                                                        |
| `limit`                                                  | **int64*                                                 | :heavy_minus_sign:                                       | Results limit per page.                                  | 10                                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.ListContactsResponse](../../models/operations/listcontactsresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Add

Create a new contact in your account’s **Address Book**.

### Example Usage

<!-- UsageSnippet language="go" operationID="addContact" method="post" path="/contacts" -->
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

    res, err := s.AddressBook.Contacts.Add(ctx, components.Contact{
        Name: postivo.Pointer("Jan Nowak"),
        Name2: optionalnullable.From(postivo.Pointer("Firma Testowa Sp. z o.o.")),
        Address: postivo.Pointer("ul. Aleje Jerozolimskie"),
        HomeNumber: optionalnullable.From(postivo.Pointer("31")),
        FlatNumber: optionalnullable.From(postivo.Pointer("2")),
        PostCode: postivo.Pointer("00-999"),
        City: postivo.Pointer("Warszawa"),
        PhoneNumber: optionalnullable.From(postivo.Pointer("+48999999999")),
        ExtID: optionalnullable.From(postivo.Pointer("my-contact-1")),
        GroupIds: optionalnullable.From(postivo.Pointer([]int64{
            13,
            534,
        })),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ContactResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |
| `request`                                                | [components.Contact](../../models/components/contact.md) | :heavy_check_mark:                                       | The request object to use for the request.               |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |

### Response

**[*operations.AddContactResponse](../../models/operations/addcontactresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Get

Get the details of a contact from your Address Book using its global `id`.

### Example Usage

<!-- UsageSnippet language="go" operationID="getContactById" method="get" path="/contacts/{id}" -->
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

    res, err := s.AddressBook.Contacts.Get(ctx, 14)
    if err != nil {
        log.Fatal(err)
    }
    if res.ContactResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | *int64*                                                  | :heavy_check_mark:                                       | Global contact `id` to fetch.                            | 14                                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.GetContactByIDResponse](../../models/operations/getcontactbyidresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Update

Update a contact by its global ID.

### Example Usage

<!-- UsageSnippet language="go" operationID="updateContact" method="put" path="/contacts/{id}" -->
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

    res, err := s.AddressBook.Contacts.Update(ctx, 14, components.Contact{
        Name: postivo.Pointer("Jan Nowak"),
        Name2: optionalnullable.From(postivo.Pointer("Firma Testowa Sp. z o.o.")),
        Address: postivo.Pointer("ul. Aleje Jerozolimskie"),
        HomeNumber: optionalnullable.From(postivo.Pointer("31")),
        FlatNumber: optionalnullable.From(postivo.Pointer("2")),
        PostCode: postivo.Pointer("00-999"),
        City: postivo.Pointer("Warszawa"),
        PhoneNumber: optionalnullable.From(postivo.Pointer("+48999999999")),
        ExtID: optionalnullable.From(postivo.Pointer("my-contact-1")),
        GroupIds: optionalnullable.From(postivo.Pointer([]int64{
            13,
            534,
        })),
    })
    if err != nil {
        log.Fatal(err)
    }
    if res.ContactResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | *int64*                                                  | :heavy_check_mark:                                       | ID of the contact to update.                             | 14                                                       |
| `contact`                                                | [components.Contact](../../models/components/contact.md) | :heavy_check_mark:                                       | A `Contact` object with the updated fields.              |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.UpdateContactResponse](../../models/operations/updatecontactresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 404, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Delete

Remove a contact from your account by system ID.

### Example Usage

<!-- UsageSnippet language="go" operationID="deleteContact" method="delete" path="/contacts/{id}" -->
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

    res, err := s.AddressBook.Contacts.Delete(ctx, 14)
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
| `id`                                                     | *int64*                                                  | :heavy_check_mark:                                       | Global contact `id` to remove.                           | 14                                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.DeleteContactResponse](../../models/operations/deletecontactresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 404, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## RemoveFromGroup

Remove a contact from a group in your Address Book. This does not delete the contact; it only detaches the contact from the group.

Provide the contact’s `id` and the group’s `group_id` parameters to perform the detachment.

### Example Usage

<!-- UsageSnippet language="go" operationID="removeContactFromGroup" method="delete" path="/contacts/{id}/group/{group_id}" -->
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

    res, err := s.AddressBook.Contacts.RemoveFromGroup(ctx, 35, 656)
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
| `id`                                                     | *int64*                                                  | :heavy_check_mark:                                       | Global contact `id` to detach from the group.            | 35                                                       |
| `groupID`                                                | *int64*                                                  | :heavy_check_mark:                                       | Group `id` to detach from the contact.                   | 656                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.RemoveContactFromGroupResponse](../../models/operations/removecontactfromgroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 404                      | application/json         |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## AddToGroup

Assign a contact to a group. If a contact and a group exist in your account, you can add the contact to that group.

Provide the contact’s `id` and the group’s `group_id` parameters to perform the assignment.

### Example Usage

<!-- UsageSnippet language="go" operationID="addContactToGroup" method="patch" path="/contacts/{id}/group/{group_id}" -->
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

    res, err := s.AddressBook.Contacts.AddToGroup(ctx, 35, 656)
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
| `id`                                                     | *int64*                                                  | :heavy_check_mark:                                       | Global contact `id` to add to the group.                 | 35                                                       |
| `groupID`                                                | *int64*                                                  | :heavy_check_mark:                                       | Group `id` to associate with the contact.                | 656                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.AddContactToGroupResponse](../../models/operations/addcontacttogroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 404                      | application/json         |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |