# HTTP Response Codes


The Foxtag API uses the following response codes:

| Code | Meaning |
| -----| ------------ |
| **200**  | **OK** |
| 401  | Unauthorized -- Your API key is unknown or has been revoked. |
| 403  | Forbidden -- Access to a specific resource is not allowed to you. |
| 404  | Not Found -- The specified resource could not be found. |
| 422  | Unprocessable Entity -- Something is wrong with the payload you sent |
| 429  | Too Many Requests -- You're requesting too much data! Slow down! |
| 500  | Internal Server Error -- We had a problem with our server. Try again later. |
| 503  | Service Unavailable -- We're temporarily offline for maintenance. Please try again later. |

!> If you are creating or updating records, **HTTP 200 does not mean that all records have been successfully saved**. Don't forget to check the response for errors (see [Create/Update Response](/create_update_response?id=createupdate-response) for details).