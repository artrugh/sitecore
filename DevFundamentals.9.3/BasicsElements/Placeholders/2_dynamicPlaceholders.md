## Dynamic Placeholders

Dynamic Placeholders allow to:
- add the same placeholder name several times, across multiple renderings.
- use the same placeholder multiple times in a single rendering.

Unique keys are guaranteed across different renderings and within one rendering.

When more than one placeholder appears, Sitecore will reassign the key with a unique placeholder key. 

```csharp
KeyValue_{GUID}_idx
```

| property | value |
| --- | --- |
| KeyValue | the same as the assigned in the key |
| GUID | unique ID |
| idx | index of the placeholder on the screen |

```csharp
@Html.Sitecore().DynamicPlaceholder("key-name");
```
