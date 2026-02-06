---
name: loop-spec
description: "Create a technical specification from a PRD for the Loop autonomous agent system. Use when you have a PRD and need to define HOW to build it - architecture, data model, API contracts, and component design. Triggers on: create spec from this prd, technical specification, how should we build this, architecture for, design spec."
---

# Loop Technical Specification

Transform a PRD into a technical implementation specification. This defines HOW we're going to build it - the architecture, data models, API contracts, and component structure.

**Important:** This skill requires an existing PRD. Use the `loop-prd` skill first if you don't have one.

---

## The Job

1. Read the PRD (markdown or prd.json)
2. Identify technical decisions needed (marked as NEEDS CLARIFICATION)
3. Generate a structured technical specification
4. Output to `specs/[feature-name]/spec.md`

**Important:** Do NOT start implementing. Just create the technical spec.

---

## Input Requirements

The PRD should contain:
- User stories with acceptance criteria
- Functional requirements
- Non-goals (scope boundaries)
- Quality gates

---

## Step 1: Extract Technical Decisions

Scan the PRD and identify decisions needed:

### Technical Context Checklist

For each item, either specify the choice OR mark `[NEEDS CLARIFICATION: specific question]`:

```markdown
## Technical Context

| Aspect | Decision |
|--------|----------|
| Language/Runtime | [e.g., TypeScript 5.x, Node 20] |
| Framework | [e.g., Next.js 14, Express] |
| Database | [e.g., PostgreSQL, SQLite, none] |
| ORM/Query | [e.g., Drizzle, Prisma, raw SQL] |
| State Management | [e.g., React state, Zustand, Redux] |
| Testing | [e.g., Vitest, Jest, Playwright] |
| Deployment | [e.g., Vercel, Docker, local only] |
```

**Maximum 3 NEEDS CLARIFICATION markers.** Make informed defaults for everything else based on:
- Existing codebase patterns (check package.json, existing code)
- Industry standards for the project type
- Simplest solution that meets requirements

---

## Step 2: Ask Clarifying Questions (If Needed)

If there are NEEDS CLARIFICATION items, present them as options:

```
1. Which database approach should we use?
   A. PostgreSQL with Drizzle ORM (recommended for production)
   B. SQLite for simplicity
   C. In-memory/file-based (no database)
   D. Other: [specify]

2. How should we handle authentication?
   A. Session-based with cookies
   B. JWT tokens
   C. OAuth only (delegate to provider)
   D. None needed for this feature
```

Wait for answers before generating the spec. User can respond with "1A, 2B" format.

---

## Step 3: Generate Technical Specification

### Spec Structure

```markdown
# Technical Specification: [Feature Name]

**Branch:** `loop/[feature-name]`
**Date:** [YYYY-MM-DD]
**PRD:** [link or path to PRD]
**Status:** Draft | Review | Approved

---

## Summary

[2-3 sentences: What we're building and the primary technical approach]

---

## Technical Context

| Aspect | Decision | Rationale |
|--------|----------|-----------|
| Language | TypeScript 5.x | Existing codebase |
| Framework | Next.js 14 | App router for server components |
| Database | PostgreSQL | Production-ready, existing setup |
| ... | ... | ... |

---

## Architecture Overview

[High-level description of components and how they interact]

### Component Diagram (Text)

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Client    │────▶│   Server    │────▶│  Database   │
│  (React)    │     │  (Actions)  │     │ (Postgres)  │
└─────────────┘     └─────────────┘     └─────────────┘
```

---

## Data Model

### Entities

For each entity, define:

#### [Entity Name]
| Field | Type | Constraints | Description |
|-------|------|-------------|-------------|
| id | uuid | PK | Unique identifier |
| name | string | NOT NULL, max 255 | Display name |
| status | enum | DEFAULT 'pending' | pending, active, done |
| created_at | timestamp | NOT NULL | Creation time |
| updated_at | timestamp | NOT NULL | Last update |

**Relationships:**
- [Entity] has many [OtherEntity]
- [Entity] belongs to [ParentEntity]

**Indexes:**
- `idx_entity_status` on (status)
- `idx_entity_user` on (user_id)

---

## API Contracts

### [Endpoint Group]

#### `POST /api/[resource]`
**Purpose:** Create a new [resource]

**Request:**
```typescript
{
  name: string;       // Required, max 255 chars
  status?: string;    // Optional, defaults to 'pending'
}
```

**Response (201):**
```typescript
{
  id: string;
  name: string;
  status: string;
  createdAt: string;  // ISO 8601
}
```

