# Proposal Lifecycle and Guidelines

Guidelines for creating and managing design proposals across bowerbird projects.

---

## Proposal Lifecycle

### 1. Draft

New proposals start in `development/proposals/draft/`. These are under active development and review.

**Status:** `Draft`

**Characteristics:**
- Under active discussion
- May change significantly
- Not yet approved for implementation
- Can be abandoned without moving to rejected/

**Location:** `development/proposals/draft/`

### 2. Accepted

Once a proposal is reviewed, approved, and implemented, it moves to `development/proposals/accepted/`.

**Status:** `Accepted`

**Characteristics:**
- Reviewed and approved by maintainers
- Implementation complete and tested
- Serves as documentation of design decisions
- May be referenced by other proposals

**Location:** `development/proposals/accepted/`

**When to Move:**
- After successful implementation
- All tests passing
- Code review complete
- Documentation updated

### 3. Rejected

If a proposal is not accepted, it moves to `development/proposals/rejected/` with a rationale section explaining why.

**Status:** `Rejected`

**Characteristics:**
- Formally considered but not approved
- Includes rationale for rejection
- Preserved for historical context
- Can inform future proposals

**Location:** `development/proposals/rejected/`

**Common Rejection Reasons:**
- Doesn't align with project goals
- Technical constraints make it infeasible
- Better alternative approach identified
- Out of scope for the project

---

## Proposal Format

All proposals must include this header:

````markdown
```
Status:   Draft | Accepted | Rejected
Project:  <project-name>
Created:  YYYY-MM-DD
Author:   Name or Team
```

---
````

### Required Sections

#### 1. Summary
Brief overview of what the proposal addresses (2-3 sentences).

#### 2. Problem
Clear description of the problem being solved. Include:
- Current limitations or pain points
- Why this matters
- Who is affected

#### 3. Proposed Solution
Detailed description of the proposed approach. Include:
- Architecture or design overview
- Key components or changes
- How it addresses the problem

#### 4. Alternatives Considered
Other approaches that were evaluated and why they were not chosen.

#### 5. Trade-offs
Honest assessment of pros and cons:
- Benefits
- Costs or limitations
- Performance implications
- Maintenance implications

### Optional Sections

#### Examples
Code examples showing how the proposal would be used.

#### Implementation Plan
Steps for implementing the proposal (if relevant).

#### Testing Strategy
How the proposal will be tested.

#### Migration Path
For breaking changes, how users will migrate.

---

## Best Practices

### Writing Proposals

1. **Start with Why**
   - Clearly state the problem
   - Explain why it needs solving
   - Show who benefits

2. **Be Specific**
   - Use concrete examples
   - Include code snippets
   - Show before/after comparisons

3. **Consider Alternatives**
   - Show you've thought through options
   - Explain why your approach is best
   - Be honest about trade-offs

4. **Keep It Readable**
   - Use clear, simple language
   - Add diagrams where helpful
   - Break up long sections

5. **Update as You Learn**
   - Proposals evolve during implementation
   - Document what changed and why
   - Keep the proposal accurate

### Reviewing Proposals

1. **Check Completeness**
   - All required sections present
   - Problem clearly stated
   - Solution well-defined

2. **Evaluate Trade-offs**
   - Are costs worth the benefits?
   - Is complexity justified?
   - Are there hidden costs?

3. **Consider Maintainability**
   - How will this age?
   - Who will maintain it?
   - Is it well-documented?

4. **Think About Users**
   - Is it intuitive?
   - Does it break existing code?
   - Is migration path clear?

### Moving Proposals

**Draft → Accepted:**
1. Implementation complete and tested
2. Code review approved
3. Documentation updated
4. Update proposal status to "Accepted"
5. Add "Implemented: YYYY-MM-DD" to header
6. Move to `accepted/` directory
7. Update project's proposal index

**Draft → Rejected:**
1. Add "Rejection Rationale" section explaining why
2. Update proposal status to "Rejected"
3. Add "Rejected: YYYY-MM-DD" to header
4. Move to `rejected/` directory
5. Update project's proposal index

---

## Example Proposal

````markdown
```
Status:   Accepted
Project:  make-bowerbird-test
Created:  2026-01-08
Implemented: 2026-01-08
Author:   Bowerbird Team
```

---

## Summary

Introduce a mock shell framework for testing Make recipes without executing their commands.

## Problem

Testing Make recipes requires executing actual commands, which:
- Depends on external tools being installed
- Can have side effects (file system changes)
- Is slow for integration tests
- Makes tests flaky (network issues, etc.)

## Proposed Solution

Create a mock shell that captures commands instead of executing them:
- Override SHELL variable for specific targets
- Capture commands to a results file
- Compare captured commands against expected output

## Alternatives Considered

1. **External shell script**: Would work but has macOS Gatekeeper issues
2. **Inline shell string**: Chosen approach, avoids file quarantine

## Trade-offs

**Benefits:**
- Fast, deterministic tests
- No external dependencies
- Test recipe construction independently

**Costs:**
- Doesn't test actual command execution
- Requires careful escaping
- Mock shell string is complex

## Examples

```makefile
$(call bowerbird::test::add-mock-test,\
    test-mock-clean,\
    clean,\
    expected-clean,)
```

````

---

## Questions?

For project-specific proposal guidance, see the proposal index in each project's `development/proposals/INDEX.md` file.
