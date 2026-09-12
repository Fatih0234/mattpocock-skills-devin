---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
triggers:
  - user
---

Implement the work described by the user in the spec or tickets.

Call the Skill tool with "mattpocock-skills:tdd" and build test-first where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, call the Skill tool with "mattpocock-skills:code-review" to review the work.

Commit your work to the current branch.
