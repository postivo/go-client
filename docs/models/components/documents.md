# Documents

A base document object.


## Supported Types

### DocumentPdf

```go
documents := components.CreateDocumentsDocumentPdf(components.DocumentPdf{/* values here */})
```

### DocumentLibrary

```go
documents := components.CreateDocumentsDocumentLibrary(components.DocumentLibrary{/* values here */})
```

### DocumentMock

```go
documents := components.CreateDocumentsDocumentMock(components.DocumentMock{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch documents.Type {
	case components.DocumentsTypeDocumentPdf:
		// documents.DocumentPdf is populated
	case components.DocumentsTypeDocumentLibrary:
		// documents.DocumentLibrary is populated
	case components.DocumentsTypeDocumentMock:
		// documents.DocumentMock is populated
}
```
