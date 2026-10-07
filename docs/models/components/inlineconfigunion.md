# InlineConfigUnion


## Supported Types

### InlineConfig

```go
inlineConfigUnion := components.CreateInlineConfigUnionInlineConfig(components.InlineConfig{/* values here */})
```

## Union Discrimination

Use the `Type` field to determine which variant is active, then access the corresponding field:

```go
switch inlineConfigUnion.Type {
	case components.InlineConfigUnionTypeInlineConfig:
		// inlineConfigUnion.InlineConfig is populated
}
```
