# Evaluation Observation

The final evaluation was completed after making the required changes to the support chatbot and running the evaluation again.

The chatbot was tested with 8 different prompts covering bug reports, platform-related questions, unsupported requests, and a prompt-injection attempt. The evaluation included both complete and incomplete bug reports to check whether the chatbot could identify missing information before proceeding.

The screenshots also show that the chatbot flow is divided into different paths based on the type of customer request. Bug reports are sent through the bug-report path, platform questions are handled through the FAQ path, and other requests are handled separately.

The bug-report Gateway and its `bugreports` target are shown as **Ready**. The target is connected to the Lambda function used for creating bug reports. The chatbot harness and its `DEFAULT` endpoint are also shown as **Ready**.

During flow testing, a customer message about the website reloading when searching for a shoe was correctly treated as a bug report. The trace shows the input, classification, bug-report prompt, condition, and output nodes completing successfully.

The final Bedrock evaluation contained 8 prompts and produced a **Correctness score of 0.88**. The detailed results show an average score of **0.875**, which is displayed as 0.88 in the evaluation summary. Seven prompts received a high score, while one prompt received a score of 0.

Overall, the final result shows that the chatbot is correctly handling most of the tested scenarios and following the intended flow. The evaluation also highlights one case that can be improved further. The screenshots included with the submission provide evidence of the chatbot configuration, Gateway, flow testing, and final evaluation results.
