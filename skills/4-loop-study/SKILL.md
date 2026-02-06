---
name: loop-study
description: "Research modern solutions and best practices for technical decisions. Use when you need to find current documentation, compare libraries, or discover best practices. Uses web search and Context7 MCP for up-to-date information. Triggers on: research this, find best practices for, what's the current approach to, look up documentation for, study how to, compare options for."
---

# Loop Research & Study

Find modern, current solutions for technical challenges. This skill uses web search and Context7 MCP to discover the latest best practices, documentation, and implementation patterns.

**Key Principle:** Solutions evolve constantly. Always search for the CURRENT best approach, not cached knowledge.

**Core Tools:**
- **Context7 MCP** - Get the most current official documentation
- **Web Search** - Find current best practices and comparisons
- When you find outdated information, note the more current reference in research.md

---

## The Job

1. Identify research topics (from spec, PRD, or direct request)
2. Search for current solutions using WebSearch and Context7
3. Document findings with decisions, rationale, and alternatives
4. Output to `specs/[feature-name]/research.md`

---

## When to Use This Skill

- Technical decisions marked `[NEEDS CLARIFICATION]` in a spec
- Library/framework comparisons ("Which state management?")
- Best practices for specific patterns ("How to handle auth in Next.js 14?")
- Current documentation lookup ("What's the Drizzle migration syntax?")
- Modern approaches ("What's the 2024/2025 way to do X?")

---

## Research Workflow

### Step 1: Identify Research Topics

Extract from the spec's "Research Needed" section OR from user request:

```markdown
## Research Topics

1. [ ] Best approach for real-time updates in Next.js 14
2. [ ] Current state management recommendations (2025)
3. [ ] Drizzle vs Prisma for this use case
4. [ ] Authentication patterns for server components
```

### Step 2: Research Each Topic

For EACH topic, follow this process:

#### A. Context7 Lookup (Official Documentation)

```
1. Use mcp__context7__resolve-library-id to find the library ID
   - Query: "[library name]"

2. Use mcp__context7__query-docs to get current documentation
   - Query: "[specific question about the topic]"
```

**Example:**
```
resolve-library-id: "next.js"
query-docs: libraryId="/vercel/next.js", query="server actions best practices"
```

#### B. Web Search (Current Best Practices)

```
Use WebSearch for:
- "[topic] best practices 2025"
- "[topic] vs [alternative] comparison 2025"
- "[framework] [pattern] current recommended approach"
```

**Example searches:**
- "Next.js 14 authentication best practices 2025"
- "Drizzle vs Prisma comparison 2025"
- "React server components state management"

#### C. Synthesize Findings

Combine Context7 documentation with web search results to form recommendations.

---

## Research Output Format

### research.md Structure

```markdown
# Research: [Feature Name]

**Date:** [YYYY-MM-DD]
**Spec:** [link to spec.md]
**Status:** Complete | In Progress

---

## Executive Summary

[2-3 sentences: Key decisions made and primary rationale]

---

## Research Topics

### 1. [Topic Title]

**Question:** [The specific question being researched]

**Decision:** [What we're going with]

**Rationale:**
- [Reason 1]
- [Reason 2]
- [Reason 3]

**Alternatives Considered:**

| Option | Pros | Cons | Why Not |
|--------|------|------|---------|
| [Alt 1] | Fast, simple | Limited features | Doesn't support X |
| [Alt 2] | Full-featured | Complex setup | Overkill for our needs |
| [Alt 3] | Popular | Poor TS support | Type safety critical |

**Sources:**
- [Source 1 - link or "Context7: library-id"]
- [Source 2 - link]
- [Source 3 - link]

**Code Example:**
```typescript
// Recommended pattern from research
const example = ...
```

---

### 2. [Next Topic]

[Same structure]

---

## Implementation Notes

[Any cross-cutting concerns or integration notes discovered during research]

---

## Updated Technical Context

Based on research, update these spec decisions:

| Aspect | Original | Researched | Reason |
|--------|----------|------------|--------|
| Auth | NEEDS CLARIFICATION | NextAuth.js v5 | Best Next.js 14 integration |
| State | NEEDS CLARIFICATION | Zustand | Simpler than Redux, TS support |

---

## Derivation Trail

**How we arrived at these solutions (A to Z):**

This section documents the research path for future agents:

1. **Starting Point:** [Initial question or requirement]
2. **First Search:** [What we searched, what we found]
3. **Pivot Point:** [If initial approach was outdated, what changed]
4. **Validation:** [How we confirmed the solution is current]
5. **Final Decision:** [What we're using and why]

---

## Outdated Information Found

| Source | Outdated Info | Current Alternative | Date Found |
|--------|---------------|---------------------|------------|
| [old source] | [what was wrong] | [correct approach] | [date] |

---

## Open Items

- [ ] [Anything that couldn't be resolved]
- [ ] [Items needing team discussion]
```

