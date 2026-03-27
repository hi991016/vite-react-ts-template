# Vite React TypeScript Template

A minimal React + TypeScript starter with Vite, SCSS, strict linting, and pre-commit hooks.

---

## Tech Stack

| | Library | Description |
|---|---|---|
| **Core** | React 19, TypeScript 5.9 | UI & type safety |
| **Build** | Vite (rolldown) 7.2 | Dev server & bundler |
| **Styling** | Sass 1.97 | SCSS support |
| **Linting** | ESLint 9 + typescript-eslint | Code quality |
| **Formatting** | Prettier 3.8 | Code style |
| **Git Hooks** | Husky 9 + lint-staged | Pre-commit checks |

---

## Project Structure

```
src/
├── assets/         # Images, fonts — exported via index.ts
├── components/     # React components — exported via index.ts
├── hooks/          # Custom hooks — exported via index.ts
├── styles/
│   ├── main.scss
│   └── imports/
│       ├── _variables.scss   # CSS variables
│       ├── _mixins.scss      # Reusable SCSS mixins
│       ├── _reset.scss       # CSS reset
│       ├── _layout.scss      # Base layout
│       └── _utils.scss       # Utility classes
├── types/          # TypeScript types — exported via index.ts
├── utils/          # Helper functions — exported via index.ts
├── App.tsx
└── main.tsx
```

---

## Path Alias

`@` maps to `src/` — configured in both `tsconfig.app.json` and Vite via `vite-tsconfig-paths`.

```ts
import Button from '@/components/Button'
```

---

## Available SCSS Mixins

```scss
@include mid();               // Flexbox center
@include mid(false);          // Absolute center
@include overtext(2);         // Clamp text to N lines
@include customscroll(6px, #f0f0f0, #999);
@include maxW(768px) { ... }  // max-width media query
@include minW(1200px) { ... } // min-width media query
```

---

## Getting Started

```bash
# Install dependencies
yarn install

# Start dev server → http://localhost:5173
yarn dev
```

---

## Scripts

| Script | Description |
|---|---|
| `yarn dev` | Start dev server |
| `yarn build` | Type-check + production build → `dist/` |
| `yarn preview` | Preview production build locally |
| `yarn check:type` | TypeScript type check |
| `yarn check:lint` | ESLint with auto-fix |
| `yarn check:prettier` | Format all files |
| `yarn check:all` | Run all checks (Prettier → ESLint → TSC) |

---

## Git Hooks

On every `git commit`, Husky runs `yarn check:all` automatically. The commit is aborted if any check fails.

Hooks are installed automatically on `yarn install` via the `prepare` script.

`.husky/pre-commit`:
```sh
yarn check:all
```

---

## Configuration

### Prettier (`.prettierrc`)

```json
{
  "semi": false,
  "singleQuote": true,
  "jsxSingleQuote": true,
  "trailingComma": "none",
  "arrowParens": "always",
  "tabWidth": 2,
  "useTabs": false,
  "printWidth": 120
}
```

### TypeScript (`tsconfig.app.json`)

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "moduleResolution": "bundler",
    "jsx": "react-jsx",
    "baseUrl": ".",
    "paths": { "@/*": ["src/*"] },

    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noUncheckedIndexedAccess": true,
    "noImplicitOverride": true,
    "noFallthroughCasesInSwitch": true,

    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "skipLibCheck": true
  }
}
```

### Vite (`vite.config.ts`)

```ts
export default defineConfig({
  plugins: [
    react(),          // Fast Refresh + JSX transform
    tsconfigPaths()   // Resolve @/* alias from tsconfig
  ],
  resolve: {
    alias: { '@': path.resolve(__dirname, './src') }
  },
  build: {
    chunkSizeWarningLimit: 1000  // Warn if chunk > 1000KB
  }
})
```