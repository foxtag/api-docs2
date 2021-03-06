# Installations

## The Installation object

| Attribute    | Type |       |
| ------------- |:----:| -----|  
| `id`          |  uuid |  Installation id, generated by foxtag | 
| `number`       |  string |  *optional*<br>Number of installation | 
| `name`   |   string |  *optional*<br>Name of installation | 
| `location_id`   |   uuid |  Id of related location |
| `installation_type_id`   |   uuid |  Id of Installation type |
| `installation_type_name`    |  string |  *readonly*<br>Name of Installation type for your convenience | 
| `updated_at`  | timestamp |  Last update of object |

## List all installations

This endpoint retrieves all installations. The response is paginated if more than 500 records exist (see [Pagination](/pagination_sorting.md) for details).

#### HTTP Request

`GET /installations`

```bash
# example request
curl "https://api.foxtag.io/api/v1/public/installations"
  -H "Authorization: Bearer token=süpersecret"
```
```json
// example response
{
  "installations": [
    {
      "id": "aa24f45b-61af-4d8c-a674-21c3fef3a2c3",
      "number": "A-1",
      "name": "",
      "location_id": "556dfe02-c287-4634-98e9-b9cc13d69e28",
      "installation_type_id": "06fc0d5d-5fd1-4766-8893-ed597ff36f0b",
      "installation_type_name": "Brandmeldeanlage",
      "updated_at": "2018-03-13T15:25:52.039Z"
    }
  ],
  "meta": {
    "current_page": 1,
    "total_pages": 1,
    "total_count": 1
  }
}
```

## Retrieve a specific installation

This endpoint retrieves a specific installation.

#### HTTP Request with Id

`GET /installations/:id`

| Parameter    | Description |
| ------------ | ----- |  
| `id`         |  The UUID of the installation to retrieve |

#### HTTP Request with installation number filter

`GET /installations/?number=:number`

| Query Parameter    | Description |
| ------------ | ----- |  
| `number`     |  The number of the installation to retrieve |

## Create or update installations

You can create or update multiple installations with a single request by posting a list of installation objects.

#### HTTP Request

`POST /installations`

| Attribute    | Type |       |
| ------------- |:----:| -----|   
|`id` | uuid |*optional*<br>Creates a new record if id is not given<br>Creates new record if given and id is not existing<br>Updates a record if given and id is already existing|
| `number`       |  string |  *optional*<br>Number of installation | 
| `name`   |   string |  *optional*<br>Name of installation | 
| `customer_id`       |  string |  *optional*<br>Related customer | 
| `shares_customer_address`   |   boolean |  `true` if address of customer is also address of installation | 
| `address_attributes` | json |*optional*<br>installation's address (see [Addresses](/objects/addresses.md)) | 

```bash
# Example request to insert/update installations
curl "https://api.foxtag.io/api/v1/public/installations"
  -H "Content-Type: application/json"
  -H "Authorization: Bearer token=süpersecret"
  -X POST
  -d '(see JSON payload below)'  
```
```json
// example JSON payload to insert/update installations
{
  "installations": [
    {
      "installation_type_id": "42561e18-79ed-4af7-9b5a-ef7d29c47d13",
      "location_id": "95ae51f5-d5e2-45b4-991a-2c15ba20913d",
      "number": "A-15"
    }
  ]
}
```
#### HTTP Response

API responds with a list of ids and/or error messages. Refer to [Create/Update Response](/create_update_response?id=createupdate-response) for details.

## Delete a single installation

#### HTTP Request

`DELETE /installations/:id`

| Parameter    | Description |
| ------------ | ----- |  
| `id`         |  The UUID of the installation to delete |   


!> The installation is scheduled for deletion. It may take a whiel until the installation and all contents are deleted. 

```bash
# Example request to delete a installation
curl "https://api.foxtag.io/api/v1/public/installations/49199fe8-a5ea-4065-8acb-8c9bd2199586"
  -H "Authorization: Bearer token=süpersecret"
  -X DELETE
```


