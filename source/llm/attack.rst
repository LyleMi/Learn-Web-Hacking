Common attack methods
========================================

Direct prompt word injection
----------------------------------------
Attackers add additional instructions to user input to cause the model to ignore original rules, change the output format, leak context, or call tools that it should not call.

Indirect prompt word injection
----------------------------------------
Attackers hide malicious instructions in external data such as web pages, documents, emails, image OCR results, code comments, knowledge base content, etc. When the model reads these, it may mistake them for instructions that need to be executed.

context override
----------------------------------------
Through a large amount of text, repeated instructions, format camouflage, etc., the model pays more attention to the content provided by the attacker and ignores the original system constraints.

Rule conflict
----------------------------------------
Task descriptions that conflict with system rules, such as requiring the model to choose between security rules and business tasks, inducing the model to prioritize completing user tasks and violating security policies.

Output format hijacking
----------------------------------------
By controlling the model output format, downstream parsers can misjudge fields, execute wrong branches, or call wrong tools.

Tool parameter contamination
----------------------------------------
The induced model generates tool calls with dangerous parameters, such as deleting files, expanding query scope, accessing internal addresses, modifying permissions, sending data to external addresses, etc.

RAG contamination
----------------------------------------
The attacker contaminates the knowledge base or retrievable external content, causing the model to reference the contaminated data when answering, output wrong conclusions, sensitive information or hidden instructions.

Multiple rounds of induction
----------------------------------------
The attacker gradually establishes context in multiple rounds of dialogue and bypasses single-round detection by gradually relaxing constraints, splitting tasks, and role-playing.

Resource consumption
----------------------------------------
Model context, inference resources, tool call quotas, and expense budgets are consumed through methods such as ultra-long text, complex formats, recursive tasks, automatic retries, and batch concurrency.
