---
id: python-sdk-reference
title: Python SDK Reference
sidebar_label: Python SDK Reference
slug: /python-sdk/python-sdk-reference
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

This page contains detailed descriptions of the class and objects supported by the Symbl Python SDK. 

- [Audio Class](#audio-class)
- [Video Class](#video-class)
- [Text Class](#text-class)
- [Conversation Object](#conversation-object)
- [Telephony Class](#telephony-class)



## Audio class
Symbl's Async APIs provide the functionality for processing audio recordings from files or public/signed URLs. The data processed for these conversations are available via the Conversation APIs once the APIs have completed the processing.

You can utilize different functions of Async APIs by directly utilizing `symbl.Audio`.

### process_file(file_path):
Returns conversation object.

Name | Required | Description
-----|------------ | --------
`file_path`| Mandatory | A valid path to a file.
`content_type` | Optional | Parameter defining the content_type of audio. Acceptable values are audio/wav, audio/mp3, audio/mpeg. Leave it blank if you're not sure about the content_type of file.
`wait`| Optional | This accepts a Boolean value and is by default `true`. Value False will execute the function `submit_audio` on a separate thread making it a non-blocking API call. This also has callback support.
`parameters`| Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/audio/post-audio/#query-params).


### process_url(url):
Returns conversation object.

Name | Required | Description
-----|------------ | --------
`url` | Mandatory | A valid url to a file hosted directly.
`wait` | Optional | Accepts a Boolean value, by default, set to `true`. Value False will execute the function `submit_video` on a separate thread making it a non-blocking API call (Has callback support).
`parameters` | Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/audio/post-audio-url#query-params).


### append_file(file_path):
Returns conversation object.

Name | Required | Description
-----|------------ | --------
`file_path`| Mandatory | A valid path to a file.
`conversation_id`| Mandatory | Unique identifiier of the previous conversation to which appending the current conversation.
`content_type`| Optional| Parameter defining the content_type of audio. Acceptable values are audio/wav, audio/mp3, audio/mpeg. Leave it blank if you're not sure about the `content_type` of file.
`wait`| Optional |  Accepts a Boolean value. By default set to `true`. Value False will execute the function `submit_audio` on a separate thread making it a non-blocking API call (Has callback support).
`parameters` | Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/audio/put-audio#query-params).


### append_url(url, conversation_id):
Returns conversation object.

Name | Required | Description
-----|------------ | --------
`url` | Mandatory |  A valid url to a file hosted directly. |
`conversation_id` | Mandatory | Unique `conversationId` of a previous conversation to which appending the current conversation.
`wait` | Optional | Accepts a Boolean value, By default `true`. Value False will execute the function `submit_video` on a separate thread making it a non-blocking API call (Has callback support).
`parameters` | Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/audio/put-audio-url#query-params).


## Video class
Symbl's Async APIs provide the functionality for processing video recordings from files or public/signed URLs. The data processed for these conversations are available via the Conversation APIs once the APIs have completed the processing.

You can utilize different functions of Async APIs by directly utilizing `symbl.Video`.

### process_file(file_path):
Returns conversation object.

Name | Required | Description
-----|------------ | --------
`file_path`| Mandatory | A valid path to a file.
`content_type` | Optional | Parameter defining the `content_type` of video. Acceptable values are `video/mp4`. Leave it blank if you're not sure about the `content_type` of file. 
`wait`| Optional | Accepts a Boolean value. By default set to `true`. Value False will execute the function `submit_video` on a separate thread making it a non-blocking API call (Has callback support).
`parameters` | Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/video/post-video#query-params).

### process_url(url):
Returns conversation object.

Name | Required | Description
-----|------------ | --------
`url`| Mandatory | A valid url to a file hosted directly.
`wait`| Optional | Accepts a Boolean. By default set to `true`. Value False will execute the function submit_video on a separate thread making it a non-blocking API call (Has callback support).
`parameters` | Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/video/post-video-url#query-params).


### append_file(file_path, conversation_id):

Returns conversation object.

Name | Required | Description
-----|------------ | --------
`file_path` | Mandatory | A valid path to a file.
`conversation_id` | Mandatory | Unique `conversationId` of a previous conversation to which appending the current conversation.
`content_type`| Optional | Parameter defining the `content_type` of video. Acceptable values are `video/mp4`. Leave it blank if you're not sure about the `content_type` of file.
`wait` | Optional | Accepts a Boolean value: `true` or `false`. By default set to `true`. Value False will execute the function `submit_video` on a separate thread making it a non-blocking API call (Has callback support).
`parameters` | Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/video/put-video#query-params).

### append_url(url, conversation_id):
Returns conversation object.

Name | Required | Description
-----|------------ | --------
`url` | Mandatory | A valid url to a file hosted directly.
`conversation_id` | Mandatory | Unique `conversationId` of a previous conversation to which appending the current conversation.
`wait` | Optional | Accepts a Boolean value: `true` or `false`. Value False will execute the function `submit_video` on a separate thread making it a non-blocking API call (Has callback support).
`parameters` | Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/video/put-video-url#query-params).


## Text class
Symbl's Async APIs provide the functionality for processing textual content from a conversation. The data processed for these conversations are available via the Conversation APIs once the APIs have completed the processing.

You can utilize different functions of Async APIs by directly utilizing symbl.Text.

### process(payload):

Returns conversation object.

Name | Required | Description
-----|------------ | --------
`payload` | Mandatory | Textual dictionary containing the conversation to be processed in textual form, See [Async API Documentation](/docs/async-api/overview/text/post-text/#code-example-1) for payload.
`wait` | Optional | Accepts a Boolean value: `true` or `false`. By default, it is set to `true`. Value False will execute the function submit_text on a separate thread making it a non-blocking API call (Has callback support).
`parameters`| Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/text/post-text#query-params).

### append(payload, conversation_id):
Returns conversation object.

Name | Required | Description
-----|------------ | --------
`payload` | Mandatory | Textual dictionary containing the conversation to be processed in textual form, See [docs](/docs/async-api/overview/text/post-text#code-example-1) for payload.
`conversation_id` | Mandatory | Unique `conversationId` of a previous conversation to which appending the current conversation.
`wait` | Optional | Accepts a Boolean value: `true` or `false`. By default, it is set to `true`. Value False will execute the function `submit_text` on a separate thread making it a non-blocking API call (Has callback support).
`parameters` | Optional | By default {}) Dictionary, Any parameter and it's value can be provided in the dictionary format. For getting a list of value check [here](/docs/async-api/overview/text/put-text#query-params).

## Conversation object
Conversation object is returned by Async API Text, Audio and Video classes. The conversation object is a shorthand for conversation API and can be utilized for fetching multiple insights.

### conversation.get_action_items():

Returns Action Items which are some specific outcomes recognized in the conversation that requires one or more people in the conversation to act in the future

### conversation.get_follow_ups():

Returns a category of action items with a connotation to follow-up a request or a task like sending an email or making a phone call or booking an appointment or setting up a meeting.

### conversation.get_members():

Returns a list of all the members in a conversation. A Member is referred to as a participant in the conversation that is uniquely identified as a speaker. Identifying different participants in the meetings can be done by implementing speaker separation.

### conversation.get_messages():

`parameters`:- (Optional) dictionary, takes a dictionary of parameters. For list of parameters accepted, click [here](/docs/conversation-api/messages#query-params).

Returns a list of messages (sentences spoken by speakers) in a conversation. You can use this for providing transcription for video conference, meeting or telephone call.

### conversation.get_questions():

Returns explicit question or request for information that comes up during the conversation, whether answered or not, is recognized as a question.

### conversation.get_topics():

`parameters`:- (Optional) dictionary, takes a dictionary of parameters. For list of parameters accepted, please click [here](/docs/conversation-api/get-topics#query-params).

Returns The most relevant topics of discussion from the conversation that is generated based on the combination of the overall scope of the discussion.

## Conversations class
The Conversation API provides a REST API interface for getting your processed Speech to Text data(also known as Transcripts) and conversational insights.

These APIs require a `conversationId`.

You can utilize different functions of Conversation APIs by directly utilizing `symbl.Conversations`.

### get_action_items(conversation_id):

Returns Action Items which are some specific outcomes recognized in the conversation that requires one or more people in the conversation to act in the future

### get_follow_ups(conversation_id):

Returns a category of action items with a connotation to follow-up a request or a task like sending an email or making a phone call or booking an appointment or setting up a meeting.

### get_members(conversation_id):

Returns a list of all the members in a conversation. A Member is referred to a participant in the conversation that is uniquely identified as a speaker. Identifying different participants in the meetings can be done by implementing speaker separation.

### get_messages(conversation_id):

`parameters`:- (Optional) dictionary, takes a dictionary of parameters. For list of parameters accepted, please click [here](/docs/conversation-api/messages#query-params).

Returns a list of messages (sentences spoken by speakers) in a conversation. You can use this for providing transcription for video conference, meeting or telephone call.

### get_questions(conversation_id):

Returns explicit question or request for information that comes up during the conversation, whether answered or not, is recognized as a question.

### get_topics(conversation_id):

`parameters`:- (Optional) dictionary, takes a dictionary of parameters. For list of parameters accepted, please click [here](/docs/conversation-api/get-topics#query-params).

Returns The most relevant topics of discussion from the conversation that is generated based on the combination of the overall scope of the discussion.

## Telephony class
Based on PSTN and SIP protocols, the Telephony API provides an interface for the developers to have Symbl bridge/join VoIP calls and get the results back in real-time as well. Optionally, the developer can also trigger an email at the end of the conversation containing the URL to view the transcription, insights and topics in a single page Web Application.

### start_pstn(phoneNumber, dtmf, actions, data):

Returns a connection object.

- `phoneNumber`: phoneNumber where symbl should call.

- `dtmf` : (Optional) dtmf sequence to entered by symbl to join the call.

- `actions` : (Optional) follows the following pattern.

```py
[{invokeOn: "stop", name: "sendSummaryEmail", parameters: {emails: ["email@example.com"]}}]
```
- `data`: (Optional) {session: {name: "sessionName"}}

For more details check documentation [here](/docs/telephony-api/api-reference#endpoint).


### start_sip(uri, audioConfig, actions, data):

Returns a connection object.

- `uri`: uri where symbl should connect.

- `audioConfig`: (Optional) audioConfigs of the SIP.

- `actions` : (Optional) follows the following pattern.

```py

[{invokeOn: "stop", name: "sendSummaryEmail", parameters: {emails: ["email@example.com"]}}]
data: (Optional) {session: {name: "sessionName"}}
```
For more details check documentation [here](/docs/telephony-api/api-reference#endpoint).

### stop(connectionId):

Only `connectionId` parameter is required. Other optional parameters can be added as defined in the [Telephony API Documentation](/telephony-api/api-reference#endpoint).

Return an updated connection object which will have the `conversationId` in the response.
