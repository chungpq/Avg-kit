---
name: enterprise-spec
description: Methodology for large-scale projects requiring multi-session specification. Uses Divide & Conquer, Tiered Documentation, and 7 Enterprise Standards for complete coverage.
version: 1.0.0
---

# Enterprise Spec - Large Project Methodology

> **For projects too large to spec in a single session.**

## 🎯 When to Use

| Trigger | Example |
|---------|---------|
| Keyword `large` or `enterprise` | `/spec large "E-commerce Platform"` |
| 5+ features mentioned | "User auth, products, cart, checkout, orders..." |
| Multi-module system | "Admin panel + Customer app + API" |

---

## 📋 The 7 Enterprise Standards

| # | Standard | Purpose |
|---|----------|---------|
| 1 | **Hierarchical Decomposition** | 3-tier: Blueprint → Module → Task |
| 2 | **External State Persistence** | State files survive sessions |
| 3 | **Conflict Detection** | Flag ambiguities before spec |
| 4 | **Dependency Awareness** | Track cross-module impact |
| 5 | **Atomic TDD** | Each task = testable unit |
| 6 | **Continuity Protocol** | Session handoff mechanism |
| 7 | **Long Chain of Thought** | Step-by-step reasoning |

---

## 🏗️ 3-Tier Documentation Structure

```
docs/
├── _blueprint.md          ← TIER 1: Macro (System Overview)
├── _registry.md           ← APIs, Events, Shared Types
├── _map.md                ← File/Module Navigation Map
│
└── modules/               ← TIER 2: Meso (Module Specs)
    ├── auth/
    │   ├── SPEC.md        
    │   └── tasks/         ← TIER 3: Micro (Atomic Tasks)
    │       ├── 001-login-form.md
    │       └── 002-jwt-validation.md
    └── checkout/
        └── ...
```

---

## 📄 State Files (Standard 2)

### `_blueprint.md` - Master System Overview

```markdown
# [Project Name] - Master Blueprint

## System Context
[One paragraph describing the system]

## Module Index
| Module | Status | Owner | Depends On |
|--------|--------|-------|------------|
| auth | ⏳ In Progress | - | - |
| checkout | 📋 Todo | - | auth |

## Global Constraints
- [Constraint 1]
- [Constraint 2]

## Integration Points
[How modules connect - diagram optional]

---
[CHECKPOINT]: Session [ID] | [Date] | Modules done: X/Y
```

### `_registry.md` - Shared Contracts

```markdown
# API & Type Registry

## API Endpoints
| Method | Path | Module | Status |
|--------|------|--------|--------|
| POST | /api/auth/login | auth | ✅ |

## Shared Types
| Type | Definition | Used By |
|------|------------|---------|
| User | { id, email, role } | auth, checkout |

## Events
| Event | Emitter | Consumers |
|-------|---------|-----------|
| user.created | auth | email, analytics |
```

---

## 🔍 Module SPEC Template (Standard 1, 3, 4)

```markdown
# [Module Name] Specification

## 1. Purpose
[What problem does this module solve?]

## 2. Clarifications Required (Standard 3)
> [!WARNING]
> **[CLARIFY-001]**: [Question that blocks progress]
> **[CLARIFY-002]**: [Another ambiguity]

⚠️ **RULE**: No spec generation until clarifications resolved.

## 3. Impact Analysis (Standard 4)
| Affects | Type | Description |
|---------|------|-------------|
| `api/auth.ts` | CREATE | New file |
| `checkout` module | DEPENDS | Requires auth token |
| `_registry.md` | UPDATE | Add 3 endpoints |

## 4. Functional Requirements
### 4.1 [Feature] (Priority: MUST)
- **User Story**: As a [X], I want [Y], so that [Z]
- **Logic/Rules**: [Business logic]
- **Inputs**: [Data schema]
- **Outputs**: [Response schema]
- **Acceptance Criteria**:
  - [ ] Given X, When Y, Then Z

## 5. Atomic Task Index (Standard 5)
| ID | Task | Tests | DoD | Status |
|----|------|-------|-----|--------|
| 001 | Login Form | 3 | Tests pass | ⏳ |
| 002 | JWT Validation | 2 | Tests pass | 📋 |

---
[HANDOFF]: Completed sections 1-3. Next: Complete section 4-5.
```

---

