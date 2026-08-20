Inject classification
========================================

Introduction
----------------------------------------
SQL injection is a code injection technique used to attack data-driven applications.
In the application, if proper filtering is not done, malicious SQL statements may be inserted into the input fields and executed (such as dumping the database contents to the attacker).

Classification by skills
----------------------------------------
Based on the techniques used, SQL injection types can be divided into

- Blind bet
    - Boolean blind injection: the Boolean value after statement execution can only be inferred from the application return
    - Time blind injection: The application does not have a clear echo and can only use a specific time function to judge.
- Error injection: the application will display all or part of the error message
- Stack injection: Some applications can add ``;`` to execute multiple statements at once
- other

Categorize by how data is obtained
----------------------------------------
In addition, it can also be divided into three categories according to the way of obtaining data.

inband
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use Web applications to directly obtain data, such as error injection. This type of injection extracts data through the site's response or error feedback.

inference
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Infer data through some reflections on the Web, such as Boolean blind injection, which is our popular blind injection.
Infer data through other changes to the web application.

out of band (OOB)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Data is obtained through other transmission methods, such as DNS resolution protocol and email.
