Injection classification
========================================

Introduction
----------------------------------------
SQL injection is a code injection technology used to attack data-driven applications.
In an application, if no proper filtering is done, a malicious SQL statement may be inserted into the input field and executed (for example, dumping the database content to the attacker).

Classified by skills
----------------------------------------
According to the techniques used, SQL injection types can be divided into

- Blind note
- Boolean blind note: Only infer the Boolean value after the statement is executed from the application return
- Time blind note: There is no clear echo in the application, and only specific time functions can be used to judge
- Error injection: The application will display all or part of the error message
- Stacking Injection: Some applications can add ``;`` to execute multiple statements at once
- other

Classify by how data is obtained
----------------------------------------
In addition, it can also be divided into 3 categories according to the method of obtaining data

inband
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use web applications to directly obtain data, such as error injection, which extracts data through site response or error feedback.

inference
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Data is inferred through some reflections of the web, such as Boolean blinds, which is our popular blinds.
Data is inferred through other changes to the web application.

out of band (OOB)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Data is obtained through other transmission methods, such as DNS resolution protocol and email.
