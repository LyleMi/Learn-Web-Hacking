Detection method
========================================

Prompt word injection test
----------------------------------------
- Test whether the model ignores system constraints
- Test whether the model will leak system prompt words
- Test whether instructions in external documents will be executed
- Test whether multiple rounds of dialogue can gradually bypass restrictions
- Test bypass capabilities under different languages, encodings, and format conversions

Tool call test
----------------------------------------
- Test whether the model calls unauthorized tools
- Test whether tool parameters can be contaminated
- Test unauthorized access to other user or tenant data
- Test whether high-risk operations require confirmation
- Test whether the injected instructions in the tool return value will affect subsequent steps

RAG test
----------------------------------------
- Test answer changes after knowledge base contamination
- Test whether similarity retrieval will recall malicious documents
- Test whether hidden text, comments, and metadata in the document will enter the context
- Test whether the model distinguishes between retrieved content and user instructions
- Test whether the source of the citation is authentic and traceable

Denial of service testing
----------------------------------------
- Test overlong input handling
- Test concurrent request handling
- Test recursive tasks and automatic retries
- Limit on the number of test tool calls
- Testing fees and Token budget control

Sensitive information testing
----------------------------------------
- Test whether sensitive information is recorded in the log
- Test whether the model outputs training samples, keys, tokens, and personal information
- Test whether there is data crosstalk between different tenants
- Test whether the export, cache, and debugging interfaces leak context
