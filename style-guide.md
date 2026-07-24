<!-- markdownlint-disable MD007 -- Unordered list indentation -->
<!-- markdownlint-disable MD010 -- No hard tabs -->
<!-- markdownlint-disable MD041 -- First line in a file should be a top-level heading -->
# Style guide

This is the canonical style guide for Captain Nemo. Agent and contributor docs point here; if another document disagrees with this one, this one wins.

The overriding principle: where a rule below conflicts with a well-established idiom of the language in use, the language idiom wins. Everything else is house style.

<!-- TOC ignore:true -->
## Table of contents

<!-- TOC -->

- [Naming](#naming)
- [Comments](#comments)
- [File headers, copyright, and license](#file-headers-copyright-and-license)
- [Rust](#rust)
	- [Errors](#errors)
	- [Ownership and borrowing](#ownership-and-borrowing)
	- [Control flow](#control-flow)
	- [Modeling with types](#modeling-with-types)
	- [Abstraction](#abstraction)
	- [API shape](#api-shape)
	- [Formatting and lints](#formatting-and-lints)
- [Markdown and prose](#markdown-and-prose)
- [Helper scripts](#helper-scripts)
- [Filenames](#filenames)

<!-- /TOC -->

## Naming

Names exist so a human can read them, and later find and change them.

- Use meaningful names. `upper_bound` beats `ub`. If a plain-text search for the name would drown in false hits or find nothing, the name is wrong.

- But don't overcorrect. Names don't need to be long or globally unique - just clear and findable.

- Single-letter names are fine where idiomatic: loop counters (`for i in ...`), and short-lived conventional locals.

- No cryptic abbreviations. Write the word out.

- Case and word-order follow the language's convention. In Rust that means `snake_case` items and locals, `CamelCase` types, `SCREAMING_SNAKE_CASE` consts - the compiler and clippy enforce this anyway.

## Comments

Comments explain why, not what. The code already says what.

- Terse, plain, human. No narration ("this function does X"), no restating the next line, no banner dividers.

- ASCII only: `->` not a unicode arrow, `-` not an em dash. Exception: `(C)` in copyright lines is written with the copyright sign.

- Language-standard comment syntax always wins over house style. Rust uses `//` and `///`.

- No decorative flowerboxing. The one standing exception is the full-width `#•••` section rule in bash scripts that already use it; match that existing style there, and only there.

## File headers, copyright, and license

- The project license is GPL-2.0-or-later (see `license.md`). Rust source carries no per-file license header; the license is declared once, in the workspace `Cargo.toml` and the repo license file.

- Standalone helper and utility scripts are usually MIT, independent of the project license. They carry the header format demonstrated in the sister project's `n8git_backup-and-publish`:

	~~~text
	##	Copyright © <year> <author>
	##	Licensed under The MIT License (MIT). Full text at:
	##		https://mit-license.org/
	##	SPDX-License-Identifier: MIT
	~~~

- Where a language has a strong header idiom (e.g. Rust's crate-level `//!` docs), that idiom wins over the house header format.

## Rust

### Errors

- Errors are values. Return `Result<T, E>` and propagate with `?`.

- No `panic!`, `unwrap()`, or `expect()` outside tests, examples, or provably unreachable cases. An unreachable case gets a comment justifying why.

- Library crates define error types with `thiserror`. Application code uses `anyhow`.

- One error strategy per crate, applied consistently.

### Ownership and borrowing

- Borrow first. Never `.clone()` to silence the borrow checker - restructure, borrow, or take references instead.

- A genuinely necessary clone gets a comment saying why.

- Avoid gratuitous `Rc<RefCell<...>>`. Shared mutability is a design smell until proven otherwise.

### Control flow

- Return early. Guard clauses keep the happy path at minimum indentation.

- `let-else` for "extract or bail": `let Some(x) = opt else { return ... };`

- `?` to propagate instead of nesting `match` or `if let`.

- No `else` after a `return`. Collapse nested `if let` with `let-else` or let-chains.

- Prefer flat combinators (`map`, `and_then`, `unwrap_or_else`) on `Option`/`Result` when they read cleanly; fall back to `match` for multi-arm logic.

- Iterators over manual loops while it stays readable. Break to a plain `for` loop when a chain would need more than about three combinators, or when the chain hurts clarity.

### Modeling with types

- Model mutually exclusive states with enums and exhaustive `match`, not boolean flags.

- No catch-all `_` arm unless truly needed - exhaustive matching is how the compiler tells you a new variant needs handling.

- Use the type system to make invalid states unrepresentable where it's cheap: newtypes, typestate.

### Abstraction

- Traits and generics for abstraction. `dyn` only for genuine heterogeneity.

- Composition, never inheritance-shaped designs.

- Derive rather than hand-roll: `Debug`, `Clone`, `PartialEq`, and friends. Every public type derives `Debug`.

### API shape

- Take `&str` over `String`, and slices over `Vec`, in arguments. Return owned types.

- Doc-comment every public item with `///`.

- Be consistent within and across files: same error strategy, same naming, same module layout throughout.

### Formatting and lints

- Format with rustfmt defaults - four spaces per indent, no overrides. Don't fight the formatter. Intentional hand-formatted data tables get `#[rustfmt::skip]`.

- Code must pass `clippy::pedantic`. It's wired in as a workspace lint (`[workspace.lints.clippy]` in `source/Cargo.toml`), so `cargo clippy` enforces it without extra flags.

## Markdown and prose

- Never hard-wrap. One paragraph or bullet is one physical line; the editor wraps it.

- Short sentences. Avoid run-ons that chain several ideas with joining punctuation. Nested bullets beat a long paragraph.

- Minimal bold, italics, and ALL-CAPS. Plain adjectives over dramatic ones.

- No unicode in prose; ASCII punctuation.

- Tabs for list nesting.

## Helper scripts

- Bash helpers follow the compact style demonstrated in the sister project's `cicd/` and `utility/` scripts: `##` comments, `#•••` full-width section rules, camelCase locals, minified helper functions where that's the established pattern.

- They must pass shellcheck; per-rule `disable` lines at the top of the script, each with a short justification, are the accepted mechanism.

- Bash files are named `*.bash` (executables in the sister lineage may omit the extension where already established).

## Filenames

Lower-case filenames throughout, except `README.md`.
