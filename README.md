[![Go Reference](https://pkg.go.dev/badge/github.com/postivo/go-client.svg)](https://pkg.go.dev/github.com/postivo/go-client)
[![GitHub Release](https://img.shields.io/github/v/release/postivo/go-client)](https://github.com/postivo/go-client)
[![GitHub License](https://img.shields.io/github/license/postivo/go-client)](https://github.com/postivo/go-client/blob/main/LICENSE)
[![Static Badge](https://img.shields.io/badge/built_by-Speakeasy-yellow)](https://www.speakeasy.com/?utm_source=postivo&utm_campaign=go)
# POSTIVO.PL REST API Client SDK for Go

This package provides the **POSTIVO.PL Hybrid Mail Services SDK** for Go, allowing you to dispatch shipments directly from your application via the [POSTIVO.PL](https://postivo.pl) platform.

## Additional documentation:

Comprehensive documentation of all methods and types is available below in [Available Resources and Operations](#available-resources-and-operations).

You can also refer to the [REST API v1 documentation](https://api.postivo.pl/rest/v1/) for additional details about this SDK.

<!-- No Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [POSTIVO.PL REST API Client SDK for Go](#postivopl-rest-api-client-sdk-for-go)
  * [Additional documentation:](#additional-documentation)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Custom HTTP Client](#custom-http-client)
  * [Special Types](#special-types)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

To add the SDK as a dependency to your project:
```bash
go get github.com/postivo/go-client
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Sending Shipment to single recipient

This example demonstrates simple sending Shipment to a single recipient:

```go
package main

import (
	"context"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/models/components"
	"github.com/postivo/go-client/optionalnullable"
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
					Name:        postivo.Pointer("Jan Nowak"),
					Name2:       optionalnullable.From(postivo.Pointer("Firma testowa Sp. z o.o.")),
					Address:     postivo.Pointer("ul. Testowa"),
					HomeNumber:  optionalnullable.From(postivo.Pointer("23")),
					FlatNumber:  optionalnullable.From(postivo.Pointer("2")),
					PostCode:    postivo.Pointer("00-999"),
					City:        postivo.Pointer("Warszawa"),
					PhoneNumber: optionalnullable.From(postivo.Pointer("+48666666666")),
					Postscript:  optionalnullable.From(postivo.Pointer("Komunikat")),
					CustomID:    optionalnullable.From(postivo.Pointer("1234567890")),
				},
			),
		),
		Documents: components.CreateShipmentDocumentsArrayOfDocuments(
			[]components.Documents{
				components.CreateDocumentsDocumentPdf(
					components.DocumentPdf{
						FileStream: "<document_1 content encoded to base64>",
						FileName:   optionalnullable.From(postivo.Pointer("document1.pdf")),
					},
				),
				components.CreateDocumentsDocumentPdf(
					components.DocumentPdf{
						FileStream: "<document_2 content encoded to base64>",
						FileName:   optionalnullable.From(postivo.Pointer("document2.pdf")),
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

### Checking the price of a shipment for single recipient

This example demonstrates simple checking the price of a Shipment to a single recipient:

```go
package main

import (
	"context"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/models/components"
	"github.com/postivo/go-client/optionalnullable"
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
					Name:        postivo.Pointer("Jan Nowak"),
					Name2:       optionalnullable.From(postivo.Pointer("Firma testowa Sp. z o.o.")),
					Address:     postivo.Pointer("ul. Testowa"),
					HomeNumber:  optionalnullable.From(postivo.Pointer("23")),
					FlatNumber:  optionalnullable.From(postivo.Pointer("2")),
					PostCode:    postivo.Pointer("00-999"),
					City:        postivo.Pointer("Warszawa"),
					PhoneNumber: optionalnullable.From(postivo.Pointer("+48666666666")),
					Postscript:  optionalnullable.From(postivo.Pointer("Komunikat")),
					CustomID:    optionalnullable.From(postivo.Pointer("1234567890")),
				},
			),
		),
		Documents: components.CreateShipmentDocumentsArrayOfDocuments(
			[]components.Documents{
				components.CreateDocumentsDocumentPdf(
					components.DocumentPdf{
						FileStream: "<document_1 content encoded to base64>",
						FileName:   optionalnullable.From(postivo.Pointer("document1.pdf")),
					},
				),
				components.CreateDocumentsDocumentPdf(
					components.DocumentPdf{
						FileStream: "<document_2 content encoded to base64>",
						FileName:   optionalnullable.From(postivo.Pointer("document2.pdf")),
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
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name     | Type | Scheme      | Environment Variable |
| -------- | ---- | ----------- | -------------------- |
| `Bearer` | http | HTTP Bearer | `CLIENT_BEARER`      |

You can configure it using the `WithSecurity` option when initializing the SDK client instance. For example:
```go
package main

import (
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
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Accounts](docs/sdks/accounts/README.md)

* [Get](docs/sdks/accounts/README.md#get) - Retrieve account details
* [GetSubaccount](docs/sdks/accounts/README.md#getsubaccount) - Get subaccount details

#### [AddressBook.Contacts](docs/sdks/contacts/README.md)

* [List](docs/sdks/contacts/README.md#list) - List contacts
* [Add](docs/sdks/contacts/README.md#add) - Add a new contact
* [Get](docs/sdks/contacts/README.md#get) - Retrieve contact details
* [Update](docs/sdks/contacts/README.md#update) - Update a contact
* [Delete](docs/sdks/contacts/README.md#delete) - Delete a contact
* [RemoveFromGroup](docs/sdks/contacts/README.md#removefromgroup) - Remove a contact from a group
* [AddToGroup](docs/sdks/contacts/README.md#addtogroup) - Add a contact to a group

#### [AddressBook.Contacts.ByExtID](docs/sdks/byextid/README.md)

* [Get](docs/sdks/byextid/README.md#get) - Retrieve contact details by EXT_ID
* [Update](docs/sdks/byextid/README.md#update) - Update a contact by EXT_ID
* [Delete](docs/sdks/byextid/README.md#delete) - Delete a contact by EXT_ID
* [RemoveFromGroup](docs/sdks/byextid/README.md#removefromgroup) - Remove a contact from a group by EXT_ID
* [AddToGroup](docs/sdks/byextid/README.md#addtogroup) - Add a contact to a group by EXT_ID

#### [AddressBook.Groups](docs/sdks/groups/README.md)

* [List](docs/sdks/groups/README.md#list) - List groups
* [Add](docs/sdks/groups/README.md#add) - Add a new group
* [Get](docs/sdks/groups/README.md#get) - Retrieve group details
* [Update](docs/sdks/groups/README.md#update) - Update a group
* [Delete](docs/sdks/groups/README.md#delete) - Delete a group

### [Common](docs/sdks/common/README.md)

* [Ping](docs/sdks/common/README.md#ping) - Check API availability and version

### [Metadata](docs/sdks/metadata/README.md)

* [List](docs/sdks/metadata/README.md#list) - List metadata
* [GetPredefinedConfigs](docs/sdks/metadata/README.md#getpredefinedconfigs) - List predefined configs

### [Senders](docs/sdks/senders/README.md)

* [List](docs/sdks/senders/README.md#list) - List senders
* [Add](docs/sdks/senders/README.md#add) - Add a new sender
* [Delete](docs/sdks/senders/README.md#delete) - Delete a sender
* [Verify](docs/sdks/senders/README.md#verify) - Verify sender

### [Shipments](docs/sdks/shipments/README.md)

* [Status](docs/sdks/shipments/README.md#status) - Retrieve shipment details with status events
* [Cancel](docs/sdks/shipments/README.md#cancel) - Cancel shipments
* [Dispatch](docs/sdks/shipments/README.md#dispatch) - Dispatch a new shipment
* [Documents](docs/sdks/shipments/README.md#documents) - Retrieve documents related to a shipment
* [Price](docs/sdks/shipments/README.md#price) - Check the shipment price

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a `retry.Config` object to the call by using the `WithRetries` option:
```go
package main

import (
	"context"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/retry"
	"log"
	"models/operations"
)

func main() {
	ctx := context.Background()

	s := postivo.New(
		postivo.WithSecurity("<YOUR API ACCESS TOKEN>"),
	)

	res, err := s.Accounts.Get(ctx, operations.WithRetries(
		retry.Config{
			Strategy: "backoff",
			Backoff: &retry.BackoffStrategy{
				InitialInterval: 1,
				MaxInterval:     50,
				Exponent:        1.1,
				MaxElapsedTime:  100,
			},
			RetryConnectionErrors: false,
		}))
	if err != nil {
		log.Fatal(err)
	}
	if res.AccountResponse != nil {
		// handle response
	}
}

```

If you'd like to override the default retry strategy for all operations that support retries, you can use the `WithRetryConfig` option at SDK initialization:
```go
package main

import (
	"context"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/retry"
	"log"
)

func main() {
	ctx := context.Background()

	s := postivo.New(
		postivo.WithRetryConfig(
			retry.Config{
				Strategy: "backoff",
				Backoff: &retry.BackoffStrategy{
					InitialInterval: 1,
					MaxInterval:     50,
					Exponent:        1.1,
					MaxElapsedTime:  100,
				},
				RetryConnectionErrors: false,
			}),
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
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

Handling errors in this SDK should largely match your expectations. All operations return a response object or an error, they will never return both.

By Default, an API error will return `apierrors.APIError`. When custom error responses are specified for an operation, the SDK may also return their associated error. You can refer to respective *Errors* tables in SDK docs for more details on possible error types for each operation.

For example, the `Get` function may return the following errors:

| Error Type              | Status Code   | Content Type             |
| ----------------------- | ------------- | ------------------------ |
| apierrors.ErrorResponse | 401, 403, 4XX | application/problem+json |
| apierrors.ErrorResponse | 5XX           | application/problem+json |

### Example

```go
package main

import (
	"context"
	"errors"
	postivo "github.com/postivo/go-client"
	"github.com/postivo/go-client/models/apierrors"
	"log"
)

func main() {
	ctx := context.Background()

	s := postivo.New(
		postivo.WithSecurity("<YOUR API ACCESS TOKEN>"),
	)

	res, err := s.Accounts.Get(ctx)
	if err != nil {

		var e *apierrors.ErrorResponse
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}

		var e *apierrors.ErrorResponse
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}

		var e *apierrors.APIError
		if errors.As(err, &e) {
			// handle error
			log.Fatal(e.Error())
		}
	}
}

```
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Name

You can override the default server globally using the `WithServer(server string)` option when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the names associated with the available servers:

| Name      | Server                                   | Description           |
| --------- | ---------------------------------------- | --------------------- |
| `prod`    | `https://api.postivo.pl/rest/v1`         | Production system     |
| `sandbox` | `https://api.postivo.pl/rest-sandbox/v1` | Test system (SANDBOX) |

#### Example

```go
package main

import (
	"context"
	postivo "github.com/postivo/go-client"
	"log"
)

func main() {
	ctx := context.Background()

	s := postivo.New(
		postivo.WithServer("sandbox"),
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

### Override Server URL Per-Client

The default server can also be overridden globally using the `WithServerURL(serverURL string)` option when initializing the SDK client instance. For example:
```go
package main

import (
	"context"
	postivo "github.com/postivo/go-client"
	"log"
)

func main() {
	ctx := context.Background()

	s := postivo.New(
		postivo.WithServerURL("https://api.postivo.pl/rest/v1"),
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
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Go SDK makes API calls that wrap an internal HTTP client. The requirements for the HTTP client are very simple. It must match this interface:

```go
type HTTPClient interface {
	Do(req *http.Request) (*http.Response, error)
}
```

The built-in `net/http` client satisfies this interface and a default client based on the built-in is provided by default. To replace this default with a client of your own, you can implement this interface yourself or provide your own client configured as desired. Here's a simple example, which adds a client with a 30 second timeout.

```go
import (
	"net/http"
	"time"

	"github.com/postivo/go-client"
)

var (
	httpClient = &http.Client{Timeout: 30 * time.Second}
	sdkClient  = postivo.New(postivo.WithClient(httpClient))
)
```

This can be a convenient way to configure timeouts, cookies, proxies, custom headers, and other low-level configuration.
<!-- End Custom HTTP Client [http-client] -->

<!-- Start Special Types [types] -->
## Special Types

This SDK defines the following custom types to assist with marshalling and unmarshalling data.

### Date

`types.Date` is a wrapper around time.Time that allows for JSON marshaling a date string formatted as "2006-01-02".

#### Usage

```go
d1 := types.NewDate(time.Now()) // returns *types.Date

d2 := types.DateFromTime(time.Now()) // returns types.Date

d3, err := types.NewDateFromString("2019-01-01") // returns *types.Date, error

d4, err := types.DateFromString("2019-01-01") // returns types.Date, error

d5 := types.MustNewDateFromString("2019-01-01") // returns *types.Date and panics on error

d6 := types.MustDateFromString("2019-01-01") // returns types.Date and panics on error
```
<!-- End Special Types [types] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=postivo&utm_campaign=go)
