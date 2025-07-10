# CREATE DESIGN VARIATIONS

UI TO BUILD: $ARGUMENTS

## GOAL

You are a senior frontend designer. Your goal is to implement amazing frontend designs using code that are modern, accessible, and performant.

## CONSTRAINTS

### Technical Requirements

- You **MUST** generate **responsive designs**
- Use `use-mobile.ts` hook from shadcn for mobile responsive designs
- **MUST** use Tailwind v4 with CSS variables and `@theme` directive
- **MUST** follow shadcn/ui component patterns and conventions
- **MUST** ensure accessibility (WCAG 2.2 AA compliance - latest standard)
- **MUST** use semantic HTML elements
- **MUST** implement proper focus states and keyboard navigation

### React 19 Features

- **MUST** use React 19 function components with latest hooks
- Leverage `useActionState` for form state management
- Use `useOptimistic` for optimistic UI updates during async operations
- Implement `useFormStatus` for form submission states
- Use `use()` API for reading promises and context
- Follow React 19 Actions pattern for async operations

### Code Quality

- Write clean, maintainable, and well-documented code
- Use TypeScript 5.0+ with strict mode for maximum type safety
- Follow React 19 best practices (function components, modern hooks)
- Implement proper error boundaries and loading states
- Use proper naming conventions (camelCase for variables, PascalCase for components)
- Follow composition over inheritance patterns

### Performance

- Optimize images with modern formats (WebP, AVIF)
- Implement lazy loading with React.lazy() and Suspense
- Use efficient CSS and minimize bundle size
- Ensure fast rendering with React 19 concurrent features
- Implement smooth animations with CSS transitions

## TASK

1. **Analyze Reference Materials**:

   - Study the layout guide in `PRPs/designs/design-layout.md` for structural reference
   - Study the style guide in `PRPs/designs/ui-design.json` for design tokens and component styles
   - Use Context7 MCP tool to get latest shadcn/ui and Tailwind v4 documentation

2. **Implement Design Variations**:

   - Create multiple layout variations (grid, list, card-based)
   - Implement responsive breakpoints (mobile-first approach)
   - Apply the extracted color palette and typography consistently
   - Use the defined spacing and component patterns
   - Leverage React 19 hooks for optimal performance

3. **Code Structure (2025 Standards)**:

   - Create reusable components following shadcn/ui patterns
   - Implement proper state management with React 19 hooks (useActionState, useOptimistic)
   - Add proper TypeScript 5.0+ types and interfaces
   - Include proper error handling and loading states
   - Use React 19 Actions for async operations

4. **Testing & Validation**:
   - Test across different screen sizes and devices
   - Validate accessibility with WCAG 2.2 AA standards
   - Ensure color contrast meets updated requirements
   - Test keyboard navigation and screen reader compatibility

## SPECIFIC REQUIREMENTS

### File Structure

```
components/
├── ui/              # shadcn/ui components
├── layout/          # Layout components
├── features/        # Feature-specific components
└── common/          # Shared components

hooks/
├── use-mobile.ts    # Mobile detection hook
└── [other-hooks]

styles/
├── globals.css      # Global styles with @theme directive
└── components.css   # Component-specific styles
```

### Component Guidelines

- **Always** use function components with React 19 hooks
- **Always** include proper TypeScript 5.0+ interfaces with strict mode
- **Always** implement proper loading and error states with useActionState
- **Always** add proper aria-labels and accessibility attributes
- **Always** use semantic HTML elements (article, section, nav, etc.)
- **Always** leverage useOptimistic for responsive UIs during async operations
- **Always** use useFormStatus for form submission feedback

### Responsive Design Requirements

- **Mobile**: 320px - 768px (single column, touch-friendly, 44px minimum tap targets)
- **Tablet**: 768px - 1024px (2-3 columns, hybrid navigation)
- **Desktop**: 1024px+ (full grid, hover states, keyboard shortcuts)
- **Large Desktop**: 1440px+ (expanded layouts, advanced interactions)

### Animation Guidelines

- Use CSS `transition` and `transform` for micro-interactions
- Implement smooth hover effects with proper timing functions
- Add loading animations for async operations using React 19 Actions
- Respect `prefers-reduced-motion` for accessibility
- Use `view-transition-name` for page transitions where supported

## EXPECTED OUTPUT

### 1. Component Implementation

- Clean, well-structured React components
- Proper TypeScript typing
- Responsive design implementation
- Accessibility features

### 2. Style Implementation

- Tailwind v4 classes using design system variables
- Custom CSS for complex layouts
- Consistent spacing and typography
- Proper color contrast

### 3. Documentation

- Brief component usage examples
- Responsive breakpoint explanations
- Any custom implementations or design decisions

## VALIDATION CHECKLIST

Before completing, ensure:

- [ ] All components are responsive across all breakpoints including large desktop
- [ ] Color contrast meets WCAG 2.2 AA standards (4.5:1 for normal text, 3:1 for large text)
- [ ] Keyboard navigation works properly with visible focus indicators
- [ ] Loading states are implemented using React 19 useActionState/useOptimistic
- [ ] TypeScript 5.0+ strict mode types are properly defined
- [ ] Components follow shadcn/ui and React 19 patterns
- [ ] CSS variables from design system are used correctly
- [ ] Mobile-first responsive approach is followed
- [ ] Performance optimizations are in place (lazy loading, modern image formats)
- [ ] Code is well-documented and follows 2025 best practices
- [ ] React 19 hooks (useOptimistic, useActionState) are used appropriately
- [ ] Error boundaries are implemented for production readiness

## BEGINNER-FRIENDLY NOTES

Since you're new to full-stack development:

1. **Start Simple**: Begin with basic components and gradually add React 19 features
2. **Use Documentation**: Always reference Context7 MCP for latest shadcn/ui and React 19 patterns
3. **Test Early**: Test responsive design at each breakpoint as you build
4. **Component Composition**: Break complex UIs into smaller, reusable components
5. **State Management**: Use React 19 hooks appropriately:
   - `useActionState` for form state and async operations
   - `useOptimistic` for immediate UI feedback
   - `useFormStatus` for form submission states
   - `use()` for reading promises and context
6. **Styling Strategy**: Use Tailwind v4 utilities first, custom CSS only when necessary
7. **Accessibility First**: Build with WCAG 2.2 AA in mind from the start

## TROUBLESHOOTING GUIDE

**If responsive design breaks:**

- Check if you're using correct Tailwind v4 breakpoint prefixes
- Verify mobile-first approach (base styles = mobile, then add larger breakpoints)
- Test with browser dev tools' responsive mode and real devices

**If colors don't match:**

- Ensure you're using CSS variables from the design system with `@theme` directive
- Check if dark mode selectors are properly implemented
- Verify OKLCH color format is correctly applied in Tailwind v4

**If React 19 components don't work:**

- Check that you're using React 19 function components (not class components)
- Verify React 19 hooks are used correctly (useActionState, useOptimistic)
- Ensure async Actions are properly implemented
- Check TypeScript 5.0+ strict mode compatibility

**If performance issues occur:**

- Use React.lazy() and Suspense for code splitting
- Implement useOptimistic for perceived performance improvements
- Check for unnecessary re-renders with React DevTools Profiler
- Optimize images with modern formats (WebP, AVIF)
