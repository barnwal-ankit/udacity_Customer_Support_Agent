# Evaluation Observation

The final evaluation was completed after updating the support chatbot flow and running the evaluation again.

The evaluation used 8 test prompts covering complete and incomplete bug reports, platform/FAQ questions, an uncovered platform question, other requests, a short bug report, and a prompt-injection attempt.

## Observation

The final evaluation achieved a **Correctness score of 0.88**. The detailed evaluation results show an average score of **0.875**, which is displayed as 0.88 in the evaluation summary. Most of the test cases received high scores, while one case received a score of 0.

The chatbot flow was also tested manually after the changes. The flow correctly classifies customer messages and routes them to the appropriate path for bug reports, platform/FAQ questions, and other requests.

## Screenshot Evidence

The screenshots included in the `screenshots` folder provide the following evidence:

- **Flow diagram screenshot** — shows the complete Bedrock Flow, including the input node, classifier prompt, condition/routing node, the three separate paths, and their corresponding output nodes.

- **Classifier prompt screenshot** — shows the prompt used to classify the incoming customer message into the different request categories.

- **Condition node screenshot** — shows the routing conditions used to send the classified message to the appropriate path.

- **Bug report path screenshot** — shows the bug-report prompt and the flow being executed for a customer reporting a problem.

- **Bug report conversation/trace screenshot** — shows the chatbot collecting the required bug information before completing the bug-report process.

- **DynamoDB screenshot** — shows the `bug-report-tool-stack-bug-reports` table containing bug-report records created through the chatbot, including the ticket ID, description, reproduction steps, environment, status, and creation time.

- **Gateway screenshot** — shows the `bugreports` Gateway target in a ready state and the configured `create_bug_report` tool used by the chatbot.

- **FAQ prompt screenshot** — shows the FAQ content embedded in the FAQ prompt used for platform-related questions.

- **Covered FAQ test screenshot** — shows the chatbot answering a question that is covered by the FAQ.

- **Uncovered FAQ test screenshot** — shows the chatbot directing the customer to human support when the question is not covered by the available FAQ information.

- **Other-request test screenshot** — shows the separate path used for requests that do not belong to the bug-report or FAQ categories.

- **AgentCore harness screenshot** — shows the support chatbot harness and its available endpoint used for testing.

- **Evaluation results screenshot** — shows the completed Bedrock Evaluation job with 8 prompts and the final **0.88 Correctness score**.

