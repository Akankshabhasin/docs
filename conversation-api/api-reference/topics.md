---
id: topics
title: GET Topics
sidebar_label: GET Topics
slug: /conversation-api/get-topics
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

The most relevant topics of discussion from the conversation that are generated
based on the combination of the overall scope of the discussion.

This API returns all the topics generated from a conversation.

#### Sentiment Analysis in Topics <font color="orange"> BETA</font>

You can enable sentiment analysis over each topics which is being discussed in the conversation.
All you need to do is pass `sentiment=true` as a query parameter. [Read more about it](/docs/concepts/sentiment-analysis)

#### Topic Hierarchy in Topics<font color="orange"> BETA</font>

:::info
"parentRefs" doesn't support "sentiment" for now.
:::

You can enable topic hierarchy in Topics API by passing `parentRefs=true`. Topic Hierarchy breaks conversation
in parent and child topics which helps outline the entire conversation faster. Read more about it [here](/docs/concepts/topic-hierarchy)

#### Refreshing Topics

Topics can be generated again when you have new discussion items. Use `refresh=true` in the Topics API as a query param. This will delete the previous Topics and will create a new one.

### HTTP Request

`GET https://api.symbl.ai/v1/conversations/{conversationId}/topics`


### Example API Call

:::info
Before using the Conversation API you must get the authentication token (`AUTH_TOKEN`) from [our authentication process](/docs/developer-tools/authentication).
:::

<Tabs
  defaultValue="cURL"
  values={[
    { label: 'cURL', value: 'cURL', },
    { label: 'Node.js', value: 'nodejs', },
    { label: 'Python', value: 'python' }
  ]
}>
<TabItem value="cURL">

```shell
curl "https://api.symbl.ai/v1/conversations/$CONVERSATION_ID/topics" \
    -H "Authorization: Bearer $AUTH_TOKEN"
```

</TabItem>

<TabItem value="nodejs">

```js
const request = require('request');
const authToken = AUTH_TOKEN;
const conversationId = CONVERSATION_ID;

request.get({
    url: `https://api.symbl.ai/v1/conversations/${conversationId}/topics`,
    headers: { 'Authorization': `Bearer ${authToken}` },
    json: true
}, (err, response, body) => {
    console.log(body);
});
```

</TabItem>
<TabItem value="python">

```py
import json
import requests

baseUrl = "https://api.symbl.ai/v1/conversations/{conversationId}/topics"
conversationId = 'your_conversation_id'  # Generated using Submit text end point

url = baseUrl.format(conversationId=conversationId)

# set your access token here. See https://docs.symbl.ai/docs/developer-tools/authentication
access_token = 'your_access_token'

headers = {
    'Authorization': 'Bearer ' + access_token,
    'Content-Type': 'application/json'
}

params = {
    'sentiment': True,  # <Optional, boolean| Give you sentiment analysis on each topic in conversation.>
    'parentRefs': True,  # <Optional, boolean| Gives you topic hierarchy.>
}

responses = {
    401: 'Unauthorized. Please generate a new access token.',
    404: 'The conversation and/or it\'s metadata you asked could not be found, please check the input provided',
    500: 'Something went wrong! Please contact support@symbl.ai'
}

response = requests.request("GET", url, headers=headers, params=json.dumps(params))

if response.status_code == 200:
    # Successful API execution
    print("topics => " + str(response.json()['topics']))  # topics object containing topics id, text, type, score, messageIds, sentiment object, parentRefs
elif response.status_code in responses.keys():
    print(responses[response.status_code])  # Expected error occurred
else:
    print("Unexpected error occurred. Please contact support@symbl.ai" + ", Debug Message => " + str(response.text))

exit()
```

</TabItem>
</Tabs>


### Query Params
Parameter | Required | Value |Description|
--------- | --------- | ------- | -------
```sentiment```| No | true | Give you sentiment analysis on each topic in conversation.
```parentRefs```| No | true | Gives you topic hierarchy.




### Response
> Topic Hierarchy Sample Response (parentRefs=true):

```javascript
{
    "topics": [
        {
            "id": "5907389282779136",
            "text": "interns",
            "type": "topic",
            "score": 0.7178597920690242,
            "messageIds": [
                "4600982711304192",
                "5487363432120320",
                "6109794119188480"
            ],
            "parentRefs": [
                {
                    "type": "topic",
                    "text": "company-wise hiring"
                }
            ]
        },
        {
            "id": "5776859730018304",
            "text": "company-wise hiring",
            "type": "topic",
            "score": 0.788856914361565,
            "messageIds": [
                "6298570346987520",
                "6330577953226752"
            ],
            "parentRefs": []
        },
        {
            "id": "6697188878974976",
            "text": "new regulations",
            "type": "topic",
            "score": 0.6968750176932417,
            "messageIds": [
                "5356560840654848",
                "5663440783802368",
                "5263998490509312",
                "6082396449406976",
                "4925138187321344",
            ],
            "parentRefs": [
                {
                    "type": "topic",
                    "text": "company-wise hiring"
                }
            ]
        }
    ]
}
```

> Sentiment Sample Response (`sentiment=true`):

```javascript
{
    "topics": [
        {
            "id": "5907389282779136",
            "text": "interns",
            "type": "topic",
            "score": 0.7178597920690242,
            "messageIds": [
                "4600982711304192",
                "5487363432120320",
                "6109794119188480"
            ],
            "sentiment": {
                "polarity": {
                    "score": 0.389
                },
                "suggested": "positive"
            },
            "parentRefs": []
        },
        {
            "id": "5776859730018304",
            "text": "company-wise hiring",
            "type": "topic",
            "score": 0.788856914361565,
            "messageIds": [
                "6298570346987520",
                "6330577953226752"
            ],
            "sentiment": {
                "polarity": {
                    "score": 0.012
                },
                "suggested": "neutral"
            },
            "parentRefs": []
        },
        {
            "id": "6697188878974976",
            "text": "new regulations",
            "type": "topic",
            "score": 0.6968750176932417,
            "messageIds": [
                "5356560840654848",
                "5663440783802368",
                "5263998490509312",
                "6082396449406976",
                "4925138187321344",
            ],
            "sentiment": {
                "polarity": {
                    "score": -0.809
                },
                "suggested": "negative"
            },
            "parentRefs": []
        }
    ]
}
```

### Response Object

Field  | Description
---------- | ------- |
```id``` | Unique conversation identifier.
```text``` | Conversation text.
```type``` | Response type. Default is topics.
```score``` | Confidence score of the generated topic. value from 0 - 1.
```messageIds``` | Unique message identifiers of the corresponding messages.
```entities``` | List of detected entity objects in the insight with `type` - entity type and `text` - corresponding text.
```parentRefs``` | This is enabled when `parentRefs` is set to true in request.
```sentiment```| Shows the [sentiment](/docs/concepts/sentiment-analysis) polarity (the intensity of negativity or positivity of a sentence) and suggested sentiment type (positive, negative and neutral).
