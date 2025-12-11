# Common Type System (CTS)
**Category:** .NET Runtime Fundamentals  
**Status:** Stable  
**Purpose:** Define the unified type system used by all .NET languages.

---

## 1. Overview
The Common Type System (CTS) provides the standard rules governing how types are declared, used, stored, and interacted with inside the .NET runtime.  
It ensures:

- Cross-language interoperability (C#, F#, VB, others)
- Type safety & memory safety
- Unified object-oriented behavior
- High-performance execution across platforms

CTS is a foundational part of the CLR and is required for any .NET language targeting the runtime.

---

## 2. Two Fundamental Type Categories

### 2.1 Value Types
Value types store data **by value**.  
Assignments produce **copies**, not references.

Characteristics:
- Typically stored on the stack or inline
- Not garbage-collected (lifetime tied to scope)
- Efficient for small, immutable values
- Includes all built-in numeric types

Examples:
- `int`, `double`, `bool`, `char`
- `DateTime`, `Decimal`
- User-defined `struct`
- `enum`

---

### 2.2 Reference Types
Reference types store **references to objects** located on the heap.

Characteristics:
- Managed by the Garbage Collector
- Assignment copies the **reference**, not the object
- Support polymorphism and inheritance

Examples:
- `class`
- `interface`
- `delegate`
- Arrays
- `string`

---

## 3. Five CTS Type Kinds

### 3.1 Classes
Classes are the most complete reference types in .NET.

Key characteristics:
- Single inheritance (one base class)
- Implicitly inherit from `System.Object`
- Can implement any number of interfaces
- Support abstract, sealed, virtual, override, static members
- Support constructors, fields, methods, properties, events
- Can contain nested types

Classes model complex objects, domain entities, services, and behaviors.

---

### 3.2 Structures (struct)
Structures are **value types** used for lightweight, performance-focused data.

Characteristics:
- Implicitly inherit from `System.ValueType`
- Always sealed
- Cannot inherit from another struct or class
- Can implement interfaces
- No user-defined parameterless constructors
- Support methods, properties, and events

**Boxing & Unboxing**  
Value types are boxed into reference types when needed (e.g., passing to `object`).

---

### 3.3 Enumerations (enum)
A special value type derived from `System.Enum`.

Characteristics:
- Underlying type must be an integer (`byte`, `int`, `long`, etc.)
- Represents named constant values
- Cannot define methods or implement interfaces
- Often used for domain states and configuration flags

Supports both:
- Traditional enums  
- `[Flags]` enums (bitwise combinations)

---

### 3.4 Interfaces
Interfaces define contracts without implementation.

Characteristics:
- Contain signatures for methods, properties, and events
- No fields or constructors
- Types must implement all members
- Support multiple inheritance of interfaces

Interfaces are central to:
- Dependency injection  
- Loose coupling  
- Polymorphic design  

---

### 3.5 Delegates
Delegates are type-safe function pointers used for callbacks and events.

Characteristics:
- Reference types
- Represent static or instance methods
- Multicast-capable via invocation list
- Foundation for the .NET event model
- Inherit from `System.MulticastDelegate`

Delegates enable:
- Event handling
- Callback patterns
- Higher-order functions

---

## 4. Type Definitions

A type definition includes:

- Attributes
- Name and namespace
- Accessibility (public, internal)
- Base type
- Implemented interfaces
- Member definitions (fields, methods, properties, events)

Type names must be unique within their namespace and valid Unicode strings.

---

## 5. Accessibility Rules

| Modifier | Meaning |
|----------|---------|
| `public` | Accessible from any assembly |
| `internal` | Accessible only within the same assembly |

Nested types inherit constraints from their containing type.

Member accessibility may include:
- private  
- protected  
- protected internal  
- private protected  
- public  

---

## 6. Type Members

CTS defines several categories of members:

### Fields
Represent internal state.  
Often private or protected.

### Properties
Encapsulate field access (getter/setter).  
May include validation logic or computed values.

### Methods
Define behavior.  
Signature = method name + parameter types.

Support:
- Overloading  
- Virtual & override  
- async/await  

### Constructors
Initialize new instances.  
Structs cannot define parameterless constructors.

### Events
Provide publish/subscribe communication using delegates.

### Nested Types
Used for grouping tightly related internal types.

---

## 7. Member Characteristics

Common modifiers include:

- `abstract` → requires derived implementation  
- `virtual` → supports overriding  
- `override` → replaces base implementation  
- `static` → belongs to the type, not instance  
- `sealed` → prevents inheritance  
- `readonly` → assignable only during initialization  
- `const` → compile-time constant  
- `new` → hides base member  

---

## 8. Overloading, Overriding & Hiding

### Overloading
Same method name, different parameters.

### Overriding
Derived class replaces virtual method from base class.

### Hiding (`new`)
Redefines a member in the derived class that has the same signature as one in the base class.

---

## 9. Attributes
Attributes provide metadata and modify runtime or framework behavior.

Characteristics:
- Classes derived from `System.Attribute`
- Apply to types, members, assemblies, parameters
- Used in serialization, DI, validation, reflection, etc.

Examples:
- `[Obsolete]`
- `[Serializable]`
- `[Flags]`
- `[Required]` (ASP.NET Core)

---

## 10. Summary

CTS provides the unified type system that all .NET languages and runtimes rely on.  
It enables:

- A single, consistent programming model  
- Safety through strong typing and memory guarantees  
- High performance via value vs reference semantics  
- Cross-language compatibility  
- Rich OOP capabilities and modern abstractions  

CTS is one of the pillars of the .NET runtime architecture.

---

