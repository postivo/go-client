# ShipmentRecipients

Recipient data for a single shipment. For one recipient, provide a `RecipientInline`, `RecipientFromAddressBook`, or `RecipientFromAddressBookByExternalId` object. For multiple recipients, provide an array of these objects (1–50).


## Supported Types

### Recipients

```go
shipmentRecipients := components.CreateShipmentRecipientsRecipients(components.Recipients{/* values here */})
```

### 

```go
shipmentRecipients := components.CreateShipmentRecipientsArrayOfRecipients([]components.Recipients{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch shipmentRecipients.Type {
	case components.ShipmentRecipientsTypeRecipients:
		// shipmentRecipients.Recipients is populated
	case components.ShipmentRecipientsTypeArrayOfRecipients:
		// shipmentRecipients.ArrayOfRecipients is populated
}
```
