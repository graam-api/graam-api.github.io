---
Title: Graam Webhook
---

You can regsiter a URL to be called (POSTed) when a call starts or stops. To register a webhook, go to the page Settings / API Integration.

Example of a payload send to the webhook on call start

```JSON
{
   "call_id":"jon984y24etwn0ut3f3r9g87",
   "our_number":"33999999910",
   "client_number":"33999999911",
   "calling_user_alias":null,
   "calling_user_email":"abcd@domain.com",
   "is_outgoing":1,
   "start_time":"2020-03-05T14:17:42+01:00",
   "agent_answer_time":null,
   "hangup_time":null,
   "duration":null,
   "onhold_duration":0,
   "user_data":null,
   "session_data":{}
}
```


Example of a payload send to the webhook on call end

```JSON
{
	"call_id": "adf20ohg80ut349fns3", // Unique ID of the call
	"our_number": "33999999910", // Our phone number
	"client_number": "33999999911", // Client phone number
	"is_outgoing": 0, // 0: Inbound call. 1: Outbound call
	"start_time": "2016-11-03T18:39:40+01:00", // Call start time
	"agent_answer_time": "2016-11-03T18:39:54+01:00", // The moment the call is anwsered by the first agent
	"hangup_time": "2016-11-03T18:40:05+01:00", // Hangup time
	"duration": 12, // Total duration of the communication
	"onhold_duration": 0, // Total onhold time
	"user_data": null, // This value is not yet used
	"session_data": [{  // List of calls with different agents (more than 1 if there is a call transfer)
		"email": "agent1@domain.com",
		"connected_time": "2016-11-03T18:39:54+01:00", // Début de la communication avec l'agent
		"end_time": "2016-11-03T18:40:06+01:00", // Fin de la communication avec l'agent
		"duration": 12 // Durée de la communication avec l'agent
	}]
}
```
