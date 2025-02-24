Tricks
========================================
- Is_numeric When there are spaces before and after, it will not be judged as true
- When comparing loosely, two different hashes starting with 0e will be judged to be equal
- Non-numeric string sequences and numeric comparisons will be automatically converted when compared loosely
- Functions such as strcmp/ereg will have unexpected behavior when the incoming parameter type is an array
