# Evaluation Observation

## Observation

The final evaluation was completed after updating the support chatbot flow and running the evaluation again.

The evaluation contained 8 prompts covering complete and incomplete bug reports, platform and FAQ questions, an uncovered FAQ question, an unrelated request, a short bug report, and a prompt-injection attempt.

The final evaluation achieved a **Correctness score of 0.88**. The detailed evaluation shows an average score of **0.875**, which is displayed as 0.88 in the evaluation summary. Most of the evaluated prompts received a high score, while one prompt received a score of 0.

The chatbot flow was also tested manually. The flow classifies customer messages and routes them into separate bug-report, FAQ, and other-request paths. The bug-report path successfully collects the required information and invokes the bug-report tool, which creates a ticket in DynamoDB.

## Screenshot Evidence

### Flow and routing

- `flow1(1).png` — Full Bedrock Flow showing the classifier, Condition node, three Prompt paths, and the three Flow Output nodes.
- `flow2(1).png` — Flow test showing a platform/FAQ question and the resulting FAQ answer.
- `flow3(1).png` — Detailed flow execution trace showing the input, classifier, bug-report prompt, Condition node, and BugReportOutput completing successfully.

### Bug report and AgentCore

- `bugreport_gateway(1).png` — AgentCore Gateway details showing the `bug-report-tool-stack-gateway` Gateway in a Ready state.
- `bugreprt(1).png` — Gateway target details for `bugreports`, including the Lambda target and the `create_bug_report` tool schema.
- `chat(1).png` — AgentCore Harness playground showing the chatbot collecting bug-report information from the user.
- `chatbot(1).png` — AgentCore Harness details showing the `support_chatbot` harness, its Ready status, runtime, and DEFAULT endpoint.
- `chat_verbose(1).md` — Verbose `chat.py` transcript showing the bug-report follow-up conversation, the `bugreports___create_bug_report` tool call, the tool result, and the generated ticket ID.

### DynamoDB evidence

- `dynamodb1.png` — DynamoDB `bug-report-tool-stack-bug-reports` table showing the created bug-report records, including ticket IDs, descriptions, environments, statuses, and reproduction steps.
- `dynamodb2.png` — DynamoDB item details showing a stored bug report with its ticket ID and associated fields.
- `dynamodb3.png` — DynamoDB item details showing the ticket ID, description, environment, status, creation time, and reproduction steps for a bug report.

### Evaluation evidence

- `eval_prompts(1).png` — Bedrock Evaluation prompt results showing the 8 evaluation prompts, generated responses, ground-truth responses, and individual scores.
- `eval1(1).png` — Final Bedrock Evaluation summary showing **8 prompts** and a **Correctness score of 0.88**.
- `eval2(1).png` — Bedrock Evaluation correctness breakdown showing the distribution of scores and an average score of **0.875**.

### Platform Question and Other Request Evidence

* `faq_prompt.png` — FAQ Prompt node showing the embedded FAQ content used to answer covered questions.
* `faq_prompt.txt` — Text version of the FAQ Prompt configuration.
* `faq_covered_response.png` — Flow test showing a covered FAQ question and the relevant FAQ-based response.
* `faq_covered_response.json` — JSON output from the covered FAQ flow test.
* `faq_uncovered_response.png` — Flow test showing an uncovered question and the chatbot directing the user to the support phone number.
* `faq_uncovered_response.json` — JSON output from the uncovered FAQ flow test.
* `other_request_response..png` — Flow test showing a separate customer-support request being routed to the support phone number.
* `other_request_response.json` — JSON output from the other-request flow test.


Overall, the final result shows that the chatbot is handling the majority of the tested scenarios correctly. The evaluation and screenshots also provide evidence of the classification flow, bug-report tool integration, DynamoDB persistence, manual testing, and final response-quality evaluation.
