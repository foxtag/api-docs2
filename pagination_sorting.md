# Pagination and sorting

## Pagination

Requests that respond with a list of records are paginated having 500 records maximum per page.

You find your current page and the number of total pages in the meta section of the response.

If you don't specify a page, you automatically get page 1, simply add a page query parameter to your request to get other pages.

`GET /users?page=3`

| Attribute    | Type |       |
| ------------- |:----:| -----|
| `current_page`  | int  | Current page |
| `total_pages`   | int  | Total available pages |
| `total_count`   | int  | Total records |

```json
// Example meta info of a paginated response
{
  "meta": {
    "current_page": 1,
    "total_pages": 3,
    "total_count": 1063
  }
}
```

## Sort order

Lists of records are ordered by `updated_at` (timestamp of last update of record), with the latest updated record at the end of the list.