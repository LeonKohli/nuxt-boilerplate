# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a modern **Nuxt 3 boilerplate** designed as a starting point for building production-ready web applications. It's configured with best practices and a comprehensive tech stack ready for customization.

**IMPORTANT**: This is a boilerplate project meant to be adapted for specific use cases. When starting a new project with this boilerplate, update this CLAUDE.md file + components, pages, and configurations to match your specific requirements.

---

## 🚫 CRITICAL RULE: Never modify files in `app/components/ui/` 🚫

**AI and all contributors must NEVER make changes to any files inside the `app/components/ui/` directory.**  
These files are managed by shadcn-vue and Reka UI, and are considered vendor or upstream code.  
- Do not edit, refactor, reformat, or auto-fix code in `app/components/ui/` under any circumstances.
- This rule exists to ensure seamless upgrades and avoid merge conflicts with upstream component updates.

---

## Tech Stack

- **Framework**: Nuxt 3 with Vue 3 (Composition API only)
- **UI Components**: shadcn-vue (Reka UI)
- **Styling**: Tailwind CSS v4 with CSS variables
- **Package Manager**: Bun (required - do not use npm/yarn/pnpm)
- **Type Checking**: TypeScript with vue-tsc
- **Utilities**: VueUse for composition utilities

## Development Commands

```bash
# Development
bun run dev          # Start development server

# Type checking
bun run typecheck    # Run type checking with nuxi typecheck

# Building
bun run build        # Build for production
bun run preview      # Preview production build
bun run generate     # Generate static site

# Testing
bun run test         # Run tests with Vitest

# Adding UI components
bunx shadcn-vue@latest add <component-name>
```

## Architecture Guidelines

### Directory Structure
The project uses Nuxt 4's app directory structure:
- `app/components/` - Vue components (PascalCase naming)
- `app/components/ui/` - shadcn-vue UI components
- `app/pages/` - File-based routing (camelCase naming)
- `app/composables/` - Reusable composition functions (use[Name] pattern)
- `app/layouts/` - Layout templates
- `app/utils/` - Utility functions
- `server/api/` - Server API endpoints

### Code Style Requirements

1. **Always use Composition API with TypeScript**:
   ```vue
   <script setup lang="ts">
   // Your code here
   </script>
   ```

2. **No manual imports for Vue/Nuxt functions** - They are auto-imported

3. **Data Fetching**:
   - Use `useFetch` for SSR-optimized requests
   - Use `$fetch` for client-side only requests
   - Use `useAsyncData` for complex data fetching scenarios

4. **State Management**: Use `useState` for cross-component reactive state

5. **Error Handling**:
   - Client: `throw createError('Error message')`
   - Server: `throw createError({ statusCode: 404, statusMessage: 'Not found' })`

## Design Principles (MUST FOLLOW)

### Minimal Design Philosophy
- Focus on essential features only
- Remove decorative elements without purpose
- Maximum 3 primary actions per view
- Limited color palette: 60% primary, 30% secondary, 10% accent

### Spacing System
- Base unit: 4px or 8px
- Small components: 8px-12px padding
- Medium components: 16px-24px padding
- Large components: 24px-32px padding
- Section spacing: 32px-48px
- Maximum content width: 680px-800px

### Typography Scale
- Base size: 16px
- Main headings: 32px-40px
- Subheadings: 24px-32px
- Body text: 16px-18px with 1.5-1.6 line height
- Maximum 65-75 characters per line

### Interactive Patterns
- Primary actions accessible within 1-2 clicks
- Minimum touch target: 44px × 44px
- Loading states for actions > 300ms
- Transitions: 150ms-300ms duration
- Hover scale: 1.02-1.05
- Focus states with 3px outline

### Responsive Design
- Mobile-first approach
- Breakpoints: 320px, 481px, 769px, 1025px, 1201px
- Single column on mobile, multi-column on desktop
- 15%-20% typography scale increase between breakpoints

## Component Development

1. **UI Components**: Use existing shadcn-vue components from `app/components/ui/`
2. **Styling**: 
   - Use inline Tailwind classes only - no @apply directives
   - **IMPORTANT**: Always use the predefined color variables from `app/assets/css/main.css`:
     - `bg-background`, `text-foreground` for main content
     - `bg-card`, `text-card-foreground` for cards
     - `bg-primary`, `text-primary-foreground` for primary actions
     - `bg-secondary`, `text-secondary-foreground` for secondary elements
     - `bg-muted`, `text-muted-foreground` for muted/subtle content
     - `bg-destructive`, `text-destructive-foreground` for errors/warnings
     - `border-border` for borders
     - `ring-ring` for focus states
   - Never use arbitrary color values or Tailwind's default colors (e.g., avoid `bg-gray-500`, `text-blue-600`)
   - The color system uses OKLCH color space and automatically adapts to dark/light modes
3. **Icons**: Use `<Icon>` component from @nuxt/icon with Lucide icons

## SEO & Performance

- Use `useSeoMeta` for SEO configuration
- Implement proper heading hierarchy (H1, H2, H3)
- Use `<NuxtLink>` for internal navigation with prefetching
- Apply lazy loading for below-fold content

## Project Customization Notes

When adapting this boilerplate for a specific project:
1. Update the homepage content in `app/pages/index.vue`
2. Modify the theme configuration in `app/assets/css/main.css`
3. Update SEO defaults in `nuxt.config.ts`
4. Add project-specific API routes in `server/api/`
5. Customize layouts and components as needed

## Important Conventions

- **PascalCase**: Component files (e.g., `MyComponent.vue`)
- **camelCase**: Pages and functions (e.g., `myPage.vue`, `useMyComposable`)
- **Composables**: Named as `use[Name]` (e.g., `useAuth`, `useTheme`)
- **No classes**: Use functional programming patterns only
- **TypeScript**: Use interfaces over types for better extendability
- **Git commits**: Never include "Co-Authored-By: Claude" in commit messages
