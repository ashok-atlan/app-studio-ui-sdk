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

## Discovering Available Packages

To see all published packages:

```bash
# List all @ashok-atlan packages
npm search @ashok-atlan --registry=https://npm.pkg.github.com
```

Or visit: https://github.com/ashok-atlan?tab=packages

## Component Structure

New components will be created at `ui-sdk/{type}/{name}/`:

```
ui-sdk/{type}/{component-name}/
├── {component-name}.tsx              # Main component
├── {component-name}.compositions.tsx # Visual examples for Bit UI
├── index.ts                          # Public exports
```

## Installing Dependencies

After identifying which packages you need:

```bash
# Install specific packages
bit install @ashok-atlan/package-name

# Install multiple packages
bit install @ashok-atlan/ui.button @ashok-atlan/ui.card @ashok-atlan/lib.utils
```

## Publishing Your Component

```bash
# Tag and publish to GitHub Packages
bit tag --message "Add component-name" --build

# Commit and push
git add . && git commit -m "Add component-name"
git push
```

## Using Packages in Other Projects

### 1. Configure `.npmrc`

```ini
@ashok-atlan:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}
```

### 2. Install and Import

```bash
npm install @ashok-atlan/package-name
```

```tsx
import { Something } from "@ashok-atlan/package-name";
```

---

$ARGUMENTS