---

## Research Patterns

### Pattern 1: Library Comparison

```markdown
**Question:** Which [category] library should we use?

**Research approach:**
1. Context7: Get docs for top 3 options
2. WebSearch: "[lib1] vs [lib2] vs [lib3] 2025"
3. WebSearch: "[lib] production experience"
4. Check: GitHub stars, recent commits, TypeScript support

**Decision framework:**
- Does it solve our specific problem?
- Is it actively maintained (commits in last 3 months)?
- Does it have good TypeScript support?
- Is the bundle size acceptable?
- Does it match our existing patterns?
```

### Pattern 2: Best Practices Lookup

```markdown
**Question:** What's the current best practice for [pattern]?

**Research approach:**
1. Context7: Query official docs for the framework
2. WebSearch: "[framework] [pattern] best practices 2025"
3. WebSearch: "[framework] [pattern] pitfalls avoid"

**Validate findings:**
- Is this from official docs or respected source?
- Was this written/updated recently (check dates)?
- Does it apply to our version?
```

### Pattern 3: Migration/Upgrade Research

```markdown
**Question:** How do we migrate from [old] to [new]?

**Research approach:**
1. Context7: Query migration guides in new version docs
2. WebSearch: "[old] to [new] migration guide"
3. WebSearch: "[new] breaking changes from [old]"

**Document:**
- Step-by-step migration path
- Breaking changes that affect us
- Deprecation timeline
```

### Pattern 4: Architecture Decision

```markdown
**Question:** Which architecture pattern for [requirement]?

**Research approach:**
1. WebSearch: "[requirement] architecture patterns 2025"
2. Context7: Query framework docs for recommended patterns
3. WebSearch: "[pattern] at scale production"

**Consider:**
- Complexity vs. our team size
- Alignment with framework conventions
- Future maintenance burden
```

---

## Using Context7 MCP

### Step 1: Resolve Library ID

```
Tool: mcp__context7__resolve-library-id
Input:
  - libraryName: "next.js" (or "react", "drizzle", etc.)
  - query: "What I'm trying to accomplish"
Output: Library ID like "/vercel/next.js"
```

### Step 2: Query Documentation

```
Tool: mcp__context7__query-docs
Input:
  - libraryId: "/vercel/next.js"
  - query: "How to implement server actions with forms"
Output: Current documentation and code examples
```

### Common Library IDs

| Library | Likely ID | Use For |
|---------|-----------|---------|
| Next.js | /vercel/next.js | React framework |
| React | /facebook/react | UI library |
| Drizzle | /drizzle-team/drizzle-orm | Database ORM |
| Prisma | /prisma/prisma | Database ORM |
| Tailwind | /tailwindlabs/tailwindcss | Styling |
| tRPC | /trpc/trpc | Type-safe APIs |
| Zustand | /pmndrs/zustand | State management |

**Note:** Always use `resolve-library-id` first - IDs may change.

