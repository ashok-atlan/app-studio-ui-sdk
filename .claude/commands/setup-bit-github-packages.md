# Setup Bit.dev with GitHub Packages

Set up a Bit.dev workspace that uses GitHub Packages as npm registry storage while Bit handles component resolution.

## Quick Start (Using This Template)

### Step 1: Clone the Template

```bash
# Clone the template repository
git clone https://github.com/ashok-atlan/app-studio-ui-sdk.git my-ui-sdk
cd my-ui-sdk

# Remove git history and start fresh
rm -rf .git
git init
```

### Step 2: Update Configuration

Update `workspace.jsonc` with your organization details:

```json
{
  "teambit.workspace/workspace": {
    "name": "your-scope-name",
    "defaultDirectory": "ui-sdk/{name}",
    "defaultScope": "your-github-org.your-scope-name"
  },
  "teambit.workspace/variants": {
    "*": {
      "teambit.pkg/pkg": {
        "packageJson": {
          "name": "@your-github-org/{name}",
          "publishConfig": {
            "registry": "https://npm.pkg.github.com"
          },
          "repository": {
            "type": "git",
            "url": "https://github.com/your-github-org/your-repo-name.git"
          }
        }
      }
    }
  }
}
```

### Step 3: Configure Authentication

Update `.npmrc` with your GitHub org:

```ini
@your-github-org:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}

@teambit:registry=https://node-registry.bit.cloud
@bitdev:registry=https://node-registry.bit.cloud
```

Also copy to home directory for global access:

```bash
cp .npmrc ~/.npmrc
```

### Step 4: Set Environment Variable

```bash
# Add to your shell profile (.bashrc, .zshrc, etc.)
export GITHUB_TOKEN="your_github_pat_here"
```

### Step 5: Install Dependencies

```bash
bit install
```

### Step 6: Verify Setup

```bash
# Start the dev server
bit start

# Open http://localhost:3000 to view components
```

---

## Starting From Scratch

If you prefer to start fresh instead of using the template:

### 1. Initialize the Workspace

```bash
npx @teambit/bvm install
bit new react my-workspace --default-scope {github-org}.{scope}
cd my-workspace
```

### 2. Configure workspace.jsonc

```json
{
  "$schema": "https://static.bit.dev/teambit/schemas/schema.json",
  "teambit.workspace/workspace": {
    "name": "{scope}",
    "defaultDirectory": "ui-sdk/{name}",
    "defaultScope": "{github-org}.{scope}"
  },
  "teambit.workspace/variants": {
    "{ui/**}, {lib/**}": {
      "teambit.react/react": {}
    },
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

```ini
@{github-org}:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}

@teambit:registry=https://node-registry.bit.cloud
@bitdev:registry=https://node-registry.bit.cloud
```

---

## Directory Structure

```
my-ui-sdk/
├── workspace.jsonc          # Bit workspace configuration
├── .npmrc                   # npm registry configuration
├── .bitmap                  # Component tracking (auto-generated)
├── ui-sdk/
│   ├── lib/                 # Utility libraries
│   │   └── utils/           # cn() helper, etc.
│   └── ui/                  # UI components
│       ├── button/
│       ├── card/
│       ├── dialog/
│       └── ...
└── .claude/
    └── commands/            # Claude Code commands
```

## Where to Add UI Changes

### Adding a New Component

```
ui-sdk/ui/{component-name}/
├── {component-name}.tsx              # Main component code
├── {component-name}.compositions.tsx # Visual examples for Bit UI
└── index.ts                          # Public exports
```

### Modifying Existing Components

1. Find the component in `ui-sdk/ui/{component-name}/`
2. Edit the `.tsx` file
3. Update compositions if needed
4. Run `bit start` to preview changes

### Adding Utilities

```
ui-sdk/lib/{util-name}/
├── {util-name}.ts           # Utility code
└── index.ts                 # Public exports
```

---

## Publishing Workflow

### Step 1: Publish to GitHub Packages (npm)

```bash
# Tag and build all components
bit tag --message "Release description" --build

# Verify packages are published
# Check: https://github.com/{org}?tab=packages
```

### Step 2: Export to Bit Cloud (Marketplace)

```bash
# First, create a scope on bit.cloud (one-time setup)
# Visit: https://bit.cloud and create a scope

# Login to Bit Cloud
bit login

# Export components to Bit Cloud marketplace
bit export
```

### Step 3: Commit and Push to Git

```bash
git add .
git commit -m "Release: description of changes"
git push
```

### Complete Release Workflow

```bash
# 1. Make your changes
# 2. Test locally with `bit start`

# 3. Tag, build, and publish to GitHub Packages
bit tag --message "v1.0.0 - Feature description" --build

# 4. Export to Bit Cloud marketplace
bit export

# 5. Commit and push
git add .
git commit -m "v1.0.0 - Feature description"
git push
```

---

## Package Name Mapping

| Component ID | npm Package | Bit Cloud ID |
|--------------|-------------|--------------|
| `{org}.{scope}/ui/button` | `@{org}/ui.button` | `{org}.{scope}/ui/button` |
| `{org}.{scope}/lib/utils` | `@{org}/lib.utils` | `{org}.{scope}/lib/utils` |

---

## Consuming Published Components

### From GitHub Packages (npm)

```bash
# Configure .npmrc in consumer project
echo "@{org}:registry=https://npm.pkg.github.com" >> .npmrc

# Install
npm install @{org}/ui.button @{org}/ui.card
```

### From Bit Cloud Marketplace

```bash
# Configure Bit in consumer project
bit init

# Install from Bit Cloud
bit install @{org}/{scope}/ui/button
```

---

## Troubleshooting

### Authentication Issues
- Ensure `GITHUB_TOKEN` is set with `write:packages` permission
- Copy `.npmrc` to home directory: `cp .npmrc ~/.npmrc`
- Verify: `npm whoami --registry=https://npm.pkg.github.com`

### Bit Cloud Export Issues
- Run `bit login` to authenticate
- Ensure scope exists on bit.cloud
- Check scope permissions

### Package Name Conflicts
- GitHub Packages requires lowercase names
- Package scope must match GitHub org/username exactly

---

$ARGUMENTS
