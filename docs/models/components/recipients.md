# Recipients

A base recipient object.


## Supported Types

### RecipientInline

```go
recipients := components.CreateRecipientsRecipientInline(components.RecipientInline{/* values here */})
```

### RecipientFromAddressBook

```go
recipients := components.CreateRecipientsRecipientFromAddressBook(components.RecipientFromAddressBook{/* values here */})
```

### RecipientFromAddressBookByExternalID

```go
recipients := components.CreateRecipientsRecipientFromAddressBookByExternalID(components.RecipientFromAddressBookByExternalID{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch recipients.Type {
	case components.RecipientsTypeRecipientInline:
		// recipients.RecipientInline is populated
	case components.RecipientsTypeRecipientFromAddressBook:
		// recipients.RecipientFromAddressBook is populated
	case components.RecipientsTypeRecipientFromAddressBookByExternalID:
		// recipients.RecipientFromAddressBookByExternalID is populated
}
```
