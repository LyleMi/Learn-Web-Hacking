Permission system design model
========================================

Common permission design patterns include the following:

- Discretionary Access Control (DAC)
- Mandatory Access Control (MAC)
- Role-Based Access Control (RBAC)
- Attribute-Based Access Control (ABAC)

Commonly used concepts are:

- User: the subject who initiates the operation
- Object: The object that initiates the operation, that is, the object of the operation
- Permission: used to refer to a type/type of operation on an object
- Access Control List (ACL): a data table describing the relationship between users and permissions
- Access Control Matrix: A set of abstract and formal security models. This set of models describes the security protection status of a computer system, representing each subsidiary body under it and the permissions it has for each object in the system.

DAC determines whether a user can operate on an object based on ACL information. A user who has permissions on an object can assign the permissions on that object to other users, so this model is called discretionary access control.

Since DAC permission control is relatively decentralized and each user and object has some permission identification, MAC was introduced. Each user and object has a permission ID. Whether a user can operate depends on the permission ID relationship between the two parties. This method cannot provide flexible authorization and is suitable for scenarios with strict permission control.

RBAC is by far the most popular permission design model, and it introduces the concept of roles.
Each user can be associated with one or more roles, and each role can also be associated with one or more permissions.
When new permission configurations are required, roles can be flexibly created according to needs.

Unlike RBAC, which associates by role, ABAC associates by attribute. Generally speaking, attributes are divided into several categories: user attributes, environment attributes (such as time), operation attributes (current operation), and object attributes. ABAC performs authorization judgment by dynamically calculating one or a group of attributes to determine whether the corresponding conditions are met.
