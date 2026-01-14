# Setup Bit.dev with GitHub Packages

Set up a Bit.dev workspace that uses GitHub Packages as npm registry storage while Bit handles component resolution.

## Required Information

Before running this command, gather:
- **GitHub Organization/Username**: Your GitHub org or username for package scoping (e.g., `my-org`)
- **Bit Scope Name**: Name for your Bit scope (e.g., `ui-sdk`, `components`)
- **GitHub Token**: A GitHub PAT with `write:packages` and `read:packages` permissions

## Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                     How It Works                              │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  Bit Workspace                    GitHub Packages             │
│  ┌────────────────┐              ┌─────────────────┐         │
│  │ • Component    │   publish    │ • Package       │         │
│  │   resolution   │ ──────────►  │   storage       │         │
│  │ • Dependency   │              │ • npm install   │         │
│  │   graphs       │              │   endpoint      │         │
│  │ • Versioning   │              │                 │         │
│  └────────────────┘              └─────────────────┘         │
│                                                               │
│  Component ID: {github-org}.{scope}/ui/button                │
│  Package Name: @{github-org}/ui.button                       │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

## Setup Steps

### 1. Initialize the Workspace

Create a new Bit workspace or initialize in existing project:

```bash
# New workspace
npx @teambit/bvm install
bit new react my-workspace --default-scope {github-org}.{scope}
cd my-workspace

# Or initialize in existing project
bit init --default-scope {github-org}.{scope}
```

### 2. Configure workspace.jsonc

Update `workspace.jsonc` with GitHub Packages configuration:

```json
{
  "$schema": "https://static.bit.dev/teambit/schemas/schema.json",
  "teambit.workspace/workspace": {
    "name": "{scope}",
    "defaultDirectory": "{scope}/{componentType}/{name}",
    "defaultScope": "{github-org}.{scope}"
  },
  "teambit.workspace/variants": {
    "*": {
      "teambit.pkg/pkg": {
        "packageJson": {
          "name": "@{github-org}/{name}",
          "publishConfig": {
            "registry": "https://npm.pkg.github.com"
          },
          "repository": {
            "type": "git",
            "url": "https://github.com/{github-org}/{repo-name}.git"
          }
        },
        "packageManagerPublishArgs": ["--access=public"]
      }
    }
  },
  "teambit.dependencies/dependency-resolver": {
    "packageManager": "teambit.dependencies/pnpm",
    "policy": {
      "dependencies": {},
      "peerDependencies": {}
    }
  }
}
```

### 3. Configure .npmrc

Create `.npmrc` for GitHub Packages authentication:

```ini
# GitHub Packages registry for your org
@{github-org}:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}

# Bit Cloud registry for teambit dependencies
@teambit:registry=https://node-registry.bit.cloud
@bitdev:registry=https://node-registry.bit.cloud
```

### 4. Set Environment Variable

```bash
# Add to your shell profile (.bashrc, .zshrc, etc.)
export GITHUB_TOKEN="your_github_pat_here"
```

### 5. Install Dependencies

```bash
bit install
```

## Creating Components

```bash
# Create a new component
bit create react ui/button

# Create a utility
bit create node utils/helpers
```

## Publishing Workflow

```bash
# 1. Build and tag components
bit tag --all --message "Initial release"

# 2. Export to Bit scope (if using remote scope)
bit export

# Components are automatically published to GitHub Packages during tag
```

## Consuming Components

In any project, configure `.npmrc`:

```ini
@{github-org}:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}
```

Then install:

```bash
npm install @{github-org}/ui.button
```

## Package Name Mapping

| Component ID | Package Name |
|--------------|--------------|
| `{org}.{scope}/ui/button` | `@{org}/ui.button` |
| `{org}.{scope}/utils/cn` | `@{org}/utils.cn` |
| `{org}.{scope}/hooks/use-toggle` | `@{org}/hooks.use-toggle` |

## Troubleshooting

### Authentication Issues
- Ensure `GITHUB_TOKEN` is set with `write:packages` permission
- Verify token is not expired
- Check `.npmrc` has correct registry URL

### Package Name Conflicts
- GitHub Packages requires lowercase names
- Package scope must match GitHub org/username exactly

### Bit Cloud Dependencies
- Some Bit aspects require `@teambit` packages
- Keep the teambit registry configuration in `.npmrc`

## Files Created

- `workspace.jsonc` - Bit workspace configuration
- `.npmrc` - npm registry configuration
- `.bitmap` - Component tracking (auto-generated)

---

$ARGUMENTS
