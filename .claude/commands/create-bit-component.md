# Create Bit Component with UI SDK

Create a new Bit component that uses the `@ashok-atlan` shadcn-ui design system packages.

## Available UI Packages

All packages are published to GitHub Packages under `@ashok-atlan` scope:

### Utilities
| Package | Import |
|---------|--------|
| `@ashok-atlan/lib.utils` | `import { cn } from "@ashok-atlan/lib.utils"` |

### Foundation
| Package | Import |
|---------|--------|
| `@ashok-atlan/ui.theme-provider` | `import { ThemeProvider, useTheme } from "@ashok-atlan/ui.theme-provider"` |

### Form Components
| Package | Import |
|---------|--------|
| `@ashok-atlan/ui.button` | `import { Button, buttonVariants } from "@ashok-atlan/ui.button"` |
| `@ashok-atlan/ui.input` | `import { Input } from "@ashok-atlan/ui.input"` |
| `@ashok-atlan/ui.textarea` | `import { Textarea } from "@ashok-atlan/ui.textarea"` |
| `@ashok-atlan/ui.label` | `import { Label } from "@ashok-atlan/ui.label"` |
| `@ashok-atlan/ui.checkbox` | `import { Checkbox } from "@ashok-atlan/ui.checkbox"` |
| `@ashok-atlan/ui.switch` | `import { Switch } from "@ashok-atlan/ui.switch"` |
| `@ashok-atlan/ui.slider` | `import { Slider } from "@ashok-atlan/ui.slider"` |
| `@ashok-atlan/ui.radio-group` | `import { RadioGroup, RadioGroupItem } from "@ashok-atlan/ui.radio-group"` |
| `@ashok-atlan/ui.select` | `import { Select, SelectTrigger, SelectValue, SelectContent, SelectItem } from "@ashok-atlan/ui.select"` |
| `@ashok-atlan/ui.calendar` | `import { Calendar } from "@ashok-atlan/ui.calendar"` |

### Display Components
| Package | Import |
|---------|--------|
| `@ashok-atlan/ui.badge` | `import { Badge, badgeVariants } from "@ashok-atlan/ui.badge"` |
| `@ashok-atlan/ui.avatar` | `import { Avatar, AvatarImage, AvatarFallback } from "@ashok-atlan/ui.avatar"` |
| `@ashok-atlan/ui.skeleton` | `import { Skeleton } from "@ashok-atlan/ui.skeleton"` |
| `@ashok-atlan/ui.progress` | `import { Progress } from "@ashok-atlan/ui.progress"` |
| `@ashok-atlan/ui.separator` | `import { Separator } from "@ashok-atlan/ui.separator"` |

### Layout Components
| Package | Import |
|---------|--------|
| `@ashok-atlan/ui.card` | `import { Card, CardHeader, CardTitle, CardDescription, CardContent, CardFooter } from "@ashok-atlan/ui.card"` |
| `@ashok-atlan/ui.accordion` | `import { Accordion, AccordionItem, AccordionTrigger, AccordionContent } from "@ashok-atlan/ui.accordion"` |
| `@ashok-atlan/ui.tabs` | `import { Tabs, TabsList, TabsTrigger, TabsContent } from "@ashok-atlan/ui.tabs"` |
| `@ashok-atlan/ui.collapsible` | `import { Collapsible, CollapsibleTrigger, CollapsibleContent } from "@ashok-atlan/ui.collapsible"` |
| `@ashok-atlan/ui.table` | `import { Table, TableHeader, TableBody, TableRow, TableHead, TableCell } from "@ashok-atlan/ui.table"` |
| `@ashok-atlan/ui.scroll-area` | `import { ScrollArea, ScrollBar } from "@ashok-atlan/ui.scroll-area"` |

### Overlay Components
| Package | Import |
|---------|--------|
| `@ashok-atlan/ui.dialog` | `import { Dialog, DialogTrigger, DialogContent, DialogHeader, DialogTitle, DialogDescription, DialogFooter } from "@ashok-atlan/ui.dialog"` |
| `@ashok-atlan/ui.sheet` | `import { Sheet, SheetTrigger, SheetContent, SheetHeader, SheetTitle, SheetDescription } from "@ashok-atlan/ui.sheet"` |
| `@ashok-atlan/ui.popover` | `import { Popover, PopoverTrigger, PopoverContent } from "@ashok-atlan/ui.popover"` |
| `@ashok-atlan/ui.tooltip` | `import { Tooltip, TooltipTrigger, TooltipContent, TooltipProvider } from "@ashok-atlan/ui.tooltip"` |
| `@ashok-atlan/ui.alert-dialog` | `import { AlertDialog, AlertDialogTrigger, AlertDialogContent, AlertDialogHeader, AlertDialogTitle, AlertDialogDescription, AlertDialogFooter, AlertDialogAction, AlertDialogCancel } from "@ashok-atlan/ui.alert-dialog"` |

