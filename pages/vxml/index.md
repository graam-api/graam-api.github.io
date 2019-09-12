---
Title: Introduction to VoiceXML
---

## Introduction

VoiceXML is the HTML of the voice web, the open standard markup language for voice applications. [Learn more about Vxml](http://www.voicexml.org/tutorials-2/introduction/)

## How to use VoiceXML with Graam

Here is what you need to use VoiceXML with Graam

1. Setup a URL that return a Vxml document when called.
2. Create a Remote IVR as described [here](/pages/call-routing-app/remote-ivr)
3. Select a phone number from "My Number" page and route it to the newly created Remote IVR.

## Examples of VoiceXML scripts


### Example 1
Put the call into a queue with voicexml, you should use the custom object [callqueue](/pages/vxml/objects/callqueue)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<vxml autoanswer="false">
    <form>
        <object name="queue" classid="call_queue">
            <param name="queue_alias" value="standard"/>
            <param name="greeting_message" value="@test-welcome"/>
            <param name="waiting_music" value="@waiting_music"/>
            <param name="main_agent" value="agent1"/>
            <param name="main_agent" value="agent2"/>
            <param name="backup_agent" value="agent3"/>
        </object>
    </form>
</vxml>
```


### Example 2

Send call to a phone number. If the called number is not available, ask the caller if he would like to talk to an assistance or to hang up and get called back later.


