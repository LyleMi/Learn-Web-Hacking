Common risks
========================================

Prompt word injection
----------------------------------------
Prompt Injection means that the attacker affects the model's understanding and execution of original instructions by constructing input content, causing the model to ignore system constraints, leak context, call tools, or output content expected by the attacker.

Prompt word injection can be divided into direct injection and indirect injection. Direct injection comes from user input, and indirect injection comes from external data such as web pages, emails, documents, knowledge bases, and code warehouses. The risk of indirect injection is higher when the model reads untrusted content and continues the task.

prison Break
----------------------------------------
Jailbreak refers to bypassing the security policy of a model or application, causing the model to output content that should not be output. Jailbreaking usually uses role-playing, code conversion, multiple rounds of induction, rule conflicts, context overwriting, etc.

Prompt word leaked
----------------------------------------
Prompt word leakage means that system prompt words, developer prompt words, few-shot examples, internal rules, tool descriptions, link configurations and other information are output by the model to unauthorized users. The leakage of prompt words may not directly cause intrusion, but it will lower the threshold of attack.

Sensitive information leaked
----------------------------------------
Sensitive information leakage includes training data, logs, user input, knowledge base content, API keys, access tokens, personal information, business secrets, etc. being output by the model or recorded, forwarded, and exposed by downstream components.

Unsafe output handling
----------------------------------------
When the model output is directly handed over to downstream components such as browsers, SQL, Shell, template engines, code executors, CI/CD, and work order systems for processing, if there is a lack of verification and escaping, traditional vulnerabilities such as XSS, SQL injection, command execution, and template injection may occur.

over-agency
----------------------------------------
Excessive Agency means that the model is given too much autonomous decision-making and execution authority. For example, the model can automatically send emails, delete data, create orders, execute code, and modify permissions, but these operations do not require secondary confirmation, permission isolation, and auditing.

Model Denial of Service
----------------------------------------
Model denial of service refers to consuming tokens, computing power, storage, external API quotas or expense budgets through excessively long input, complex reasoning, multiple rounds of loops, recursive tool calls, and a large number of concurrent requests, resulting in service unavailability or abnormal costs.

Data poisoning
----------------------------------------
Data poisoning refers to an attacker contaminating training data, fine-tuning data, RAG knowledge base, vector index, feedback data or evaluation set, causing the model to output errors, biases, malicious content or content preset by the attacker under certain conditions.

model stealing
----------------------------------------
Model theft refers to obtaining model capabilities, parameters, training data characteristics or business logic through interface abuse, batch query, weight leakage, image leakage, debugging interface leakage, etc.

Model Supply Chain Risk
----------------------------------------
Large model applications rely on model weights, data sets, inference frameworks, plug-ins, prompt word templates, evaluation sets, embedding models, vector databases and third-party services. Once these links are contaminated or compromised, they may affect the final system behavior.

Attack surface analysis
----------------------------------------

Input side
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- User issues
- Multiple rounds of conversation history
- Upload files
- Web content
- Email content
- Knowledge base documentation
- Code repository content
- OCR/ASR recognition results
-External API return content

model side
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- base model
- Fine-tune the model
- Embed model
- Reorder model
- Content security model
- Model inference parameters
-Context splicing logic
- System prompt words

data side
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- training data
- Fine-tune data
- Evaluation data
- RAG Knowledge Base
- vector index
- User session
- Operation log
- Feedback data
- cache data

tool side
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Function Calling
- Plugins
- Browser
- Code interpreter
- Shell
- database
- file system
- Mail system
- Work order system
- Cloud API

Arrangement side
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Agent Planner
-Multi-Agent collaboration
- Workflow engine
- Task queue
- Memory module
- Authorization agent
- output parser
- Exception retry logic
