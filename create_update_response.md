# Create/Update Responses

Most endpoints allow to create or update multiple records by sending a list of objects within a `POST` request.

| Attribute    | Type |       |
| ------------- |:----:| -----|  
| `status` |  string |  `success` or `with_errors` | 
| `errors_count` |  int |  Error count. `0` if no errors | 
| `results` |   json |  Result per record | 
| `results` > `id` |   uuid |  Id of a single record if available | 
| `results` > `success` |   boolean |   Record has been saved | 
| `results` > `message`  |  string |  Error message. `null` if successful |


## Successful requests

If successful, the response returns a list of ids of the newly inserted or updated records.

Requests without errors have the `status` field set to `success` and `errors_count` = 0.


```json
// Example Response with 2 successful updates (HTTP 200)
{
    "status": "success",
    "errors_count": 0,
    "results": [
        {
            "id": "88e08d4b-b410-4afb-be50-6b980926ed70",
            "success": true,
            "message": null
        },
        {
            "id": "428d87f7-99a4-40b5-b337-7775b958c022",
            "success": true,
            "message": null
        }
    ]
}
```

## Requests with errors

If some or all records cannot be saved, the response returns a mixed list of ids of the newly inserted or updated records.

Requests with errors have the `status` field set to `with_errors` and `errors_count` > 0.

!> Responses with errors respond with HTTP status `200`, not with a HTTP error code. 

```json
// Example Response with one error (HTTP 200)
{
  "status": "with_errors",
  "errors_count": 1,
  "results": [
    {
      "id": null,
      "success": false,
      "message": "Customer no. is taken"
    },
    {
      "id": "4071d49e-bb5b-4647-85cd-2635fca6b00b",
      "success": true,
      "message": null
    }
  ]
}
```