---

## Using Web Search

### Effective Search Queries

**DO:**
- Include year: "React server components 2025"
- Be specific: "Next.js 14 app router authentication"
- Include context: "TypeScript Drizzle PostgreSQL migrations"

**DON'T:**
- Vague queries: "how to do auth"
- Old patterns: "React class components" (unless specifically needed)
- Skip the year: Results may be outdated

### Evaluating Sources

**Trust hierarchy:**
1. Official documentation (highest)
2. Framework team blog posts
3. Respected tech blogs (Vercel, Kent C. Dodds, etc.)
4. Recent Stack Overflow answers (check dates!)
5. Tutorial sites (verify against official docs)

**Red flags:**
- No date or old date (pre-2023 for modern frameworks)
- Contradicts official docs
- Uses deprecated APIs
- From content farms

---

## Research Checklist

Before completing research.md:

- [ ] Each topic has a clear Decision
- [ ] Rationale explains WHY (not just what)
- [ ] Alternatives were genuinely considered
- [ ] Sources are linked and recent
- [ ] Code examples are included where helpful
- [ ] Updated Technical Context table completed
- [ ] Derivation Trail documented for future agents
- [ ] Outdated information flagged with current alternatives
- [ ] No NEEDS CLARIFICATION items remain unresolved

---

## Example: Real-Time Updates Research

**Topic:** Best approach for real-time task status updates

**Context7 Queries:**
```
resolve-library-id: "next.js"
query-docs: "/vercel/next.js", "real-time updates server components"
```

**Web Searches:**
- "Next.js 14 real-time updates best practices 2025"
- "Server-sent events vs websockets Next.js"
- "React server components real-time data"

**Output:**
```markdown
### 1. Real-Time Task Status Updates

**Question:** How should we implement real-time status updates for the task list?

**Decision:** Server-Sent Events (SSE) with React Server Components

**Rationale:**
- SSE is simpler than WebSockets for one-way updates
- Native browser support, no library needed
- Works well with Next.js streaming
- Automatic reconnection built-in

**Alternatives Considered:**

| Option | Pros | Cons | Why Not |
|--------|------|------|---------|
| WebSockets | Bi-directional | Complex setup, needs ws library | Overkill for one-way updates |
| Polling | Simple | Inefficient, delayed updates | Poor UX for real-time |
| Pusher/Ably | Managed, scalable | External dependency, cost | Small scale doesn't need it |

**Sources:**
- Context7: /vercel/next.js - Streaming documentation
- https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming
- "Server-Sent Events Next.js 14 2025" - web search results

**Derivation Trail:**
1. Starting Point: Need real-time task updates without page refresh
2. First Search: "Next.js real-time" - found WebSockets and SSE options
3. Pivot Point: WebSockets overkill for one-way server→client updates
4. Validation: Checked Next.js docs via Context7, confirmed SSE works with streaming
5. Final Decision: SSE with native ReadableStream API

**Code Example:**
```typescript
// app/api/tasks/stream/route.ts
export async function GET() {
  const encoder = new TextEncoder()
  const stream = new ReadableStream({
    async start(controller) {
      const unsubscribe = subscribeToTasks((task) => {
        controller.enqueue(encoder.encode(`data: ${JSON.stringify(task)}\n\n`))
      })
      return () => unsubscribe()
    }
  })
  return new Response(stream, {
    headers: { 'Content-Type': 'text/event-stream' }
  })
}
```
```

---

## Output Location

Save to: `specs/[feature-name]/research.md`

If no feature directory exists:
```
specs/[feature-name]/
├── spec.md           # From loop-spec skill
└── research.md       # This research document
```

---

## Next Step

After completing research, update the technical specification (`spec.md`) with:
1. Resolved NEEDS CLARIFICATION items
2. Updated Technical Context table
3. Any new considerations discovered

Then proceed to `/loop-task` to break the spec into implementable user stories.
