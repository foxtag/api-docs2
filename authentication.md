# Authentication

Foxtag uses API keys to allow access to the API.

We expect the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer token=süpersecret`

```bash
curl "https://api.foxtag.io/api/v1/public/users"
  -H "Authorization: Bearer token=süpersecret"
```

!> Make sure to replace **süpersecret** with your API key.

## How to get your API key?

You can manage API keys in the administration section of your foxtag web account.

![logo](/_images/admin_api_key.png)

> API Access is only supported in the Foxtag Pro plan