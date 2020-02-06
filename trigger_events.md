# Trigger Events

> Experimental API, please talk to us before using this

Trigger events are sent to the technicians apps of active jobs (job status "active" translates to "Termin läuft"). The are used to mark a single component as *triggered*, e.g. smoke detector has been triggered successfully.

## Checking for active jobs

Trigger events can only be created for active jobs of a specific installation. If you do not specifiy a job when sending events, the event is linked to the current active job. The current active job is the active job with *newest date* of the given installation.

You can check for active jobs before sending events with this request.

#### HTTP Request

`GET /trigger_events/active_job?installation_number=:installation_number`

| Query Parameter    | Description |
| ------------ | ----- |  
| `installation_number`|  The number of the installation you want to check for active jobs |

#### HTTP Response

API responds with the current active job and a list of other older but still active jobs.



```json
// Example response
{
    "active_job": {
      "job_id": "f2955438-f530-4613-8ef7-3cdeff8f9e10", 
      "job_number": "A-1002", 
      "job_label": "Wartungstermin 06.02.2020"
    },
    "alternatives": [
      {
        "job_id": "ccae6aeb-8853-4c0f-ba71-f95d9003f796", 
        "job_number": "A-1001",
        "job_label": "Wartungstermin 05.02.2020"
      }
    ]
}
```

If no active jobs are found, the API responds with `HTTP 404 (not found)` and body `"errors": "no active job found"`, `"errors": "installation not found"` or `"errors": "thing not found"`


## Sending trigger events

Trigger events have to be sent one event per request.


#### HTTP Request

`POST /trigger_events`

| Attribute    | Type |       |
| ------------- |:----:| -----|  
| `installation_number`  |  string | *optional, ignored if job_number is given*<br>Installation number | 
| `job_number`  |  string |  *optional*<br>Number of active job to link event to  | 
| `thing_number`       |  integer |  Number of affected thing | 
| `group_number`   |   integer | *optional*<br>Group number of thing, if thing is inside group | 
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
// Example payload with given installation number
// (API creates event for the current active job of INST-1)
{
    "event": {
      "installation_number": "INST-1",
      "thing_number": 1,
      "group_number": 5,
      "eventtype": "triggered",
      "eventdate": "2018-08-21T09:34:23.377Z"
    }
}
```
```json
// Example payload with given job number
// (API creates event for job A-123 if it is active)
{
    "event": {
      "job_number": "A-123",
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
      "id": "d011d838-9e76-4b5e-9cda-a14c4ff5b7fb",
      "job_id": "c90735b0-fcf3-47e0-8ffb-268a8ce0c131", 
      "job_number": "A-123", 
      "job_label": "Wartungstermin 06.02.2020"
    }
}
```

If no active job, no installation or no thing is found, the API responds with `HTTP 404 (not found)` and an error message as body. E.g. `"errors": "no active job found"`

