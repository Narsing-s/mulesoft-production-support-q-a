# Slide 05 — DataWeave: Clear Interview Explanations

## Q41. What is DataWeave?
**Answer:** DataWeave is MuleSoft's transformation language. It transforms JSON, XML, CSV, Java objects and other data representations.

**Production perspective:** I use it for mapping, filtering, grouping, conditional logic, normalization, validation and preparing payloads for downstream systems.

## Q42. Explain map vs mapObject.
**Answer:** `map` transforms elements of an array. `mapObject` transforms key-value pairs of an object.

```dw
payload.customers map (c) -> {
  id: c.id,
  name: c.name
}
```

For an object:

```dw
payload mapObject (value, key) -> {
  (key): value
}
```

## Q43. What is filter?
**Answer:** Filter returns only array elements satisfying a condition.

```dw
payload filter ((item) -> item.status == "ACTIVE")
```

Filtering early can reduce unnecessary downstream processing.

## Q44. What is filterObject?
**Answer:** filterObject is used when the input is an object and we need to retain only selected key-value pairs. It is useful when transforming dynamic object structures.

## Q45. What is reduce?
**Answer:** reduce processes collection elements and accumulates them into one result. It can be used for totals and custom aggregation.

**Production advice:** If a simpler built-in function expresses the requirement clearly, I prefer it for maintainability.

## Q46. How do you handle null or missing fields?
**Answer:** I distinguish between an absent field and an explicit null. I use safe navigation/defaulting where appropriate and validate mandatory fields before calling a downstream system.

For optional data, the transform should not fail unnecessarily. For mandatory data, I prefer a controlled validation error.

## Q47. How do you handle datatype issues?
**Answer:** I inspect the real input and expected schema. A field that previously arrived as a number may arrive as a string after a source-system change. I use explicit conversions and validation instead of relying on assumptions.

## Q48. How do you troubleshoot XML namespace errors?
**Answer:** I inspect the actual namespace URI in the payload. DataWeave selectors must reference the correct namespace. A visible XML prefix alone is not enough because prefixes can vary while the namespace URI identifies the vocabulary.

## Q49. How do you optimize a slow DataWeave transformation?
**Answer:** I inspect payload size, repeated traversal, nested loops, unnecessary fields, expensive expressions and large payload logging. I filter/select required data early and avoid recalculating the same expression.

## Q50. How do you troubleshoot a DataWeave error in production?
**Answer:** I capture the failing input shape, correlation ID, exact error line, expected schema and a successful example. Then I determine whether the cause is null data, datatype mismatch, missing field, namespace, malformed input or source schema change.

## Q51. Payload vs variables?
**Answer:** Payload represents the current event data. Variables store supporting state for later processors. I avoid keeping unnecessarily large objects in variables because they can increase memory usage.

## Q52. Why does streaming matter?
**Answer:** Streaming can allow large content to be processed without materializing the entire data set in memory, depending on the connector and operation. For large files I check whether the flow preserves streaming and avoid unnecessary full-payload operations.
