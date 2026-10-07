# OptionsObj


## Supported Types

### ShipmentOptions

```go
optionsObj := components.CreateOptionsObjShipmentOptions(components.ShipmentOptions{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch optionsObj.Type {
	case components.OptionsObjTypeShipmentOptions:
		// optionsObj.ShipmentOptions is populated
}
```
