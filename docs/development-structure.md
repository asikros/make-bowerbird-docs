# Development Directory Structure

Standard structure for the `development/` directory across all Bowerbird Make projects.

---

## Purpose

The `development/` directory serves as a central location for:
- Developer onboarding and reference material
- Design proposals and architectural decisions
- Project-specific development guidelines

## Standard Structure

All Bowerbird Make projects should follow this structure:

```
development/
├── proposals/          # Design documents and feature specifications
│   ├── draft/          # Proposals under active development
│   ├── accepted/       # Proposals that have been implemented
│   ├── rejected/       # Proposals that were not accepted (with rationale)
│   └── INDEX.md        # Index of all proposals
└── DEVELOPMENT.md      # Developer guide for the project
```

## File Descriptions

### DEVELOPMENT.md

The main developer guide for the project. Should include:

**Required Sections:**
- **Code Standards**: Links to [Make Style Guide](make-styleguide.md)
- **Development Workflows**: Links to relevant workflow docs (testing, proposals, etc.)
- **Key Principles**: Core development principles (testing, root cause analysis, etc.)
- **Quick Start**: Common commands for building, testing, and running the project
- **Directory Structure**: Visual representation of the development directory

**Optional Sections:**
- Project-specific setup instructions
- Common troubleshooting tips
- Links to external documentation

**Example Template:**

````markdown
# Developer Guide

Quick reference for contributing to [project-name].

## Code Standards

