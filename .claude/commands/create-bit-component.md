# Create Bit Component

Create a new Bit component that uses packages from the `@ashok-atlan` scope on GitHub Packages.

## How to Use

Tell me what component you want to create and what packages it should use. I will:

1. Create the component with proper structure
2. Install the required `@ashok-atlan/*` dependencies
3. Set up the component with proper imports and exports

## Example Requests

```
Create a user-card component using @ashok-atlan/ui.card and @ashok-atlan/ui.avatar
```

```
Create a form-field component that wraps @ashok-atlan/ui.input with @ashok-atlan/ui.label
```

```
Create a data-table component using @ashok-atlan/ui.table, @ashok-atlan/ui.button, and @ashok-atlan/lib.utils
```

---

## Step-by-Step: Creating a New Component

### Step 1: Create Component Directory

```bash
# Create the component structure
mkdir -p ui-sdk/ui/{component-name}
```

### Step 2: Create Component Files

```
ui-sdk/ui/{component-name}/
├── {component-name}.tsx              # Main component
├── {component-name}.compositions.tsx # Visual examples for Bit UI
└── index.ts                          # Public exports
```

### Step 3: Install Dependencies

```bash
# Install packages from @ashok-atlan scope
bit install @ashok-atlan/ui.button @ashok-atlan/ui.card @ashok-atlan/lib.utils
```

### Step 4: Preview Changes

```bash
# Start Bit dev server
bit start

# Open http://localhost:3000 to view your component
```

### Step 5: Publish

```bash
# Tag and publish to GitHub Packages
bit tag --message "Add {component-name}" --build

# Export to Bit Cloud marketplace
bit export

# Commit and push
git add .
git commit -m "Add {component-name} component"
git push
```

---

## Component Template

### Main Component (`{component-name}.tsx`)

```tsx
import * as React from "react";
import { cn } from "@ashok-atlan/lib.utils";
// Import other @ashok-atlan packages as needed

export interface {ComponentName}Props {
  className?: string;
  children?: React.ReactNode;
}

export function {ComponentName}({
  className,
  children,
  ...props
}: {ComponentName}Props) {
  return (
    <div className={cn("your-styles", className)} {...props}>
      {children}
    </div>
  );
}
```

### Compositions (`{component-name}.compositions.tsx`)

```tsx
import React from "react";
import { {ComponentName} } from "./{component-name}";

export const Basic{ComponentName} = () => (
  <{ComponentName}>
    Example content
  </{ComponentName}>
);

export const {ComponentName}WithProps = () => (
  <{ComponentName} className="custom-class">
    With custom props
  </{ComponentName}>
);
```

### Index (`index.ts`)

```ts
export { {ComponentName} } from "./{component-name}";
export type { {ComponentName}Props } from "./{component-name}";
```

---

## Where to Add Components

```
ui-sdk/
├── lib/                    # Utilities and helpers
│   └── utils/              # cn() function, etc.
│
└── ui/                     # UI Components
    ├── button/             # Existing: Button component
    ├── card/               # Existing: Card component
    ├── dialog/             # Existing: Dialog component
    ├── ...
    └── {your-component}/   # NEW: Add your component here
```

---

## Discovering Available Packages

```bash
# List all @ashok-atlan packages
npm search @ashok-atlan --registry=https://npm.pkg.github.com
```

Or visit: https://github.com/ashok-atlan?tab=packages

---

## Publishing Checklist

Before publishing, ensure:

- [ ] Component works in `bit start` preview
- [ ] Compositions show different use cases
- [ ] Exports are correct in `index.ts`
- [ ] No TypeScript errors (`bit compile`)

Then publish:

```bash
# 1. Tag and publish to GitHub Packages (npm registry)
bit tag --message "Add component-name" --build

# 2. Export to Bit Cloud (marketplace)
bit export

# 3. Commit and push to Git
git add . && git commit -m "Add component-name"
git push
```

---

## Using in Other Projects

### Install from GitHub Packages

```bash
# Add to .npmrc
@ashok-atlan:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}

# Install
npm install @ashok-atlan/{component-name}
```

### Install from Bit Cloud

```bash
bit install ashok-atlan.ui-sdk/ui/{component-name}
```

### Import and Use

```tsx
import { ComponentName } from "@ashok-atlan/ui.{component-name}";

function App() {
  return <ComponentName>Hello</ComponentName>;
}
```

---

$ARGUMENTS
