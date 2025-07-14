# PRP Template: Full-Stack Next.js & tRPC

**Name:** "Base PRP Template v3 - Full-Stack Next.js project"

**Description:**
Template optimized for AI agents to implement full-stack features using:

- Next.js
- tRPC+Tanstack React Query for API
- Drizzle+neon for orm and database
- Tailwind v4 and shadcn/ui for UI
- Better-auth for authentication.

It provides comprehensive context and validation loops to ensure iterative success and high-quality code.

---

## **Core Principles**

1.  **Context is King**: Include all necessary documentation, examples, and caveats.
2.  **Validation Loops** – Ensure linting, typing, testing, and E2E flows are enforced and fixable.
3.  **Reuse & Convention** – Follow existing folder structures and idioms.
4.  **Progressive Enhancement** – Start with schema/backend, then client logic and UI.
5.  **Avoid Reinventing** – Extend working patterns from similar features.
6.  **Global Rules**: Be sure to follow all project-specific guidelines in `CLAUDE.md`.

---

## **Goal**

_A clear and specific description of the final desired state of the feature._
**Example:** "Build a project management dashboard where users can create, view, and delete projects. New projects are created via a modal form, and the project list updates in real-time."

---

## **Why**

- **Business Value:** What is the impact on the user or business?
- **Integration:** How does this fit into the existing application?
- **Problem Solved:** What specific problem does this feature solve, and for whom?

---

## **What**

_A summary of the user-facing behavior and technical requirements._

### ✅ Success Criteria

- [ ] Uses better-auth for user sessions and protected procedures.
- [ ] DrizzleORM schema with migration is correct and deployed.
- [ ] tRPC procedures created, tested, and type-safe.
- [ ] Frontend UI uses shadcn/ui components and real-time sync (TanStack React Query).
- [ ] All lint/type/test checks pass.
- [ ] Mobile and desktop responsive UI.

---

## **All Needed Context**

### **Documentation & References**

```yaml
# MUST READ - Include these in your context window
- url: https://orm.drizzle.team/docs/tutorials/drizzle-with-neon
  why: For defining database schemas and writing queries.

- url: https://trpc.io/docs/client/tanstack-react-query
  why: To understand creating routers, procedures, and using hooks on the client i.e., backend layer implementation.

- url: https://www.better-auth.com/docs/introduction
  why: authentication with better-auth
```

### Current Codebase tree (run `tree -I "node_modules|.next"` in the root of the project) to get an overview of the codebase

```bash

```

### Desired Codebase tree with files to be added and responsibility of file

```bash

```

### Known Gotchas of our codebase & Library Quirks

```ts
// CRITICAL: Ensure all tRPC procedures that mutate data are marked as `mutation`.
// CRITICAL: Use server components for data fetching whenever possible to reduce bundle size.
// CRITICAL: Protect tRPC procedures by using the `protectedProcedure` helper from our tRPC context.
// GOTCHA: Use `use client` directive only when strictly needed
// GOTCHA: When using shadcn/ui, components must be imported from your local `components/ui` directory, not directly from the library.
// PATTERN: Always use Zod for input validation on tRPC procedures.
// PATTERN: Database schema changes require running `pnpm drizzle-kit generate:pg` and then `pnpm drizzle-kit push:pg`.
```

## Implementation Blueprint

### Data Models and Structure (Drizzle & Zod)

Define the core data models in lib/db/schema.ts and input validation schemas.

```ts
// In lib/db/schema.ts
import { pgTable, serial, text, varchar } from "drizzle-orm/pg-core";

export const projects = pgTable("projects", {
  id: serial("id").primaryKey(),
  name: varchar("name", { length: 256 }).notNull(),
  description: text("description"),
  // ... other fields, like userId
});

// In server/api/routers/project.ts (for input validation)
import { z } from "zod";

export const createProjectSchema = z.object({
  name: z.string().min(1, "Project name is required."),
  description: z.string().optional(),
});
```