### Navigation Components
| Package | Import |
|---------|--------|
| `@ashok-atlan/ui.dropdown-menu` | `import { DropdownMenu, DropdownMenuTrigger, DropdownMenuContent, DropdownMenuItem } from "@ashok-atlan/ui.dropdown-menu"` |
| `@ashok-atlan/ui.context-menu` | `import { ContextMenu, ContextMenuTrigger, ContextMenuContent, ContextMenuItem } from "@ashok-atlan/ui.context-menu"` |
| `@ashok-atlan/ui.breadcrumb` | `import { Breadcrumb, BreadcrumbList, BreadcrumbItem, BreadcrumbLink, BreadcrumbSeparator } from "@ashok-atlan/ui.breadcrumb"` |
| `@ashok-atlan/ui.command` | `import { Command, CommandInput, CommandList, CommandEmpty, CommandGroup, CommandItem } from "@ashok-atlan/ui.command"` |

### Feedback Components
| Package | Import |
|---------|--------|
| `@ashok-atlan/ui.alert` | `import { Alert, AlertTitle, AlertDescription } from "@ashok-atlan/ui.alert"` |
| `@ashok-atlan/ui.sonner` | `import { Toaster } from "@ashok-atlan/ui.sonner"` |

## Creating a New Component

### Step 1: Create the Component

Ask me to create a component and specify:
- **Component name**: e.g., `user-profile-card`, `login-form`, `data-table`
- **Component type**: `ui` for UI components, `features` for feature components
- **UI packages needed**: Which `@ashok-atlan` packages to use

Example request:
> Create a `user-profile-card` component that uses Card, Avatar, Badge, and Button

### Step 2: Install Dependencies

After creating the component, install the required packages:

```bash
bit install @ashok-atlan/ui.card @ashok-atlan/ui.avatar @ashok-atlan/ui.badge @ashok-atlan/ui.button
```

Or install all UI packages at once:

```bash
bit install @ashok-atlan/lib.utils @ashok-atlan/ui.button @ashok-atlan/ui.card @ashok-atlan/ui.input @ashok-atlan/ui.label @ashok-atlan/ui.badge @ashok-atlan/ui.avatar @ashok-atlan/ui.dialog @ashok-atlan/ui.dropdown-menu @ashok-atlan/ui.tabs @ashok-atlan/ui.tooltip
```

### Step 3: Component Structure

New components will be created with this structure:

```
ui-sdk/{type}/{component-name}/
├── {component-name}.tsx           # Main component
├── {component-name}.compositions.tsx  # Visual examples
├── index.ts                       # Exports
```

## Example Component

Here's an example of a component using the UI SDK:

```tsx
import * as React from "react";
import { cn } from "@ashok-atlan/lib.utils";
import { Card, CardHeader, CardTitle, CardContent } from "@ashok-atlan/ui.card";
import { Avatar, AvatarImage, AvatarFallback } from "@ashok-atlan/ui.avatar";
import { Badge } from "@ashok-atlan/ui.badge";
import { Button } from "@ashok-atlan/ui.button";

export interface UserProfileCardProps {
  name: string;
  email: string;
  avatarUrl?: string;
  role: "admin" | "user" | "guest";
  onEdit?: () => void;
  className?: string;
}

export function UserProfileCard({
  name,
  email,
  avatarUrl,
  role,
  onEdit,
  className,
}: UserProfileCardProps) {
  return (
    <Card className={cn("w-[350px]", className)}>
      <CardHeader className="flex flex-row items-center gap-4">
        <Avatar>
          <AvatarImage src={avatarUrl} alt={name} />
          <AvatarFallback>{name.slice(0, 2).toUpperCase()}</AvatarFallback>
        </Avatar>
        <div className="flex flex-col">
          <CardTitle className="text-lg">{name}</CardTitle>
          <p className="text-sm text-muted-foreground">{email}</p>
        </div>
        <Badge variant={role === "admin" ? "default" : "secondary"} className="ml-auto">
          {role}
        </Badge>
      </CardHeader>
      <CardContent>
        <Button onClick={onEdit} variant="outline" className="w-full">
          Edit Profile
        </Button>
      </CardContent>
    </Card>
  );
}
```

## Publishing Your Component

After creating your component:

```bash
# Tag and publish
bit tag --message "Add user-profile-card component" --build

# Push to git
git add . && git commit -m "Add user-profile-card component"
git push
```

## Consumer Setup

To use these packages in another project:

### 1. Configure `.npmrc`

```ini
@ashok-atlan:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}
```

### 2. Install Packages

```bash
npm install @ashok-atlan/ui.button @ashok-atlan/ui.card
```

### 3. Import and Use

```tsx
import { Button } from "@ashok-atlan/ui.button";
import { Card, CardContent } from "@ashok-atlan/ui.card";

export function MyComponent() {
  return (
    <Card>
      <CardContent>
        <Button>Click me</Button>
      </CardContent>
    </Card>
  );
}
```

---

$ARGUMENTS
