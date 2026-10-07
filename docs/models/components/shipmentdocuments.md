# ShipmentDocuments

Document payload to print and enclose into shipment. For a single document, provide `DocumentPdf`, `DocumentLibrary`, or `DocumentMock` (for checking the price only). For multiple documents, provide an array of `DocumentPdf`, `DocumentLibrary`, or `DocumentMock` objects (1–20).


## Supported Types

### Documents

```go
shipmentDocuments := components.CreateShipmentDocumentsDocuments(components.Documents{/* values here */})
```

### 

```go
shipmentDocuments := components.CreateShipmentDocumentsArrayOfDocuments([]components.Documents{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch shipmentDocuments.Type {
	case components.ShipmentDocumentsTypeDocuments:
		// shipmentDocuments.Documents is populated
	case components.ShipmentDocumentsTypeArrayOfDocuments:
		// shipmentDocuments.ArrayOfDocuments is populated
}
```
