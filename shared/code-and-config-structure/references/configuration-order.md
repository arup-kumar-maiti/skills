# Configuration Order

Keep required headers, schemas, version declarations, and order-dependent entries in the order mandated by the owning tool. Do not reorder maps, lists, or document blocks whose order is consumed by a runtime, workflow engine, task runner, or deployment tool.

## Declarative Maps

Otherwise, order top-level sections as follows, omitting sections that do not apply:

1. Format, schema, or build-system declarations.
2. Project, application, or package identity and runtime metadata.
3. Required dependencies and inputs.
4. Optional dependency groups.
5. Packaging, build, or distribution configuration.
6. Tool-specific configuration, grouped by tool name.

Within a table, put identity before runtime requirements, requirements before optional capabilities, and shared tool settings before nested tool sections. Alphabetize unrelated keys, tables, and unordered lists. Preserve narrative, dependency, priority, and tool-mandated order.

## Ignore Patterns

Treat patterns as independent only after verifying they do not overlap or override one another. Otherwise preserve their existing relative order, including negated patterns beginning with `!`.

For verified independent patterns, separate these nonempty groups with blank lines:

1. Operating-system and editor artifacts.
2. Environment files and local credentials.
3. Language runtime and generated artifacts.
4. Tool caches, build output, and other generated project artifacts.

Within a group, put a general pattern before a more-specific pattern it subsumes; otherwise alphabetize. Do not add group comments solely to label an obvious group.
