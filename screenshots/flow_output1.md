# Details: Trace (4)

**Request ID:** `0f7faeae-d2b0-47d1-9439-6d9f16db56a7`

---

##### **FlowInputNode (Input node)**

**Output trace**

```json
{
  "fields": [
    {
      "content": {
        "document": "hi"
      },
      "next": [
        {
          "inputFieldName": "input",
          "nodeName": "ClassifyCustomerMessage"
        }
      ],
      "nodeOutputName": "document",
      "type": "STRING"
    }
  ],
  "nodeName": "FlowInputNode",
  "timestamp": "2026-08-23T11:09:23.545Z"
}
```

---

##### **ClassifyCustomerMessage (Prompt node)**

**Input trace**

```json
{
  "fields": [
    {
      "content": {
        "document": "hi"
      },
      "nodeInputName": "input",
      "source": {
        "expression": "$.data",
        "nodeName": "FlowInputNode",
        "outputFieldName": "document"
      },
      "type": "STRING"
    }
  ],
  "nodeName": "ClassifyCustomerMessage",
  "timestamp": "2026-08-23T11:09:23.545Z"
}
```

**Action trace**

```json
{
  "nodeName": "ClassifyCustomerMessage",
  "operationName": "Converse",
  "operationRequest": {
    "requestMetadata": {},
    "promptVariables": {},
    "system": [],
    "additionalModelRequestFields": null,
    "modelId": "amazon.nova-pro-v1:0",
    "inferenceConfig": {
      "maxTokens": 512,
      "temperature": 0.699999988079071,
      "topP": 1,
      "stopSequences": []
    },
    "additionalModelResponseFieldPaths": [],
    "messages": [
      {
        "content": [
          {
            "type": "TEXT",
            "text": "You are a customer support message classifier.\n\nClassify the customer's message into exactly ONE of these categories:\n\nBUG_REPORT\nPLATFORM_QUESTION\nOTHER_REQUEST\n\nRules:\n- BUG_REPORT: The customer is reporting a problem, error, malfunction, or unexpected behavior with the product/service.\n- PLATFORM_QUESTION: The customer is asking about the shop/platform, such as delivery, returns, refunds, orders, products, or other FAQ-related information.\n- OTHER_REQUEST: Anything that is not a bug report or a platform/FAQ question.\n\nReturn ONLY the category name.\nDo not add explanations, punctuation, or additional text.\n\nCustomer message:\nhi"
          }
        ],
        "role": "user"
      }
    ]
  },
  "operationResponse": {
    "output": {
      "message": {
        "content": [
          {
            "type": "TEXT",
            "text": "OTHER_REQUEST"
          }
        ],
        "role": "assistant"
      },
      "type": "MESSAGE"
    },
    "stopReason": "end_turn",
    "sdkHttpResponse": {
      "statusText": "OK",
      "statusCode": 200,
      "successful": true
    },
    "responseMetadata": {
      "metadata": {
        "Connection": "keep-alive",
        "x-amzn-RequestId": "926392f1-da2d-407a-80d8-9dd69ee59019",
        "AWS_REQUEST_ID": "926392f1-da2d-407a-80d8-9dd69ee59019",
        "Content-Length": "216",
        "Date": "Sun, 23 Aug 2026 11:09:23 GMT",
        "Content-Type": "application/json"
      }
    },
    "metrics": {
      "latencyMs": 281
    },
    "usage": {
      "inputTokens": 139,
      "outputTokens": 4,
      "totalTokens": 143,
      "cacheDetails": []
    }
  },
  "requestId": "926392f1-da2d-407a-80d8-9dd69ee59019",
  "serviceName": "bedrock",
  "timestamp": "2026-08-23T11:09:23.861Z"
}
```

**Output trace**

```json
{
  "fields": [
    {
      "content": {
        "document": "OTHER_REQUEST"
      },
      "next": [
        {
          "inputFieldName": "document",
          "nodeName": "OtherRequestOutput"
        },
        {
          "inputFieldName": "document",
          "nodeName": "BugReportOutput"
        },
        {
          "inputFieldName": "document",
          "nodeName": "PlatformQuestionOutput"
        },
        {
          "inputFieldName": "category",
          "nodeName": "ConditionNode_1"
        }
      ],
      "nodeOutputName": "modelCompletion",
      "type": "STRING"
    }
  ],
  "nodeName": "ClassifyCustomerMessage",
  "timestamp": "2026-08-23T11:09:23.861Z"
}
```

---

##### **ConditionNode_1 (Condition node)**

**Input trace**

```json
{
  "fields": [
    {
      "content": {
        "document": "OTHER_REQUEST"
      },
      "nodeInputName": "category",
      "source": {
        "expression": "$.data",
        "nodeName": "ClassifyCustomerMessage",
        "outputFieldName": "modelCompletion"
      },
      "type": "STRING"
    }
  ],
  "nodeName": "ConditionNode_1",
  "timestamp": "2026-08-23T11:09:23.861Z"
}
```

**Condition trace**

```json
{
  "satisfiedConditions": [
    {
      "conditionName": "default"
    }
  ],
  "nodeName": "ConditionNode_1",
  "timestamp": "2026-08-23T11:09:23.861Z"
}
```

---

##### **OtherRequestOutput (Output node)**

**Input trace**

```json
{
  "fields": [
    {
      "content": {
        "document": "OTHER_REQUEST"
      },
      "nodeInputName": "document",
      "source": {
        "expression": "$.data",
        "nodeName": "ClassifyCustomerMessage",
        "outputFieldName": "modelCompletion"
      },
      "type": "STRING"
    }
  ],
  "nodeName": "OtherRequestOutput",
  "timestamp": "2026-08-23T11:09:23.862Z"
}
```
