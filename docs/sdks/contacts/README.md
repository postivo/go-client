# AddressBook.Contacts

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

Retrieve a paginated list of contacts defined in your account's **Address Book**. An Address Book without contacts returns an empty list.

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
| `page`                                                   | `*int64`                                                 | :heavy_minus_sign:                                       | Page number of results                                   | 1                                                        |
| `limit`                                                  | `*int64`                                                 | :heavy_minus_sign:                                       | Results limit per page.                                  | 10                                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.ListContactsResponse](../../models/operations/listcontactsresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 4XX            | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Add

Create a new contact in your account's **Address Book**. An optional external (custom) ID must be unique within the Address Book.

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
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 409, 415, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Get

Get the details of an Address Book contact using its system ID.

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
| `id`                                                     | `int64`                                                  | :heavy_check_mark:                                       | Global contact `id` to fetch.                            | 14                                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.GetContactByIDResponse](../../models/operations/getcontactbyidresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 404, 4XX            | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Update

Update an Address Book contact using its system ID. Submitting unchanged details leaves the contact unchanged.

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
| `id`                                                     | `int64`                                                  | :heavy_check_mark:                                       | ID of the contact to update.                             | 14                                                       |
| `contact`                                                | [components.Contact](../../models/components/contact.md) | :heavy_check_mark:                                       | Updated contact details.                                 |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.UpdateContactResponse](../../models/operations/updatecontactresponse.md), error**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| apierrors.ErrorResponse      | 401, 405                     | application/problem+json     |
| apierrors.ErrorResponse      | 400, 403, 404, 409, 415, 4XX | application/problem+json     |
| apierrors.ErrorResponse      | 5XX                          | application/problem+json     |

## Delete

Remove an Address Book contact using its system ID.

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
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | `int64`                                                  | :heavy_check_mark:                                       | Global contact `id` to remove.                           | 14                                                       |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.DeleteContactResponse](../../models/operations/deletecontactresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## RemoveFromGroup

Remove a contact from an Address Book group using the contact and group system IDs. The contact remains in the Address Book.

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
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | `int64`                                                  | :heavy_check_mark:                                       | Global contact `id` to detach from the group.            | 35                                                       |
| `groupID`                                                | `int64`                                                  | :heavy_check_mark:                                       | Group `id` to detach from the contact.                   | 656                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.RemoveContactFromGroupResponse](../../models/operations/removecontactfromgroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## AddToGroup

Assign a contact to an Address Book group using the contact and group system IDs. Both the contact and the group must exist in your Address Book.

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
    if res != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                | Type                                                     | Required                                                 | Description                                              | Example                                                  |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `ctx`                                                    | [context.Context](https://pkg.go.dev/context#Context)    | :heavy_check_mark:                                       | The context to use for the request.                      |                                                          |
| `id`                                                     | `int64`                                                  | :heavy_check_mark:                                       | Global contact `id` to add to the group.                 | 35                                                       |
| `groupID`                                                | `int64`                                                  | :heavy_check_mark:                                       | Group `id` to associate with the contact.                | 656                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.AddContactToGroupResponse](../../models/operations/addcontacttogroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 401, 405                 | application/problem+json |
| apierrors.ErrorResponse  | 400, 403, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |