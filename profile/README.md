<p align="center"><img src="https://raw.githubusercontent.com/go-pcore/brand/main/social/go-pcore.png" alt="go-pcore" width="640"></p>

<h1 align="center">go-pcore</h1>
<p align="center"><strong>Puppet's Pcore type system in pure Go — the type calculus, parser, value model and assignability lattice, no cgo.</strong></p>

<p align="center">
  🌐 <a href="https://go-pcore.github.io">Website</a> ·
  📚 <a href="https://go-pcore.github.io/docs/">Documentation</a>
</p>

<p align="center">
  <a href="https://go-pcore.github.io/docs/"><img alt="Docs" src="https://img.shields.io/badge/docs-mkdocs--material-FBBF24?style=flat-square"></a>
  <a href="https://github.com/go-pcore/pcore/blob/main/LICENSE"><img alt="License: BSD-3-Clause" src="https://img.shields.io/badge/license-BSD--3--Clause-blue?style=flat-square"></a>
  <img alt="Go 1.26.4+" src="https://img.shields.io/badge/go-1.26.4%2B-00ADD8?style=flat-square&logo=go&logoColor=white">
  <img alt="Coverage 100%" src="https://img.shields.io/badge/coverage-100%25-1a7f37?style=flat-square">
</p>

---

**go-pcore** is a **pure-Go (no cgo) reimplementation of [Pcore](https://github.com/puppetlabs/puppet-specifications/blob/master/language/types_values_variables.md)**,
the data-type and value model that underpins **Puppet**, **Hiera** and
**Facter** values. It gives a Go program the Puppet type calculus — a type
model, a type **parser**, a value model, and the load-bearing operations
(instance-of, assignability, inference and rich-data serialization) — with names
and semantics that track Puppet's `Puppet::Pops::Types`, so it is a drop-in for
Puppet type expressions.

It is the foundational type layer for **go-puppet** (the Puppet DSL evaluator)
and for **go-ruby-puppet**, which marshals `rbgo.Value ↔ pcore.Value`.

## Repositories

| Repo | What it is |
|------|------------|
| [**pcore**](https://github.com/go-pcore/pcore) | the library: type model, `Parse`, value model, `IsInstance` / `IsAssignable` / `Infer` / `Generalize` / `CommonType`, and `ToData` / `FromData` |
| [**docs**](https://github.com/go-pcore/docs) | MkDocs Material documentation, versioned with [mike], served at [/docs/](https://go-pcore.github.io/docs/) |
| [**go-pcore.github.io**](https://github.com/go-pcore/go-pcore.github.io) | the Hugo landing page |
| [**brand**](https://github.com/go-pcore/brand) | logos and brand assets |

## Principles

- **Pure Go, zero cgo.** Cross-compiles and embeds anywhere; a static binary by
  default, green across the six 64-bit Go targets.
- **Faithful to Pcore.** Type names, the grammar, the assignability rules and the
  rich-data protocol track Puppet's specification.
- **Round-trippable.** Every `Type.String()` parses back through `Parse`.
- **100% test coverage** is the target, enforced as a CI gate.

## Status

**v0.2 — full Pcore type calculus.** The complete Puppet `Puppet::Pops::Types`
set is implemented: the type calculus (scalar, collection, abstract, plus
`Timestamp` / `Timespan` ranges, `Binary`, `SemVer` / `SemVerRange`, `Init`,
`Object`, `RichData`, `Runtime`, `URI`, `Iterable` / `Iterator`, `Error` and
`Callable`), a round-trippable type parser, the value model (with a redacting
`Sensitive`), `IsInstance` / `IsAssignable` / `Infer` / `Generalize` /
`CommonType` / `ToData` / `FromData`, and **recursive type aliases** and
**`TypeSet`** via a `Loader` type environment — at 100% coverage, `gofmt` +
`go vet` clean, CI green across amd64, arm64, riscv64, loong64, ppc64le and
s390x.

BSD-3-Clause.

[mike]: https://github.com/jimporter/mike
