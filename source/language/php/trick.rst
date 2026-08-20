Tricks
========================================
- is_numeric will not be judged as true when there are spaces before and after it
- During loose comparison, two different hashes starting with 0e will be judged as equal.
- Non-numeric string sequences and numeric comparisons are automatically converted when comparing loosely
- Functions such as strcmp/ereg will have unexpected behavior when the input parameter type is an array.
