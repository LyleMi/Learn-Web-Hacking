Permission system design model
========================================

There are several common permission design patterns:

- Discretionary Access Control (DAC)
- Mandatory Access Control (MAC)
- Role-Based Access Control (RBAC)
- Attribute-Based Access Control, ABAC

Commonly used concepts are:

- User: The principal that initiated the operation
- Object: The object that initiates the operation, that is, the object of the operation
- Permission: Used to refer to a type of operation/class of operations on a certain object
- Access Control List (ACL): Data table describing the relationship between a user and permissions
- Access Control Matrix: An abstract and formal security model. This set of models describes the security protection status in a computer system, each representing the permissions it has for each appendix subbody under it.

DAC determines whether the user can operate on an object based on the information of the ACL. Users with permissions to a certain object can allocate the permissions of the object to other users, so this model is called Discretionary access control.

Since the DAC permission control is relatively scattered, each user and object has some permission identifiers, MAC was introduced. Each user and object has permission identification, and whether the user can operate depends on the permission identification relationship between the two parties. This method cannot be flexibly authorized and is suitable for scenarios with stricter permission control.

RBAC is by far the most popular permission design model, introducing the concept of role (Role).
Each user can associate one or more roles, and each role can also associate one or more permissions.
When new permission configuration is required, roles can be created flexibly according to requirements.

Unlike RBAC that is associated by role, ABAC is associated by attributes. Generally speaking, attributes are divided into several categories: user attributes, environment attributes (such as time), operation attributes (current operation), and object attributes. ABAC makes authorization judgment by dynamically calculating one or a set of attributes to meet the corresponding conditions.
