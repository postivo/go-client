# ByExtID
(*AddressBook.Contacts.ByExtID*)

## Overview

### Available Operations

* [Get](#get) - Retrieve contact details by EXT_ID
* [Update](#update) - Update a contact by EXT_ID
* [Delete](#delete) - Delete a contact by EXT_ID
* [RemoveFromGroup](#removefromgroup) - Remove a contact from a group by EXT_ID
* [AddToGroup](#addtogroup) - Add a contact to a group by EXT_ID

## Get

Get the details of a contact from your Address Book using your external (custom) ID (the value you defined when creating the contact).

### Example Usage

<!-- UsageSnippet language="go" operationID="getContactByExternalId" method="get" path="/contacts/external/{ext_id}" -->
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

    res, err := s.AddressBook.Contacts.ByExtID.Get(ctx, "my-ext-id-44")
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
| `extID`                                                  | *string*                                                 | :heavy_check_mark:                                       | External (custom) ID of the contact to fetch.            | my-ext-id-44                                             |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.GetContactByExternalIDResponse](../../models/operations/getcontactbyexternalidresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 404, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Update

Update a contact by its external (custom) ID - the value you defined when creating the contact.

### Example Usage

<!-- UsageSnippet language="go" operationID="updateContactByExternalId" method="put" path="/contacts/external/{ext_id}" -->
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

    res, err := s.AddressBook.Contacts.ByExtID.Update(ctx, "my-id-2", components.Contact{
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
| `extID`                                                  | *string*                                                 | :heavy_check_mark:                                       | External (custom) ID of the contact to update.           | my-id-2                                                  |
| `contact`                                                | [components.Contact](../../models/components/contact.md) | :heavy_check_mark:                                       | A `Contact` object with the updated fields.              |                                                          |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.UpdateContactByExternalIDResponse](../../models/operations/updatecontactbyexternalidresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 404, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## Delete

Remove a contact from your account by its external (custom) ID - the value defined when the contact was created.

### Example Usage

<!-- UsageSnippet language="go" operationID="deleteContactByExternalId" method="delete" path="/contacts/external/{ext_id}" -->
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

    res, err := s.AddressBook.Contacts.ByExtID.Delete(ctx, "my-id-2")
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
| `extID`                                                  | *string*                                                 | :heavy_check_mark:                                       | External (custom) ID of the contact to remove.           | my-id-2                                                  |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.DeleteContactByExternalIDResponse](../../models/operations/deletecontactbyexternalidresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 400, 401, 403, 404, 4XX  | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## RemoveFromGroup

Remove a contact from a group in your Address Book using the contact’s external (custom) ID. This operation does not delete the contact; it only detaches the contact from the group. Provide the contact’s `ext_id` and the group’s `group_id` parameters to perform the detachment.

### Example Usage

<!-- UsageSnippet language="go" operationID="removeContactByExtIdToGroup" method="delete" path="/contacts/external/{ext_id}/group/{group_id}" -->
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

    res, err := s.AddressBook.Contacts.ByExtID.RemoveFromGroup(ctx, "my-id-1", 656)
    if err != nil {
        log.Fatal(err)
    }
    if res.ErrorResponse != nil {
        // handle response
    }
}
```

### Parameters

| Parameter                                                     | Type                                                          | Required                                                      | Description                                                   | Example                                                       |
| ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| `ctx`                                                         | [context.Context](https://pkg.go.dev/context#Context)         | :heavy_check_mark:                                            | The context to use for the request.                           |                                                               |
| `extID`                                                       | *string*                                                      | :heavy_check_mark:                                            | External (custom) ID of the contact to detach from the group. | my-id-1                                                       |
| `groupID`                                                     | *int64*                                                       | :heavy_check_mark:                                            | Group `id` to detach from the contact.                        | 656                                                           |
| `opts`                                                        | [][operations.Option](../../models/operations/option.md)      | :heavy_minus_sign:                                            | The options for this request.                                 |                                                               |

### Response

**[*operations.RemoveContactByExtIDToGroupResponse](../../models/operations/removecontactbyextidtogroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 404                      | application/json         |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |

## AddToGroup

Assign a contact to a group using the contact’s external (custom) ID (assigned when creating the contact). If a contact and a group exist in your account, you can add the contact to that group.

Provide the contact’s `ext_id` and the group’s `group_id` parameters to perform the assignment.

### Example Usage

<!-- UsageSnippet language="go" operationID="addContactByExtIdToGroup" method="patch" path="/contacts/external/{ext_id}/group/{group_id}" -->
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

    res, err := s.AddressBook.Contacts.ByExtID.AddToGroup(ctx, "my-id-1", 656)
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
| `extID`                                                  | *string*                                                 | :heavy_check_mark:                                       | External (custom) ID of the contact to add to the group. | my-id-1                                                  |
| `groupID`                                                | *int64*                                                  | :heavy_check_mark:                                       | Group `id` to associate with the contact.                | 656                                                      |
| `opts`                                                   | [][operations.Option](../../models/operations/option.md) | :heavy_minus_sign:                                       | The options for this request.                            |                                                          |

### Response

**[*operations.AddContactByExtIDToGroupResponse](../../models/operations/addcontactbyextidtogroupresponse.md), error**

### Errors

| Error Type               | Status Code              | Content Type             |
| ------------------------ | ------------------------ | ------------------------ |
| apierrors.ErrorResponse  | 404                      | application/json         |
| apierrors.ErrorResponse  | 400, 401, 403, 4XX       | application/problem+json |
| apierrors.ErrorResponse  | 5XX                      | application/problem+json |