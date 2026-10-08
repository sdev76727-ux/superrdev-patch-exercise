# Patch notes

- Search bug: Reading the repository SQL showed that `AND` binds more tightly than `OR`, so description matches could bypass archive and status filters. Parenthesized the title/description alternatives in both SQL references.
- Paging/performance bug: The controller loaded every matching row, sliced in memory, and deliberately slept before querying. Replaced this with database paging and counting, deterministic tie ordering, and removed the delay.
- Input bug: Invalid pages or statuses could trigger bad results or exceptions. Added HTTP 400 validation and bounded page size to 100.
- UI request bug: Inspecting the hook showed old requests could finish after newer searches and errors stayed visible. Abort superseded requests, clear errors when fetching, and reset to page 1 when filters change.
- I did not add debounce or indexes, or change wildcard matching; those need workload/product decisions. Biggest remaining risk: leading-wildcard substring search will not scale well.
- Validation: Maven package, Vite production build, API smoke checks for filtering, paging and invalid inputs, and production dependency audit passed. AI-assisted review/patching used Copilot in VS Code; I reviewed the changes.

**Handwriting reminder:** Write the four bug explanations above by hand, photograph or scan them, and place the image files in this folder before submitting. This file is only a guide, not a substitute for handwritten evidence.
