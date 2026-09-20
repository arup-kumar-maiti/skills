# Source Order

## File Order

Order a normal source file as follows, omitting sections that do not apply:

1. Required preamble: shebang, license, package, module, or namespace declaration.
2. File or module documentation.
3. Dependencies. Keep order-dependent dependencies in their required semantic order. Otherwise group standard library, external packages, project modules, and relative modules; alphabetize within each group.
4. Types, interfaces, schemas, enums, and data models.
5. Constants and immutable configuration.
6. Public classes, functions, and exported API.
7. Private or internal helpers.
8. Entrypoint function and startup code.

In a library module without startup code, put private helpers after their public callers. In an executable module, follow the language or repository convention when one exists. Otherwise, put its entrypoint function after the helpers required by its startup path and put the code that invokes it last.

## Constants and Types

Group constants by purpose, then order them by first use in the primary workflow. Keep values used together in their consumer's order; otherwise alphabetize unrelated constants by name.

Order type declarations as follows:

1. Primitive, opaque, or branded aliases and type parameters.
2. Interfaces, protocols, traits, and abstract contracts.
3. Enums, discriminated unions, and fixed-value sets.
4. Input, output, transport, and validation schemas.
5. Value objects and immutable data structures.
6. Persistent entities, records, and domain data models.
7. Abstract and base classes.

Within a category, put dependencies first. For unrelated declarations, alphabetize by name. For mutually recursive declarations, put public declarations before private ones, then alphabetize the remainder.

Put a base class before every derived class, even when that overrides the category order above.

## Operations and Classes

Apply these rules in order; stop at the first that distinguishes items:

1. Put prerequisites before consumers: base types before derived types, data types before consumers, and constants before users.
2. Put public operations in caller workflow order: create or configure, run, inspect, then close or delete.
3. Put a private helper after its primary caller. When one helper calls another, put the caller first.
4. In an executable module with one clear primary workflow, order private helpers by first use along its successful path. Put error-only helpers after them.
5. Alphabetize unrelated named peers.

Put an explicit public facade before the public services it coordinates.

For classes and equivalent types, follow the language or repository member-order convention when one exists. Otherwise use this member order when applicable:

1. Type-level constants and static configuration.
2. Constructors and lifecycle initialization.
3. Required protocol, interface, override, or language-magic members.
4. Alternate constructors, factories, and static methods.
5. Properties, getters, and setters.
6. Public methods in caller workflow order.
7. Private helpers in call order.

Keep an accessor near its related operation only when separating it would make the type harder to read.

Within a member category, preserve workflow and call order; otherwise alphabetize unrelated named members.

## Tests

1. Within each test, use arrange, act, then compare.
2. Order test cases by the public behavior they describe; otherwise alphabetize independent cases by description.
3. Keep fixtures and data builders near the tests that need them. Put test-only helpers after the tests unless a fixture depends on one. Alphabetize unrelated fixtures, data builders, and test-only helpers by name.
