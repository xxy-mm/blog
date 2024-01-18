# Reference Types

## difference

- whenever a variable of value type is used, you get an independent copy.
- but the value of a reference type is shared across all variables which refer to it.

## usage notes

- using carefully, can be modified through multiple different names of variables.

- always have to explicitly provide the data area where the type is stored.

## store location

- memory:
  - lifetime limited to an external function call.
  - allowed in all functions.
- storage:
  - lifetime limited to the lifetime of a contract.
  - allowed in internal and private functions.
- calldata:
  - lifetime limited to an external function call
  - will avoid copies
  - data cannot be modified
  - allowed in all functions

> local storage variable can only be assigned with a pointer referencing a storage object.

**Note**

- Assignments between `storage` and `memory`(or from `calldata`) always create an independent copy.
- Assignments from `memory` to `memory` only create references.
- Assignments from `storage` to a `local storage` variable also only assign a reference.
- All other assignments to `storage` always copy.