## ⚛️ Atomic Task Template (Standard 5)

```markdown
# Task [ID]: [Name]

## Meta
- **Module**: [parent module]
- **Atomic Check**: ✅ Single action, 1-3 tests

## Specification
- **Input**: [Schema]
- **Output**: [Schema]
- **Logic**: [Step-by-step]

## TDD Test Cases
1. `test_[name]_success`: Valid input → Expected output
2. `test_[name]_invalid`: Invalid input → Error
3. `test_[name]_edge`: Edge case → Handled

## Definition of Done
- [ ] Tests written BEFORE code
- [ ] All tests pass
- [ ] No lint errors
- [ ] _registry.md updated (if API)

---
[STATUS]: 📋 Todo | ⏳ In Progress | ✅ Done
```

---

## 🧠 Long Chain of Thought (Standard 7)

### When Required

| Context | Reasoning Steps |
|---------|-----------------|
| Architecture Decision | Options → Pros/Cons → Trade-offs → Recommendation |
| Module Decomposition | Boundaries → Interfaces → Dependencies |
| Conflict Resolution | Problem → Root Cause → Solutions |
| Risk Assessment | Risk → Probability → Impact → Mitigation |

### Thinking Block Format

```markdown
## 🧠 [THINKING]: [Decision Point]

**Step 1: Problem**
- [What are we deciding?]

**Step 2: Context**
- [Constraints, requirements]

**Step 3: Options**
| Option | Pros | Cons |
|--------|------|------|
| A | ... | ... |
| B | ... | ... |

**Step 4: Trade-offs**
- [What matters most?]

**Step 5: Recommendation**
> [Decision] because [rationale]

**Checkpoint**: Does this align with your expectations?
```

---

## 🔄 Continuity Protocol (Standard 6)

### Session End Block (MANDATORY)

```markdown
---
## 📋 [HANDOFF] Session Summary

**Session ID**: [timestamp or identifier]

**Completed**:
- ✅ Created `_blueprint.md` (5 modules)
- ✅ Spec'd `auth` module (6 features, 12 tasks)

**Remaining**:
- 📋 `checkout` module (0% complete)
- 📋 `inventory` module (not started)

**State Files Updated**:
- `docs/_blueprint.md` ✅
- `docs/_registry.md` ✅
- `docs/modules/auth/SPEC.md` ✅

**Next Session Command**:
> `/spec continue` or `/spec module checkout`

**Blockers**:
- [CLARIFY-003] awaiting user response
```

---

## 🚀 Usage

### Start New Large Project
```bash
/spec large "E-commerce Platform with admin, customer app, and vendor portal"
```

### Continue Previous Session
```bash
/spec continue
```

### Spec Specific Module
```bash
/spec module checkout
```

### List Progress
```bash
/spec status
```

---

## 📊 Process Flow

```
/spec large "Project"
       ↓
┌─────────────────────────────────┐
│ PHASE 0: Blueprint Creation     │
│ - Create _blueprint.md          │
│ - Identify all modules          │
│ - Ask: "Which module first?"    │
└─────────────────────────────────┘
       ↓
┌─────────────────────────────────┐
│ PHASE 1: Module Iteration       │
│ FOR each module:                │
│ - Read _blueprint.md (refresh)  │
│ - Flag [CLARIFY] items          │
│ - Create SPEC.md                │
│ - Update _blueprint.md status   │
└─────────────────────────────────┘
       ↓
┌─────────────────────────────────┐
│ PHASE 2: Task Decomposition     │
│ FOR each feature:               │
│ - Create atomic task file       │
│ - Define TDD test cases         │
│ - Set Definition of Done        │
└─────────────────────────────────┘
       ↓
┌─────────────────────────────────┐
│ SESSION END: Continuity         │
│ - Update _blueprint.md          │
│ - Output [HANDOFF] block        │
│ - Suggest next session command  │
└─────────────────────────────────┘
```

---

## ⚠️ Enforcement Rules

1. **No Spec Without Clarification**: `[CLARIFY]` items MUST be resolved
2. **No Assumption Without Reasoning**: Use `[THINKING]` blocks
3. **No Session End Without Handoff**: Always output `[HANDOFF]`
4. **State Files First**: Read `_blueprint.md` before any module work
5. **Atomic = Testable**: If task can't be tested with 1-3 tests, decompose further
