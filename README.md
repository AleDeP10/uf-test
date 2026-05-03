# uf-test

> Union-Find based Java testing library. Define equivalence partitions over your input domain, draw random samples from them, and get human-readable diagnostics when tests fail. Integrates with jqwik as a custom Arbitrary.

---

## The problem

Property-based testing tools like jqwik are excellent at *finding* counterexamples. They are less helpful at *explaining* them. When a randomly generated input causes a failure, you know *what* broke — but not *why* that value ended up there, which equivalence class it belongs to, or what boundary it crossed.

uf-test fills that gap.

---

## The idea

Every function under test partitions its input domain into equivalence classes: groups of values that all produce the same observable outcome. uf-test lets you declare those classes explicitly using a Union-Find structure, draw random samples from them in a controlled way, and — when something fails — navigate backwards through the partition graph to understand the failure in context.

```
Make-Set  →  each input value starts as its own singleton partition
Union     →  group values you know are functionally equivalent
Find      →  given any value, retrieve its class representative
Sample    →  draw a random element from a named partition
Diagnose  →  given a failure, trace back to the partition and its history
```

---

## Key features

- **Partition-aware generation** — samples are always drawn from a declared equivalence class, never blindly random
- **Bidirectional graph** — navigate from any element to its representative *and* from any representative to all its members
- **Human-readable diagnostics** — failure reports describe which partition was involved and how it was built, not raw data dumps
- **Fail-fast misconfiguration** — if your partitions are incomplete or overlapping, uf-test throws at setup time, not at test time
- **jqwik integration** — plugs in as a custom `Arbitrary`; no new runner, no new annotations required
- **Generic types** — works with any Java type; register a custom equivalence predicate in fewer than 5 lines

---

## How it compares to jqwik

| | jqwik | uf-test |
|---|---|---|
| Random input generation | ✅ | ✅ (partition-constrained) |
| Shrinking | ✅ | — |
| Equivalence class declaration | — | ✅ |
| Post-failure diagnostics | minimal | ✅ human-readable |
| Partition history / graph traversal | — | ✅ |
| Works standalone | ✅ | integrates with jqwik |

uf-test is not a replacement for jqwik. It is a diagnostic and structural layer on top of it — in the same spirit that AssertJ extends JUnit 5 without replacing it.

---

## Status

🚧 Early development — Milestone 1 in progress.

This is a research and development project. The API is unstable. Contributions and feedback are welcome.

---

## Requirements

- Java 21+
- Maven 3.8+
- JUnit 5
- jqwik (optional, for `Arbitrary` integration)

---

## License

MIT
