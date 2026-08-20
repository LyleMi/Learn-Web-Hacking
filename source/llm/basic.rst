Basic concepts
========================================

Introduction
----------------------------------------
Large model security refers to the protection of models, data, tools and business processes around large language models (LLM) and their application systems during training, deployment, calling, orchestration, operation and maintenance, etc., to prevent models from being induced to perform unexpected behaviors, leak sensitive information, make wrong decisions, or be used for attacks.

Unlike traditional web applications, the input of large model applications often includes instructions, data, and context at the same time. The model itself cannot naturally distinguish which content comes from the system, which comes from the user, and which comes from untrusted external data. Therefore, new attack surfaces such as prompt word injection, jailbreaking, tool abuse, and RAG pollution will be generated.

In actual systems, large models usually do not exist alone, but form an application with components such as vector databases, knowledge bases, plug-ins, agents, workflows, external APIs, file parsers, browsers, and code executors. Therefore, large model security includes not only the security of the model itself, but also traditional application security, data security, supply chain security and business security in the model application link.

Related concepts
----------------------------------------

large language model
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The big language model is a natural language processing model based on large-scale corpus training. It is often used in scenarios such as dialogue, summarization, translation, code generation, information extraction, and retrieval-enhanced question and answer.

prompt word
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Prompt is the input content submitted to the model. Prompt words can include task descriptions, context, examples, constraints, and user questions.

System prompt word
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
System prompts (System Prompt) are usually set by application developers and are used to constrain the role, capability boundaries, output formats and security policies of the model. After the system prompt word is leaked, the attacker can construct a more targeted bypass method accordingly.

context window
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The context window is the range of Tokens that the model can process in one inference. The larger the context window, the more information the model can process, while also potentially expanding the risk of injection, leakage, and resource consumption.

Retrieval enhancement generation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Retrieval-Augmented Generation (RAG) refers to retrieving relevant content from external sources such as knowledge bases, search engines, databases, etc., and then handing these content and user questions to the model to generate answers.

vector database
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Vector databases are used to store vector representations of text, images, codes and other data, and are often used in similarity retrieval, knowledge base Q&A and recommendation scenarios.

Agent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Agent is a large model application form with task planning, tool calling, state memory and multi-step execution capabilities. Agents can call tools such as browsers, emails, databases, command execution, work order systems, etc., so they usually have higher risks.

Tool call
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Tool Calling/Function Calling is the ability of the model to call external functions or APIs according to an agreed format. Tool calling expands the scope of influence of the model and requires permission control and parameter verification.
