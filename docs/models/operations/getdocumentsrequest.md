# GetDocumentsRequest


## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              | Example                                                                  |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `ID`                                                                     | *string*                                                                 | :heavy_check_mark:                                                       | Single shipment ID assigned by the system when the shipment was created. | A0043456                                                                 |
| `Type`                                                                   | [operations.DocumentType](../../models/operations/documenttype.md)       | :heavy_check_mark:                                                       | Type of document/certificate to generate.                                | dispatch_cert                                                            |