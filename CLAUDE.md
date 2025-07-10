### AI Assistant Guidelines

- **Core Behavior:**
  - Be concise and direct. Omit unnecessary explanations.
  - Always think step-by-step and outline your plan before generating code.
  - Ask for clarification if a request is ambiguous.
  - Never hallucinate libraries or functions.

### Development Principles

- **Clarity & Readability:** Prioritize writing code that is clear, readable, and easy to understand over overly clever or complex solutions.
- **Consistency:** Adhere to the established coding styles and patterns found throughout the existing codebase.
- **Simplicity (KISS):** Keep It Simple, Stupid. Avoid introducing unnecessary complexity.
- **Do Not Repeat Yourself (DRY):** Strive for reusable code and abstract logic where appropriate to avoid duplication.

### Version Control

- **Branching:**
  - Create a new branch for every main task (e.g., feature, bug fix, chore).
  - Use descriptive, kebab-case branch names prefixed with `feature/`, `fix/`, or `chore/` (e.g., `feature/new-user-auth`).
- **Commits:**
  - Write clear and concise commit messages adhering to the **Conventional Commits** specification.
- **Merge Process:**
  - Merge feature branches to main after completion.

### Technology & Library Preferences

- Use **pnpm** for all Node.js package management.
- The framework is **Next.js** with **React**.
- Use **functional components with hooks**.
- For styling, use **Tailwind CSS v4+** as the base utility framework.
- For UI components, use **shadcn/ui** and customize them with Tailwind CSS as needed.
- For all date and time manipulation, use the **`date-fns`** library.
- For form management, use **`react-hook-form`** with **`zod`** for validation.
- For global state management (if needed), use **`zustand`** or **`jotai`**.

### Code Style & Formatting

- **Automation:**
  - **Automate formatting with Prettier** (`singleQuote: true`, `semi: false`).
  - **Enforce code quality with ESLint**.
- **Syntax:**
  - In JavaScript/TypeScript, use **single quotes** and **omit semicolons**.
  - **Use absolute imports for modules** (e.g., `@/features/*`).
- **Structure & Comments:**
  - Organize code into **feature-based folders** if possible.
  - Proactively refactor code into smaller modules (aim for < 700 lines if possible).
  - **Comment non-obvious code** and ensure everything is understandable to an entry-level developer.
- **React 19+ Best Practices:**
  - **Leverage Server Components:** Default to using React Server Components (RSCs) to minimize the client-side JavaScript bundle and improve performance. Use client components (`'use client'`) only when interactivity is required.
  - **Component Architecture:** Keep pages and layouts as Server Components. Push client components as low as possible in the component tree (ideally as leaf components) to minimize bundle size.
- **Naming Conventions:**
  - **Variables and Functions:** Use `camelCase`.
  - **Classes and Components:** Use `PascalCase`.
  - **Constants:** Use `UPPER_SNAKE_CASE`.
- **Error Handling:**
  - Implement robust error handling for all external service calls, API routes, and I/O operations.
  - Use `try...catch` blocks for synchronous code and `.catch()` for promises.

### Testing

- **Write tests using Vitest**.
- **Use React Testing Library** for component testing.
- Aim for meaningful test coverage on critical business logic and UI.

### Security & Code Integrity

- **Secrets:** Never include API keys or secrets in the code. Use `.env.local` and provide a `.env.example` file.
- **Validation:** Validate environment variables on startup using Zod.
- **Database:** Always use an ORM (like Drizzle) to prevent SQL injection.
- **Code Manipulation:** Never delete or overwrite code unless explicitly instructed or as part of an assigned task such as from task-master.