**Errors:**
- 400: Invalid input (validation failed)
- 401: Unauthorized
- 500: Server error

#### `GET /api/[resource]`
...

#### `PUT /api/[resource]/:id`
...

#### `DELETE /api/[resource]/:id`
...

---

## Component Structure

### New Components

| Component | Location | Purpose |
|-----------|----------|---------|
| FeatureList | `components/feature/` | Display list of items |
| FeatureForm | `components/feature/` | Create/edit form |
| FeatureCard | `components/feature/` | Individual item display |

### Modified Components

| Component | Changes |
|-----------|---------|
| Header | Add navigation link |
| Sidebar | Add feature section |

---

## File Changes

### New Files
- `app/feature/page.tsx` - Main feature page
- `app/api/feature/route.ts` - API endpoints
- `components/feature/FeatureList.tsx` - List component
- `lib/db/schema/feature.ts` - Database schema
- `lib/actions/feature.ts` - Server actions

### Modified Files
- `lib/db/schema/index.ts` - Export new schema
- `app/layout.tsx` - Add navigation

---

## State Management

[How state flows through the application]

- Server state: [Approach - e.g., Server Components, React Query]
- Client state: [Approach - e.g., React useState, Zustand]
- Form state: [Approach - e.g., React Hook Form, native]

---

## Error Handling

| Scenario | Handling |
|----------|----------|
| Network failure | Show retry button, preserve input |
| Validation error | Display inline field errors |
| Auth failure | Redirect to login |
| Not found | Show 404 component |

---

## Security Considerations

- [ ] Input validation on all endpoints
- [ ] Authorization checks (user can only access own data)
- [ ] CSRF protection (if using forms)
- [ ] Rate limiting (if public API)

---

## Testing Strategy

| Type | Coverage | Tool |
|------|----------|------|
| Unit | Business logic, utilities | Vitest |
| Integration | API routes, database | Vitest |
| E2E | Critical user flows | Playwright |

### Key Test Cases
1. [Test case from acceptance criteria]
2. [Test case from acceptance criteria]
3. [Edge case handling]

---

## Migration Plan

1. Create database migration
2. Deploy schema changes
3. Deploy application code
4. Verify in staging
5. Deploy to production

---

## Open Questions

- [Any remaining technical questions]
- [Dependencies on other teams/features]

---

## Appendix: Research Needed

[Items requiring research in the next phase - loop-study]

- [ ] Best approach for [specific technical challenge]
- [ ] Current best practices for [technology/pattern]
- [ ] Library comparison for [functionality]
```

---

## Spec Quality Checklist

Before saving, verify:

- [ ] All NEEDS CLARIFICATION resolved (or max 3 with clear questions)
- [ ] Data model covers all entities from PRD
- [ ] API contracts cover all functional requirements
- [ ] Component structure matches user stories
- [ ] Error handling defined for each failure mode
- [ ] Testing strategy covers acceptance criteria
- [ ] Security considerations addressed
- [ ] No vague statements ("works correctly", "handles errors")

---

## Output Location

Save to: `specs/[feature-name]/spec.md`

Create the directory structure:
```
specs/[feature-name]/
├── spec.md           # This technical specification
├── research.md       # Created by loop-study skill
└── contracts/        # Optional: detailed API specs
    └── [resource].yaml
```

---

## Example: Task Status Feature

**Input PRD excerpt:**
```markdown
## User Stories
### US-001: Add status field to tasks table
As a developer, I need to store task status in the database.

### US-002: Display status badge on task cards
As a user, I want to see task status at a glance.
```

**Output spec excerpt:**
```markdown
## Data Model

### Task (modified)
| Field | Type | Constraints | Description |
|-------|------|-------------|-------------|
| id | uuid | PK | Existing |
| title | string | NOT NULL | Existing |
| **status** | enum | DEFAULT 'pending' | NEW: pending, in_progress, done |
| updated_at | timestamp | NOT NULL | Existing |

## API Contracts

### `PATCH /api/tasks/:id/status`
**Purpose:** Update task status

**Request:**
```typescript
{ status: 'pending' | 'in_progress' | 'done' }
```

**Response (200):**
```typescript
{ id: string; status: string; updatedAt: string }
```

## Component Structure

### New Components
| Component | Location | Purpose |
|-----------|----------|---------|
| StatusBadge | `components/tasks/` | Colored status indicator |
| StatusDropdown | `components/tasks/` | Status change control |
```

---

## Next Step

After creating the spec, use `/loop-study` to research any items in the "Research Needed" appendix using web search and Context7 for current documentation.
