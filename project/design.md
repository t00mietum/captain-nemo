<!-- markdownlint-disable MD007 -- Unordered list indentation -->
<!-- markdownlint-disable MD010 -- No hard tabs -->
<!-- markdownlint-disable MD033 -- No inline html -->
<!-- markdownlint-disable MD055 -- Table pipe style [Expected: leading_and_trailing; Actual: leading_only; Missing trailing pipe] -->
<!-- markdownlint-disable MD041 -- First line in a file should be a top-level heading -->
# Design

Design, requirements, and direction. The active pre-v1.0.0 bug/feature task list lives in `backlog.md`.

## Assumptions

## Project structure

### Folder structure

Repo root stays clean, matching the nemo-anywhere layout: docs and license files plus a few top-level dirs.

- `source/` - the buildable project: a cargo workspace (`source/Cargo.toml`), with crates under `source/crates/`. Point cargo here.
	- `crates/captain-nemo/` - the application binary crate. Further crates get split out as real boundaries emerge, not up front.
- `project/` - design and backlog.
- `utility/` - standalone helper scripts.
- `.github/` - repo metadata only.

Toolchain and formatting are pinned in-tree: `source/rust-toolchain.toml` (stable channel) and `source/rustfmt.toml` (tabs). rustfmt output is canonical. Release profile builds for small-and-fast: fat LTO, one codegen unit, stripped.

### Logical code structure

### Data flow

### Execution flow/loops

## Direction decisions

## Plan

## Architecture

### Software stack

### Configuration model

### Saves and persistence

### UI

### Testing
