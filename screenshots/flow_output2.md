# Details: Trace (4)

---

##### **FlowInputNode (Input node)**

**Output trace**

```json
{
  "fields": [
    {
      "content": {
        "document": "What is your return policy?"
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
  "timestamp": "2026-08-23T11:15:49.340Z"
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
        "document": "What is your return policy?"
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
  "timestamp": "2026-08-23T11:15:49.340Z"
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
            "text": "You are a customer support message classifier.\n\nClassify the customer's message into exactly ONE of these categories:\n\nBUG_REPORT\nPLATFORM_QUESTION\nOTHER_REQUEST\n\nRules:\n- BUG_REPORT: The customer is reporting a problem, error, malfunction, or unexpected behavior with the product/service.\n- PLATFORM_QUESTION: The customer is asking about the shop/platform, such as delivery, returns, refunds, orders, products, or other FAQ-related information.\n- OTHER_REQUEST: Anything that is not a bug report or a platform/FAQ question.\n\nReturn ONLY the category name.\nDo not add explanations, punctuation, or additional text.\n\nCustomer message:\nWhat is your return policy?"
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
            "text": "PLATFORM_QUESTION"
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
        "x-amzn-RequestId": "aa3c0891-ce61-4f37-b51e-8c94b6595d49",
        "AWS_REQUEST_ID": "aa3c0891-ce61-4f37-b51e-8c94b6595d49",
        "Content-Length": "220",
        "Date": "Sun, 23 Aug 2026 11:15:49 GMT",
        "Content-Type": "application/json"
      }
    },
    "metrics": {
      "latencyMs": 269
    },
    "usage": {
      "inputTokens": 144,
      "outputTokens": 6,
      "totalTokens": 150,
      "cacheDetails": []
    }
  },
  "requestId": "aa3c0891-ce61-4f37-b51e-8c94b6595d49",
  "serviceName": "bedrock",
  "timestamp": "2026-08-23T11:15:49.653Z"
}
```

**Output trace**

```json
{
  "fields": [
    {
      "content": {
        "document": "PLATFORM_QUESTION"
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
  "timestamp": "2026-08-23T11:15:49.653Z"
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
        "document": "PLATFORM_QUESTION"
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
  "timestamp": "2026-08-23T11:15:49.653Z"
}
```

**Condition trace**

```json
{
  "nodeName": "ConditionNode_1",
  "satisfiedConditions": [
    {
      "conditionName": "PlatformQuestion"
    }
  ],
  "timestamp": "2026-08-23T11:15:49.654Z"
}
```

---

##### **PlatformQuestionOutput (Output node)**

**Input trace**

```json
{
  "fields": [
    {
      "content": {
        "document": "PLATFORM_QUESTION"
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
  "nodeName": "PlatformQuestionOutput",
  "timestamp": "2026-08-23T11:15:49.654Z"
}
```
