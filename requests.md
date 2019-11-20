# Basic Requests

## Retrieving data

Most resources expose 3 types of HTTP routes:

- index route, e.g. `GET /users` to retrieve the complete list. [Results are paginated](/pagination_sorting.md) (500 records per page).
- index route with filters, e.g. `GET /users?number=U1` to retrieve some records
- route with ID, e.g. `GET /users/d412502b-3888-4bbb-8726-09ba5998fb89` to retrieve a single record

#### Example response with json payload

```json
// example response
{
  "users": [
    {
      "id": "e5ff453e-694a-4d67-a4f1-7d3eda135e96",             
      "email": "peter.parker@example.com",
      "firstname": "Peter",
      "lastname": "Parker",
      "roles": [
        "admin"
      ],
      "updated_at": "2018-02-28T14:05:20.706Z"
    }
  ],
  "meta": {
    "current_page": 1,
    "total_pages": 1,
    "total_count": 1
  }
}
```

## Creating or Updating records

Both creating and updating of records can be done via `POST` requests (upsert). The required JSON payload obviously varies from resource to resource, but the response is always formatted the same way.

See [Create/Update Response](/create_update_response.md) for details.

#### Limit of objects per upsert request

To avoid long running requests, creating or updating records is **limited to 100 objects per request**. If you send more objects in a single request, the API responds with HTTP `422` and the message "Too many elements in a single request".

```json
// Example response 'too many elements' (HTTP 422)
{
    "message": "Too many elements in a single request"
}
```

## Deleting records

Some resources allow to get deleted via http delete, e.g. `DELETE /locations/d412502b-3888-4bbb-8726-09ba5998fb89`

!> Deleting a single `installation` also deletes all of its contents: the whole inventory (things), all check events and reports.

