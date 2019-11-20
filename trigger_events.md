# Trigger Events

> Experimental API, please talk to us before using this

Trigger events are sent to the technicians apps of a running job. The are used to mark a single component as *triggered*, e.g. smoke detector has been triggered successfully.

## Sending trigger events

Trigger events have to be sent one event per request.


#### HTTP Request

`POST /trigger_events`

| Attribute    | Type |       |
| ------------- |:----:| -----|  
| `installation_number`  |  string |  Installation number | 
| `thing_number`       |  string |  Number of affected thing | 
| `group_number`   |   string | *optional*<br>Group number of thing, if thing is inside group | 
| `thing_serial_number`    |  string |  *optional*<br>You can use serial number as alternative to thing_number/group_number | 
| `eventtype`  | string |  For now only `triggered` event type is supported |
| `eventdate`  | timestamp |  Event date/time |

```bash
# Example request to create a trigger event
curl "https://api.foxtag.io/api/v1/public/trigger_events"
  -H "Content-Type: application/json"
  -H "Authorization: Bearer token=süpersecret"
  -X POST
  -d '(see json payload below)'

    Example JSON payload to create a trigger event
```
```json
// Example payload
{
    "event":
    {
      "installation_number": "A2",
      "thing_number": 1,
      "group_number": 5,
      "eventtype": "triggered",
      "eventdate": "2018-08-21T09:34:23.377Z"
    }
}
```

#### HTTP Response
```json
// Example response
{
    "status": "success",
    "event": {
        "id": "d011d838-9e76-4b5e-9cda-a14c4ff5b7fb"
    }
}
```