Follow the project's coding conventions:
- **[Make Style Guide](https://github.com/asikros/make-bowerbird-docs/blob/main/docs/make-styleguide.md)** - Naming conventions, documentation patterns, and formatting rules for Makefiles

## Development Workflows

- **[Testing Workflow](https://github.com/asikros/make-bowerbird-docs/blob/main/docs/testing-workflow.md)** - How to test changes, debug failures, and ensure test coverage

## Key Principles

1. **Test everything**: Run `make clean && make check` after any modifications
2. **Root cause failures**: Fix underlying issues, don't hack tests or code to pass
3. **Simple, direct tests**: Test failures should clearly indicate what's broken
4. **Add missing coverage**: If a bug wasn't caught, add a test for it

## Quick Start

```bash
# Run all tests
make check

# Clean build artifacts and run tests
make clean && make check

# Run a specific test
make test-<name>
```

---

## Directory Structure

```
development/
├── proposals/      # Design documents and feature specifications
│   ├── draft/      # Proposals under active development
│   ├── accepted/   # Proposals accepted and implemented
│   ├── rejected/   # Proposals that were rejected (with rationale)
│   └── INDEX.md    # Index of all proposals
└── DEVELOPMENT.md  # This file
```

**Note**: Code standards and workflow documentation are centralized in the [make-bowerbird-docs](https://github.com/asikros/make-bowerbird-docs) repository.

## Proposals

See **[proposals/INDEX.md](proposals/INDEX.md)** for a list of all design documents.

For proposal lifecycle and format guidelines, see **[Proposal Guidelines](https://github.com/asikros/make-bowerbird-docs/blob/main/docs/proposals.md)** in make-bowerbird-docs.
````

### proposals/INDEX.md

Index of all proposals in the project. Should include:

**Required Content:**
- Link to [Proposal Guidelines](https://github.com/asikros/make-bowerbird-docs/blob/main/docs/proposals.md) in make-bowerbird-docs
- Section for each proposal status (Draft, Accepted, Rejected)
- List of proposals with brief descriptions

**Example Template:**

````markdown
# Proposals Index

Design documents and feature specifications for [project-name].

See **[Proposal Lifecycle and Guidelines](https://github.com/asikros/make-bowerbird-docs/blob/main/workflows/proposals.md)** in make-bowerbird-docs for how to create and manage proposals.

---

## Draft

Proposals under active development:

- [01-feature-name.md](draft/01-feature-name.md) - Brief description
- [02-another-feature.md](draft/02-another-feature.md) - Brief description

## Accepted

Proposals that have been reviewed, approved, and implemented:

- [01-implemented-feature.md](accepted/01-implemented-feature.md) - Brief description

## Rejected

_(Proposals move here if not accepted, with rationale)_
````

### proposals/ subdirectories

- **draft/**: Active proposals being discussed and refined
- **accepted/**: Implemented proposals serving as design documentation
- **rejected/**: Proposals that were considered but not implemented, with rejection rationale

## What NOT to Include

**Do not add these to the development/ directory:**

- ❌ **README.md** - Not needed; DEVELOPMENT.md serves as the entry point
- ❌ **Duplicate documentation** - Link to make-bowerbird-docs instead
- ❌ **Build artifacts** - Use `.make/` or `.build/` directories instead
- ❌ **Test fixtures** - Keep in `test/` directory alongside test files
- ❌ **Source code** - Belongs in `src/` directory
- ❌ **Scripts** - Use `bin/` or `scripts/` directory

## Rationale

### Why DEVELOPMENT.md instead of README.md?

1. **Clear Purpose**: `DEVELOPMENT.md` clearly indicates it's for developers
2. **Convention**: Many projects use `CONTRIBUTING.md` or `DEVELOPMENT.md` for developer docs
3. **Avoid Confusion**: `README.md` in subdirectories can be confusing (is it for the directory or the project?)
4. **Single Entry Point**: Top-level `README.md` is for users; `development/DEVELOPMENT.md` is for contributors

### Why Centralize Documentation?

1. **Single Source of Truth**: Style guides and workflows apply to all projects
2. **Consistency**: All projects follow the same standards
3. **Easier Updates**: Update once, applies everywhere
4. **Reduced Duplication**: No need to sync docs across multiple repos

### Why Include proposals/?

1. **Design History**: Track why decisions were made
2. **Context for Maintainers**: New maintainers can understand design rationale
3. **Reference for Future Work**: Rejected proposals can inform future decisions
4. **Living Documentation**: Proposals evolve with implementation

## Migration Guide

If your project has a different structure:

### Old Structure → New Structure

```
development/README.md          → development/DEVELOPMENT.md
development/proposals/         → (keep as-is)
docs/                          → (move to development/ or delete if duplicates make-bowerbird-docs)
CONTRIBUTING.md                → (merge into development/DEVELOPMENT.md)
```

### Steps

1. **Rename or create DEVELOPMENT.md**
   ```bash
   cd development/
   # If you have README.md, rename it
   git mv README.md DEVELOPMENT.md
   # Or create new from template above
   ```

2. **Update content**
   - Remove duplicate style guide content (link to make-bowerbird-docs)
   - Remove duplicate proposal guidelines (link to make-bowerbird-docs)
   - Add quick start commands
   - Add directory structure diagram

3. **Create proposals/INDEX.md if needed**
   ```bash
   # If proposals/ exists but no INDEX.md
   touch proposals/INDEX.md
   # Add content from template above
   ```

4. **Delete old files**
   ```bash
   # Remove any duplicate documentation
   git rm docs/coding-style.md  # if it duplicates make-styleguide.md
   git rm CONTRIBUTING.md       # if merged into DEVELOPMENT.md
   ```

## Examples

See these projects for reference implementations:

- [make-bowerbird-test/development/](https://github.com/asikros/make-bowerbird-test/tree/main/development)
- [make-bowerbird-deps/development/](https://github.com/asikros/make-bowerbird-deps/tree/main/development)
- [make-bowerbird-help/development/](https://github.com/asikros/make-bowerbird-help/tree/main/development)

---

## Summary

**Standard structure:**
```
development/
├── proposals/
│   ├── draft/
│   ├── accepted/
│   ├── rejected/
│   └── INDEX.md
└── DEVELOPMENT.md
```

**Key points:**
- ✅ Use `DEVELOPMENT.md` (not README.md)
- ✅ Link to make-bowerbird-docs for standards
- ✅ Keep proposals organized by status
- ✅ Include INDEX.md for proposals
- ❌ Don't duplicate documentation
- ❌ Don't include build artifacts or source code