### list of tasks to be completed to fullfill the PRP in the order they should be completed

```yaml
Task 1:
  MODIFY lib/db/schema.ts:
    - ACTION: Add the `projects` table schema.

Task 2:
  RUN MIGRATION:
    - COMMAND: `pnpm drizzle-kit generate:pg` to create the migration file.
    - COMMAND: `pnpm drizzle-kit push:pg` to apply the schema to the Neon database.

Task 3:
  CREATE server/api/routers/project.ts:
    - ACTION: Implement tRPC procedures: `create`, `getAll`, `delete`.
    - PATTERN: Use Zod for input validation on the `create` mutation.
    - AUTH: Protect procedures using the `protectedProcedure` tRPC middleware.

Task 4:
  MODIFY server/api/root.ts:
    - ACTION: Mount the new `projectRouter` to the main `appRouter`.

Task 5:
  CREATE app/(dashboard)/projects/components/project-list.tsx:
    - ACTION: Build a client component that uses `api.project.getAll.useQuery()` to fetch and display projects.
    - UI: Use `Table` and `Card` components from shadcn/ui.

Task 6:
  CREATE app/(dashboard)/projects/components/create-project-button.tsx:
    - ACTION: Build a client component with a `Dialog` and `Form` from shadcn/ui.
    - LOGIC: Use `api.project.create.useMutation()` to handle form submission.
    - FEEDBACK: On success, invalidate the `getAll` query to trigger a refetch.

Task 7:
  CREATE app/(dashboard)/projects/page.tsx:
    - ACTION: Assemble the `ProjectList` and `CreateProjectButton` components on the page.

...(...)

Task N:
...

```

## Validation Loop

### Level 1: Syntax & Style

```bash
# Run these FIRST - fix all errors before proceeding.
pnpm lint --fix   # ESLint for style and syntax
pnpm tsc --noEmit # TypeScript for static type checking

# Expected: No errors. READ the error messages and fix them.
```

### Level 2: Backend Unit/Integration Tests (tRPC)

(Optional, but recommended for complex procedures)

```ts
// CREATE tests/project.router.test.ts
// (Assuming Vitest or Jest is set up)

import { test, expect } from "vitest";
// import router and mock context

test("createProject", async () => {
  const caller = appRouter.createCaller({ session: mockSession });
  const result = await caller.project.create({ name: "Test" });
  expect(result.name).toBe("Test");
});
```

```bash
# Run and iterate until passing:
pnpm test

# If failing: Read the error, understand the root cause, fix the code, and re-run.
```

### Level 3: End-to-End Test (Manual)

```bash
# 1. Start the development server
pnpm dev

# 2. Test the UI flow in the browser
# - Open http://localhost:3000/projects
# - Log in if required.
# - Click the "Create Project" button, fill out the form, and submit.
# - Verify the new project appears in the list.
# - Verify you can delete the project.

# If errors occur: Check the terminal for server-side errors and the browser's developer console for client-side errors.
```

## Final Validation Checklist

[ ] All linting checks pass
[ ] The project compiles without type errors
[ ] All automated tests pass
[ ] The manual end-to-end test flow is successful.
[ ] The feature is responsive and works on mobile and desktop viewports.
[ ] Server-side logs are clean and informative.
[ ] Client-side console has no errors.
[ ] All new components and procedures handle loading and error states gracefully.
[ ] Zod validations on input
[ ] .env.local is not hardcoded anywhere

---

## Anti-Patterns to Avoid

❌ Don't mix "use client" and "use server" semantics incorrectly.
❌ Don't fetch data in a client component when a server component can do it.
❌ Don't write raw SQL; use the Drizzle ORM for type safety.
❌ Don't forget to validate all user input on the server with Zod.
❌ Don't hardcode secrets or environment variables; use .env.local.
❌ Don't prop-drill; use TanStack React Query's cache or React Context where appropriate.
❌ Don't use Global any or as any casting
