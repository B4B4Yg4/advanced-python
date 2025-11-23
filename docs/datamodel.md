# Data Model

## Objects, values and types

Objects are Python's abstraction for data.All data in a Python program is
represented by objects or by relations betweeen objects.

Every object has an identity, a type and a value. An object's identity never
changes once it has been created.  
`is` operator compares the identity of two objects, the `id` function returns
an integer representing its identity.  

In CPython, `id(x)` is the memory address where `x` is stored.  
Value of some objects can change. Objects whose value can change are said to be
mutable and others are immutable.  

Objects are never explicitly destroyed; however, when they become unreachable
they may be garbage-collected.  
Note that the use of the implementation’s tracing or debugging facilities may
keep objects alive that would normally be collectable. Also note that catching
an exception with a `try…except` statement may keep objects alive.  

For immutable types, operations that compute new values may actually return a
reference to any existing object with the same type and value, while for
mutable objects this is not allowed.  

## Standard Type Hierarchy

* None
* NotImplemented
* Ellipsis

### Sequences

* Mutable (List, Byte Arrays)
* Immutable (String, Tuples, Bytes)

### Set Types

* sets
* frozen sets

### Mappings

* Dictionary
