## WSO2 AM Policies

Space to declare the policies which are used in WSO2 AM product to apply mediation into API request or response.

## Reference

### tranform_json_by_jsonpath
Transform the incoming JSON message into an outgoing JSON by JSON path.
- `jsonPath`: JSON Path to be used to convert the input JSON. It's complied with Jayway JSON Path

### json_field_to_postfix
This reads specific field from JSON body to create `REST_URL_POSTFIX` value of API.
- `jsonPath`: JSON path to the field to be read
- `postfixPattern`: The pattern in which contains static value `doc_id`. For instance, `/_doc/doc_id`. The portion `doc_id` of the pattern will be replace by the field read from above `jsonPath` paramter.

Examples JSON input:

```json
{
    "customerId" : "12345"
}
```

| `jsonPath` | `postfixPattern` | Generated Postfix |
|------------|------------------|-------------------|
| `$.customerId` | `/_doc/doc_id` | `/_doc/12345` 
| `$.customerId` | `/doc_id/read` | `/12345/read` 
