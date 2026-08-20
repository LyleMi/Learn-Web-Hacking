Security defense
========================================

Safe design
----------------------------------------

border demarcation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Large model applications require clear boundaries between system instructions, user input, external data, model output, and tool results. Untrusted content can only be processed as data and cannot be directly executed as instructions.

least privilege
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Models and agents should follow the principle of least privilege when calling tools. Different business scenarios should use different credentials, different authority scopes, and different network access policies to prevent one model session from having excessive operating capabilities.

Explicit authorization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Manual confirmation or secondary authorization should be added for high-risk operations, such as transfers, deletions, sending emails, modifying permissions, executing code, accessing sensitive data, etc. The confirmation content should include the operation object, scope of influence and key parameters.

Enter rating
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Classify input sources according to their credibility. Different cleaning, isolation and auditing strategies should be adopted for direct user input, internal corporate documents, Internet web pages, email attachments, third-party API return values, etc.

Output isolation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Model output should not go directly into the hazard interpreter. Output such as HTML, Markdown, SQL, Shell, Python, templates, JSON, YAML, etc. should be verified, escaped or sandboxed according to downstream semantics.

memory control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Long-term memory and session memory require restrictions on where writes come from, what is written, and what is read. Instructions from untrusted content should not enter long-term memory, and sensitive information should not be retained for long periods of time.

Observability
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Model requests, retrieval results, tool calls, permission decisions, blocking reasons, and user confirmation results should be logged. Logs need to be desensitized to avoid writing tokens, keys, personal information and business sensitive data into logs.

defense strategy
----------------------------------------

Prompt word protection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Clear distinction between instructions and data in the system prompt words
- Use quote blocks, tags or structured field wrapping for external content
- Reduce the exposure of sensitive rules and keys in prompt words
- Avoid implementing security policies only in prompt words
- Use independent safety decision logic for high-risk tasks

Input validation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Limit input length, file type and file size
- Parse sandbox isolation of uploaded files
- Perform format verification on URL, email, domain name, IP and other fields
- Add source identification to content from the Internet
- Security classification and de-righting of suspicious content

Output verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Use structured output Schema
- Whitelist verification of tool parameters
- Safe rendering of HTML/Markdown
- Manual validation or sandbox execution of code and command output
- Detect and desensitize sensitive information

Tool safety
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Define clear permission boundaries for tools
- Separate read-only tools and write operation tools
- Enable manual confirmation for high-risk tools
- Limit the networks, files and accounts the tool can access
- Audit and rate limit tool calls
- Mark tool return values ​​as untrusted data

RAG security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Control knowledge base writing permissions
- Checksum signature of document source
- Conduct security scans on incoming content
- Search results come with source and time information
- Limit the influence of a single document on the final answer
- Process hidden instructions, invisible characters, and obfuscated content
- Regularly rebuild indexes and clean up expired data

Agent security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Limit the maximum number of execution steps
- Limit the maximum number of tool calls
- Limit the budget of a single task
- Manual confirmation of external actions
- Use task-level temporary credentials
- Prohibit models from expanding their permissions on their own
- Audit plans and execution results

Model interface security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Authentication and authentication for interfaces
- Rate limit for users, tenants, models and scenarios
- Set token, concurrency, fee and time limits
- Circuit breaker for abnormal requests
- Change management of model versions and parameters
- Avoid exposing model keys on the client side

Data security
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Training and fine-tuning data should be hierarchically classified
- Sensitive data should be desensitized or minimized before entering the model
- Access control should be set for logs, caches, and vector indexes
- User data should be segregated by tenant
- There should be clear procedures for data deletion and model memory deletion
- Third-party model calls should evaluate data export and compliance requirements

security baseline
----------------------------------------
- Large model interfaces must have authentication, authorization and rate limiting
- Untrustworthy content must be marked with source and cannot be executed as system instructions
- Model output must be verified before entering downstream components
- High-risk tool calls must have access control and manual confirmation
- RAG knowledge base must control write permissions and document origin
- Agent must limit the number of execution steps, budget and permission scope
- Logs, caches, and vector libraries must be desensitized and access controlled
- Changes to models, prompts, tools, and knowledge bases must be auditable
- Red team testing and regression testing should be performed regularly
