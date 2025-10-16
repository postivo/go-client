# MetadataResponse

Metadata response.


## Fields

| Field                                                                                      | Type                                                                                       | Required                                                                                   | Description                                                                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| `Carriers`                                                                                 | [][components.MetadataResponseCarrier](../../models/components/metadataresponsecarrier.md) | :heavy_minus_sign:                                                                         | List of carriers and their available services.                                             |
| `Papers`                                                                                   | [][components.Paper](../../models/components/paper.md)                                     | :heavy_minus_sign:                                                                         | Available paper types.                                                                     |
| `EnvelopeTemplates`                                                                        | [][components.EnvelopeTemplate](../../models/components/envelopetemplate.md)               | :heavy_minus_sign:                                                                         | Envelope template groups, each containing related templates.                               |
| `StatusCodes`                                                                              | [][components.StatusCode](../../models/components/statuscode.md)                           | :heavy_minus_sign:                                                                         | Available status codes.                                                                    |