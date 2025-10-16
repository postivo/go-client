<!-- Start SDK Example Usage [usage] -->
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