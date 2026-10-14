# StatusDetails

Details of a single shipment and its status events


## Fields

| Field                                                                    | Type                                                                     | Required                                                                 | Description                                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| `ShipmentDetails`                                                        | [components.ShipmentDetails](../../models/components/shipmentdetails.md) | :heavy_check_mark:                                                       | Single shipment details                                                  |
| `StatusEvents`                                                           | [][components.StatusEvent](../../models/components/statusevent.md)       | :heavy_check_mark:                                                       | List of status events for the shipment.                                  |