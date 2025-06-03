---
description:
globs:
alwaysApply: true
---
You are an expert in Laravel, PHP, Livewire, Alpine.js, TailwindCSS, and Flux UI.

    Key Principles

    - Write concise, technical responses with accurate PHP and Livewire examples.
    - Focus on component-based architecture using Livewire and Laravel's latest features.
    - Follow Laravel and Livewire best practices and conventions.
    - Use object-oriented programming with a focus on SOLID principles.
    - Prefer iteration and modularization over duplication.
    - Use descriptive variable, method, and component names.
    - Use lowercase with dashes for directories (e.g., app/Http/Livewire).
    - Favor dependency injection and service containers.

    PHP/Laravel

    - Use PHP 8.1+ features when appropriate (e.g., typed properties, match expressions).
    - Follow PSR-12 coding standards.
    - Use strict typing: `declare(strict_types=1);`
    - Utilize Laravel 11's built-in features and helpers when possible.
    - Implement proper error handling and logging:
      - Use Laravel's exception handling and logging features.
      - Create custom exceptions when necessary.
      - Use try-catch blocks for expected exceptions.
    - Use Laravel's validation features for form and request validation.
    - Implement middleware for request filtering and modification.
    - Utilize Laravel's Eloquent ORM for database interactions.
    - Use Laravel's query builder for complex database queries.
    - Implement proper database migrations and seeders.

    Livewire

    - Use Livewire for dynamic components and real-time user interactions.
    - Favor the use of Livewire's lifecycle hooks and properties.
    - Use the latest Livewire (3.5+) features for optimization and reactivity.
    - Implement Blade components with Livewire directives (e.g., wire:model).
    - Handle state management and form handling using Livewire properties and actions.
    - Use wire:loading and wire:target to provide feedback and optimize user experience.
    - Apply Livewire's security measures for components.

    Flux UI

    - Use Flux UI components as the primary UI building blocks.
    - Follow Flux's component-based approach for consistent design.
    - Leverage Flux's pre-built components before creating custom ones.
    - Use Flux's CSS variable system for theming.
    - Implement dark mode using Flux's built-in support.
    - Follow Flux's accessibility guidelines.
    - Use Flux Pro components where available for advanced features.

    Dependencies

    - Laravel 11 (latest stable version)
    - Livewire 3.5+ for real-time, reactive components
    - Alpine.js for lightweight JavaScript interactions
    - Tailwind CSS for utility-first styling
    - Flux UI 2.x Pro for pre-built UI components and themes
    - Composer for dependency management
    - NPM/Yarn for frontend dependencies

# Flux UI Documentation# Flux UI Documentation - Core Components

## Getting Started & Installation

### Overview

Flux is a robust, hand-crafted UI component library for Livewire applications. It's built using Tailwind CSS and provides a set of components that are easy to use and customize.

**Note**: Starting a new project? Flux comes baked into the new [Livewire starter kit](https://laravel.com/docs/12.x/starter-kits#livewire).

### Prerequisites

Flux requires the following before installing:

1. **Laravel**: Version 10 or later
2. **Livewire**: Version 3.5.19 or later  
3. **Tailwind CSS**: Version 4 or later

### Installation Process

#### Step 1: Install Flux

Install Flux via composer from your project root:

```bash
composer require livewire/flux
```

#### Step 2: Install Flux Pro (Optional)

If you have purchased a Flux Pro license, you can install it using:

```bash
php artisan flux:activate
```

During the activation process, you will be prompted to enter:
- Your email address
- Your license key

**Important Notes about Flux Pro**:
- The command creates an `auth.json` file in your project's root directory
- This file contains your email and license key for downloading and installing Flux
- **Do not add `auth.json` to version control**
- You'll need to manually recreate it in every new project environment
- View your licenses and install instructions at `/dashboard`

#### Step 3: Include Flux Assets

Add the `@fluxAppearance` and `@fluxScripts` Blade directives to your layout file:

```blade
<head>
    ...
    @fluxAppearance
</head>
<body>
    ...
    @fluxScripts
</body>
```

#### Step 4: Set up Tailwind CSS

**Important**: Flux v2.0 requires Tailwind CSS v4.0 or later.

Add the following configuration to your `resources/css/app.css` file:

```css
@import 'tailwindcss';
@import '../../vendor/livewire/flux/dist/flux.css';

@custom-variant dark (&:where(.dark, .dark *));
```

If you don't have Tailwind installed, follow the [Tailwind installation guide for Laravel](https://tailwindcss.com/docs/guides/laravel).

#### Step 5: Use the Inter Font Family (Optional but Recommended)

Add the following to the `<head>` tag in your layout file:

```html
<head>
    ...
    <link rel="preconnect" href="https://fonts.bunny.net">
    <link href="https://fonts.bunny.net/css?family=inter:400,500,600&display=swap" rel="stylesheet" />
</head>
```

Configure Tailwind to use this font family in your `resources/css/app.css` file:

```css
@import 'tailwindcss';
@import '../../vendor/livewire/flux/dist/flux.css';

...

@theme {
    --font-sans: Inter, sans-serif;
}
```

### Configuration Options

#### Dark Mode

By default, Flux handles the appearance of your application by adding a `dark` class to the `html` element based on:
- User's system preference
- Selected appearance

To disable automatic dark mode handling, remove the `@fluxAppearance` directive from your layout file:

```blade
<head>
    ...
    {{-- @fluxAppearance --}}
</head>
```

#### Publishing Components

To customize specific Flux components, publish their blade files into your project:

```bash
php artisan flux:publish
```

Options:
- You'll be prompted to search and select which components to publish
- Use the `--all` flag to publish all components at once

#### Keeping Flux Updated

Regularly update your composer dependencies:

```bash
composer update livewire/flux livewire/flux-pro
```

**Important**: If you've published Flux components, check the [changelog](https://github.com/livewire/flux/releases) for breaking changes before updating.

### Environment-Specific Installation

#### Laravel Forge

To authenticate Flux using Laravel Forge's Packages feature:

1. Navigate to the packages page (server or site level)
2. Click "Add Credential"
3. Enter the following details:
   - **Repository URL**: `composer.fluxui.dev`
   - **Username**: Your Flux account email
   - **Password**: Your Flux license key
4. Click "Save"

You can now install Flux using `composer require livewire/flux-pro`.

#### Laravel Cloud

To authenticate Flux in Laravel Cloud:

1. Open your environment and go to "Settings" → "Deployments"
2. In the "Build Commands" section, add the following command above `composer install`:

```bash
composer config http-basic.composer.fluxui.dev your-email your-license-key
```

Replace `your-email` and `your-license-key` with your actual credentials.

#### GitHub Actions

To use Flux in GitHub Actions:

1. Add repository secrets in **Settings > Secrets and variables > Actions**:
   - `FLUX_USERNAME` – Your Flux account email
   - `FLUX_LICENSE_KEY` – Your Flux license key

2. Add to your workflow before `composer install`:

```yaml
- name: Add Flux license
  run: composer config http-basic.composer.fluxui.dev "${{ secrets.FLUX_USERNAME }}" "${{ secrets.FLUX_LICENSE_KEY }}"
```

#### Generic CI Environments

For CI environments without an `auth.json` file:

```bash
composer config http-basic.composer.fluxui.dev "${FLUX_USERNAME}" "${FLUX_LICENSE_KEY}"
```

### Server Configuration

#### Nginx Configuration

If you encounter issues loading Flux's JavaScript and CSS assets, add the following to your nginx configuration:

```nginx
location ~ ^/flux/flux(\.min)?\.(js|css)$ {
    expires off;
    try_files $uri $uri/ /index.php?$query_string;
}
```

**Note**: By default, Flux exposes two routes for serving assets:
- `/flux/flux.js`
- `/flux/flux.css`

### Asset Routes

Flux automatically handles serving its assets through these routes:
- **JavaScript**: `/flux/flux.js`
- **CSS**: `/flux/flux.css`

These routes are registered automatically when Flux is installed and don't require manual configuration in most cases.

### Additional Resources

- [Theming Documentation](/docs/theming) - Learn about customizing Flux's appearance
- [Dark Mode Documentation](/docs/dark-mode) - Detailed dark mode configuration
- [Customization Documentation](/docs/customization) - Advanced component customization
- [Laravel Forge Packages Documentation](https://forge.laravel.com/docs/sites/packages.html)
- [Laravel Cloud Private Composer Packages](https://cloud.laravel.com/docs/environments#private-composer-packages)
- [Flux Release Notes](https://github.com/livewire/flux/releases)

## Layout Components

Flux UI provides two main layout components that help structure your application with consistent navigation patterns.

### flux:header

A full-width top navigation layout component for your application.

#### Props

| Prop | Description |
|------|-------------|
| `sticky` | When present, makes the header sticky when scrolling |
| `container` | When present, constrains the header content to a container width |

#### Slots

| Slot | Description |
|------|-------------|
| `default` | Content to display within the header, typically including branding, navigation, and user profile elements |

#### CSS Classes

| Property | Description |
|----------|-------------|
| `class` | Additional CSS classes applied to the header. Common uses: `bg-zinc-50`, `border-b`, `sticky`, etc. |

#### Example Usage

```blade
<flux:header class="bg-white dark:bg-zinc-900 border-b border-zinc-200 dark:border-zinc-700">
    <flux:brand href="#" logo="/img/logo.png" name="Acme Inc." />
    
    <flux:navbar>
        <flux:navbar.item href="#">Home</flux:navbar.item>
        <flux:navbar.item href="#">Products</flux:navbar.item>
        <flux:navbar.item href="#">About</flux:navbar.item>
    </flux:navbar>
    
    <flux:spacer />
    
    <flux:profile avatar="/img/user.png" name="John Doe" />
</flux:header>
```

### flux:sidebar

A sidebar navigation layout component that keeps your application content front and center.

#### Props

| Prop | Description |
|------|-------------|
| `sticky` | When present, makes the sidebar sticky when scrolling |
| `stashable` | When present, allows the sidebar to be toggled on/off on smaller screens |

#### Slots

| Slot | Description |
|------|-------------|
| `default` | Content to display within the sidebar, typically including branding, navigation elements, and user profile |

#### CSS Classes

| Property | Description |
|----------|-------------|
| `class` | Additional CSS classes applied to the sidebar. Common uses: `bg-zinc-50`, `border-r`, etc. |

#### Example Usage

```blade
<flux:sidebar sticky stashable class="bg-zinc-50 dark:bg-zinc-900 border-r border-zinc-200 dark:border-zinc-700">
    <flux:sidebar.toggle class="lg:hidden" icon="x-mark" />
    
    <flux:brand href="#" logo="/img/logo.png" name="Acme Inc." />
    
    <flux:input as="button" variant="filled" placeholder="Search..." icon="magnifying-glass" />
    
    <flux:navlist variant="outline">
        <flux:navlist.item icon="home" href="#" current>Home</flux:navlist.item>
        <flux:navlist.item icon="inbox" badge="12" href="#">Inbox</flux:navlist.item>
        <flux:navlist.item icon="document-text" href="#">Documents</flux:navlist.item>
        <flux:navlist.item icon="calendar" href="#">Calendar</flux:navlist.item>
        
        <flux:navlist.group expandable heading="Favorites">
            <flux:navlist.item href="#">Marketing site</flux:navlist.item>
            <flux:navlist.item href="#">Android app</flux:navlist.item>
            <flux:navlist.item href="#">Brand guidelines</flux:navlist.item>
        </flux:navlist.group>
    </flux:navlist>
    
    <flux:spacer />
    
    <flux:dropdown position="top" align="start">
        <flux:profile avatar="/img/user.png" name="Olivia Martin" />
        
        <flux:menu>
            <flux:menu.item icon="cog-6-tooth">Settings</flux:menu.item>
            <flux:menu.separator />
            <flux:menu.item icon="arrow-right-start-on-rectangle">Logout</flux:menu.item>
        </flux:menu>
    </flux:dropdown>
</flux:sidebar>
```

### flux:sidebar.toggle

A toggle button component used to show/hide the sidebar on mobile devices.

#### Attributes

| Attribute | Description |
|-----------|-------------|
| `icon` | The icon to display in the toggle button (e.g., `bars-2`, `x-mark`) |
| `inset` | Positioning of the toggle button (e.g., `left`) |

#### CSS Classes

| Property | Description |
|----------|-------------|
| `class` | Additional CSS classes applied to the toggle button. Common uses: `lg:hidden` to show only on mobile |

#### Example Usage

```blade
<!-- Inside sidebar for closing -->
<flux:sidebar.toggle class="lg:hidden" icon="x-mark" />

<!-- Inside header for opening -->
<flux:sidebar.toggle class="lg:hidden" icon="bars-2" inset="left" />
```

### flux:main

A main content area component that works alongside the header and sidebar layouts.

#### Props

| Prop | Description |
|------|-------------|
| `container` | When present, constrains the main content to a container width |

#### Slots

| Slot | Description |
|------|-------------|
| `default` | Content to display within the main content area |

#### Example Usage

```blade
<flux:main>
    <flux:heading size="xl" level="1">Good afternoon, Olivia</flux:heading>
    <flux:text class="mb-6 mt-2 text-base">Here's what's new today</flux:text>
    
    <flux:separator variant="subtle" />
    
    <!-- Your main content here -->
</flux:main>
```

### Complete Layout Examples

#### Header Layout

```blade
<!DOCTYPE html>
<html>
<head>
    <!-- ... -->
    @fluxAppearance
</head>
<body class="min-h-screen bg-white dark:bg-zinc-800">
    <flux:header sticky class="bg-white dark:bg-zinc-900 border-b">
        <flux:brand href="/" logo="/img/logo.png" name="Acme Inc." />
        
        <flux:navbar>
            <flux:navbar.item href="#" current>Dashboard</flux:navbar.item>
            <flux:navbar.item href="#">Projects</flux:navbar.item>
            <flux:navbar.item href="#">Team</flux:navbar.item>
        </flux:navbar>
        
        <flux:spacer />
        
        <flux:dropdown>
            <flux:profile avatar="/img/user.png" />
            <flux:menu>
                <flux:menu.item icon="cog-6-tooth">Settings</flux:menu.item>
                <flux:menu.item icon="arrow-right-start-on-rectangle">Logout</flux:menu.item>
            </flux:menu>
        </flux:dropdown>
    </flux:header>
    
    <flux:main container>
        {{ $slot }}
    </flux:main>
    
    @fluxScripts
</body>
</html>
```

#### Sidebar Layout

```blade
<!DOCTYPE html>
<html>
<head>
    <!-- ... -->
    @fluxAppearance
</head>
<body class="min-h-screen bg-white dark:bg-zinc-800">
    <flux:sidebar sticky stashable class="bg-zinc-50 dark:bg-zinc-900 border-r">
        <flux:sidebar.toggle class="lg:hidden" icon="x-mark" />
        
        <flux:brand href="/" logo="/img/logo.png" name="Acme Inc." />
        
        <flux:navlist variant="outline">
            <flux:navlist.item icon="home" href="#" current>Home</flux:navlist.item>
            <flux:navlist.item icon="inbox" badge="12" href="#">Inbox</flux:navlist.item>
            <flux:navlist.item icon="document-text" href="#">Documents</flux:navlist.item>
        </flux:navlist>
        
        <flux:spacer />
        
        <flux:profile avatar="/img/user.png" name="John Doe" />
    </flux:sidebar>
    
    <!-- Mobile header -->
    <flux:header class="lg:hidden">
        <flux:sidebar.toggle icon="bars-2" inset="left" />
        <flux:spacer />
        <flux:profile avatar="/img/user.png" />
    </flux:header>
    
    <flux:main>
        {{ $slot }}
    </flux:main>
    
    @fluxScripts
</body>
</html>
```

#### Header with Secondary Sidebar

```blade
<!DOCTYPE html>
<html>
<head>
    <!-- ... -->
    @fluxAppearance
</head>
<body class="min-h-screen bg-white dark:bg-zinc-800">
    <flux:header sticky container>
        <flux:brand href="/" logo="/img/logo.png" name="Acme Inc." />
        <flux:spacer />
        <flux:profile avatar="/img/user.png" name="John Doe" />
    </flux:header>
    
    <div class="flex">
        <flux:sidebar class="bg-zinc-50 dark:bg-zinc-900 border-r">
            <flux:navlist variant="outline">
                <flux:navlist.item icon="home" href="#" current>Overview</flux:navlist.item>
                <flux:navlist.item icon="chart-bar" href="#">Analytics</flux:navlist.item>
                <flux:navlist.item icon="users" href="#">Team</flux:navlist.item>
            </flux:navlist>
        </flux:sidebar>
        
        <flux:main class="flex-1">
            {{ $slot }}
        </flux:main>
    </div>
    
    @fluxScripts
</body>
</html>
```

### Layout Component Best Practices

1. **Responsive Design**: Always include mobile toggles when using sidebars
2. **Dark Mode**: Add appropriate dark mode classes to maintain consistency
3. **Sticky Navigation**: Use the `sticky` prop for better UX on long pages
4. **Container Width**: Use the `container` prop on `flux:main` to maintain readable content width
5. **Spacers**: Use `flux:spacer` to push elements to opposite ends in headers/sidebars
6. **Consistent Styling**: Apply border and background classes for visual separation

## Navigation Components

### flux:navbar
A horizontal navigation container for arranging navigation links side by side.

**Props:**
- None specific to the navbar component

**Slots:**
- `default`: The navigation items

**Attributes:**
- `data-flux-navbar`: Applied to the root element for styling and identification

**Example:**
```blade
<flux:navbar>
    <flux:navbar.item href="/dashboard">Dashboard</flux:navbar.item>
    <flux:navbar.item href="/users">Users</flux:navbar.item>
    <flux:navbar.item href="/settings">Settings</flux:navbar.item>
</flux:navbar>
```

### flux:navbar.item
Individual navigation item within a navbar.

**Props:**
- `href`: URL the item links to
- `current`: If true, applies active styling (auto-detected based on current URL if not specified)
- `icon`: Name of the icon to display at the start of the item
- `icon:trailing`: Name of the icon to display at the end of the item
- `badge`: Text or number to display as a badge
- `badge-color`: Color for the badge (e.g., 'lime', 'red', etc.)

**Attributes:**
- `data-current`: Applied when the item is active/current

**Examples:**
```blade
<!-- Basic navigation -->
<flux:navbar.item href="{{ route('home') }}">Home</flux:navbar.item>

<!-- With icon -->
<flux:navbar.item href="/dashboard" icon="home">Dashboard</flux:navbar.item>

<!-- With badge -->
<flux:navbar.item href="/inbox" badge="12">Inbox</flux:navbar.item>
<flux:navbar.item href="/calendar" badge="Pro" badge-color="lime">Calendar</flux:navbar.item>

<!-- Manual current state -->
<flux:navbar.item href="/" :current="request()->is('/')">Home</flux:navbar.item>

<!-- Dropdown navigation -->
<flux:dropdown>
    <flux:navbar.item icon:trailing="chevron-down">Account</flux:navbar.item>
    <flux:navmenu>
        <flux:navmenu.item href="/profile">Profile</flux:navmenu.item>
        <flux:navmenu.item href="/settings">Settings</flux:navmenu.item>
        <flux:navmenu.item href="/billing">Billing</flux:navmenu.item>
    </flux:navmenu>
</flux:dropdown>
```

### flux:navlist
A vertical navigation container (sidebar navigation).

**Props:**
- None specific to the navlist component

**Slots:**
- `default`: The navigation items and groups

**Attributes:**
- `data-flux-navlist`: Applied to the root element for styling and identification

**Example:**
```blade
<flux:navlist class="w-64">
    <flux:navlist.item href="/home" icon="home">Home</flux:navlist.item>
    <flux:navlist.item href="/features" icon="puzzle-piece">Features</flux:navlist.item>
    <flux:navlist.item href="/pricing" icon="currency-dollar">Pricing</flux:navlist.item>
</flux:navlist>
```

### flux:navlist.item
Individual navigation item within a navlist.

**Props:**
- `href`: URL the item links to
- `current`: If true, applies active styling (auto-detected based on current URL if not specified)
- `icon`: Name of the icon to display at the start of the item
- `badge`: Text or number to display as a badge
- `badge-color`: Color for the badge

**Attributes:**
- `data-current`: Applied when the item is active/current

**Examples:**
```blade
<!-- With badges -->
<flux:navlist class="w-64">
    <flux:navlist.item href="/home" icon="home">Home</flux:navlist.item>
    <flux:navlist.item href="/inbox" icon="envelope" badge="12">Inbox</flux:navlist.item>
    <flux:navlist.item href="/calendar" icon="calendar-days" badge="Pro" badge-color="lime">Calendar</flux:navlist.item>
</flux:navlist>
```

### flux:navlist.group
Groups related navigation items together with optional heading.

**Props:**
- `heading`: Text displayed as the group heading
- `expandable`: If true, makes the group collapsible
- `expanded`: If true, expands the group by default when expandable (default: true)

**Slots:**
- `default`: The group's navigation items

**Examples:**
```blade
<!-- Basic group -->
<flux:navlist>
    <flux:navlist.group heading="Account" class="mt-4">
        <flux:navlist.item href="/profile">Profile</flux:navlist.item>
        <flux:navlist.item href="/settings">Settings</flux:navlist.item>
        <flux:navlist.item href="/billing">Billing</flux:navlist.item>
    </flux:navlist.group>
</flux:navlist>

<!-- Collapsible group -->
<flux:navlist class="w-64">
    <flux:navlist.item href="/dashboard" icon="home">Dashboard</flux:navlist.item>
    <flux:navlist.item href="/transactions" icon="list-bullet">Transactions</flux:navlist.item>
    
    <flux:navlist.group heading="Account" expandable>
        <flux:navlist.item href="/profile">Profile</flux:navlist.item>
        <flux:navlist.item href="/settings">Settings</flux:navlist.item>
        <flux:navlist.item href="/billing">Billing</flux:navlist.item>
    </flux:navlist.group>
</flux:navlist>

<!-- Collapsed by default -->
<flux:navlist.group heading="Account" expandable :expanded="false">
    <!-- items -->
</flux:navlist.group>
```

### flux:breadcrumbs
Help users navigate and understand their place within your application.

**Slots:**
- `default`: The breadcrumb items to display

**Example:**
```blade
<flux:breadcrumbs>
    <flux:breadcrumbs.item href="/">Home</flux:breadcrumbs.item>
    <flux:breadcrumbs.item href="/blog">Blog</flux:breadcrumbs.item>
    <flux:breadcrumbs.item>Post</flux:breadcrumbs.item>
</flux:breadcrumbs>
```

### flux:breadcrumbs.item
Individual breadcrumb item.

**Props:**
- `href`: URL the breadcrumb item links to (if omitted, renders as non-clickable text)
- `icon`: Name of the icon to display before the badge text
- `icon:variant`: Icon variant - Options: `outline`, `solid`, `mini`, `micro` (default: `mini`)
- `separator`: Name of the icon to display as the separator (default: `chevron-right`)

**Examples:**
```blade
<!-- With slashes as separators -->
<flux:breadcrumbs>
    <flux:breadcrumbs.item href="/" separator="slash">Home</flux:breadcrumbs.item>
    <flux:breadcrumbs.item href="/blog" separator="slash">Blog</flux:breadcrumbs.item>
    <flux:breadcrumbs.item separator="slash">Post</flux:breadcrumbs.item>
</flux:breadcrumbs>

<!-- With icon -->
<flux:breadcrumbs>
    <flux:breadcrumbs.item href="/" icon="home" />
    <flux:breadcrumbs.item href="/blog">Blog</flux:breadcrumbs.item>
    <flux:breadcrumbs.item>Post</flux:breadcrumbs.item>
</flux:breadcrumbs>

<!-- With ellipsis -->
<flux:breadcrumbs>
    <flux:breadcrumbs.item href="/" icon="home" />
    <flux:breadcrumbs.item icon="ellipsis-horizontal" />
    <flux:breadcrumbs.item>Post</flux:breadcrumbs.item>
</flux:breadcrumbs>

<!-- With ellipsis dropdown -->
<flux:breadcrumbs>
    <flux:breadcrumbs.item href="/" icon="home" />
    <flux:breadcrumbs.item>
        <flux:dropdown>
            <flux:button icon="ellipsis-horizontal" variant="ghost" size="sm" />
            <flux:navmenu>
                <flux:navmenu.item>Client</flux:navmenu.item>
                <flux:navmenu.item icon="arrow-turn-down-right">Team</flux:navmenu.item>
                <flux:navmenu.item icon="arrow-turn-down-right">User</flux:navmenu.item>
            </flux:navmenu>
        </flux:dropdown>
    </flux:breadcrumbs.item>
    <flux:breadcrumbs.item>Post</flux:breadcrumbs.item>
</flux:breadcrumbs>
```

### flux:tabs (Pro Component)
Organize content into separate panels within a single container.

**Container: flux:tab.group**
**Slots:**
- `default`: The tabs and panels components

**Component: flux:tabs**
**Props:**
- `wire:model`: Binds the active tab to a Livewire property
- `variant`: Visual style - Options: `default`, `segmented`, `pills`
- `size`: Size of the tabs - Options: `base` (default), `sm`

**Slots:**
- `default`: The individual tab components

**Attributes:**
- `data-flux-tabs`: Applied to the root element for styling and identification

**Component: flux:tab**
**Props:**
- `name`: Unique identifier for the tab, used to match with its panel
- `icon`: Name of the icon to display at the start of the tab
- `icon:trailing`: Name of the icon to display at the end of the tab
- `icon:variant`: Variant of the icon - Options: `outline`, `solid`, `mini`, `micro`
- `action`: Converts the tab to an action button (used for "Add tab" functionality)
- `accent`: If true, applies accent color styling to the tab
- `size`: Size of the tab (only applies when variant="segmented") - Options: `base` (default), `sm`
- `disabled`: Disables the tab

**Slots:**
- `default`: The tab label content

**Attributes:**
- `data-flux-tab`: Applied to the tab element for styling and identification
- `data-selected`: Applied when the tab is selected/active

**Component: flux:tab.panel**
**Props:**
- `name`: Unique identifier matching the associated tab

**Slots:**
- `default`: The panel content displayed when the associated tab is selected

**Attributes:**
- `data-flux-tab-panel`: Applied to the panel element for styling and identification

**Examples:**
```blade
<!-- Basic tabs -->
<flux:tab.group>
    <flux:tabs wire:model="tab">
        <flux:tab name="profile">Profile</flux:tab>
        <flux:tab name="account">Account</flux:tab>
        <flux:tab name="billing">Billing</flux:tab>
    </flux:tabs>
    
    <flux:tab.panel name="profile">
        <!-- Profile content -->
    </flux:tab.panel>
    <flux:tab.panel name="account">
        <!-- Account content -->
    </flux:tab.panel>
    <flux:tab.panel name="billing">
        <!-- Billing content -->
    </flux:tab.panel>
</flux:tab.group>

<!-- With icons -->
<flux:tabs>
    <flux:tab name="profile" icon="user">Profile</flux:tab>
    <flux:tab name="account" icon="cog-6-tooth">Account</flux:tab>
    <flux:tab name="billing" icon="banknotes">Billing</flux:tab>
</flux:tabs>

<!-- Padded edges -->
<flux:tabs class="px-4">
    <flux:tab name="profile">Profile</flux:tab>
    <flux:tab name="account">Account</flux:tab>
    <flux:tab name="billing">Billing</flux:tab>
</flux:tabs>

<!-- Segmented tabs -->
<flux:tabs variant="segmented">
    <flux:tab>List</flux:tab>
    <flux:tab>Board</flux:tab>
    <flux:tab>Timeline</flux:tab>
</flux:tabs>

<!-- Segmented with icons -->
<flux:tabs variant="segmented">
    <flux:tab icon="list-bullet">List</flux:tab>
    <flux:tab icon="squares-2x2">Board</flux:tab>
    <flux:tab icon="calendar-days">Timeline</flux:tab>
</flux:tabs>

<!-- Small segmented tabs -->
<flux:tabs variant="segmented" size="sm">
    <flux:tab>Demo</flux:tab>
    <flux:tab>Code</flux:tab>
</flux:tabs>

<!-- Pill tabs -->
<flux:tabs variant="pills">
    <flux:tab>List</flux:tab>
    <flux:tab>Board</flux:tab>
    <flux:tab>Timeline</flux:tab>
</flux:tabs>

<!-- Dynamic tabs -->
<flux:tab.group>
    <flux:tabs>
        @foreach ($tabs as $id => $tab)
            <flux:tab :name="$id">{{ $tab }}</flux:tab>
        @endforeach
        
        <flux:tab icon="plus" wire:click="addTab" action>Add tab</flux:tab>
    </flux:tabs>
    
    @foreach ($tabs as $id => $tab)
        <flux:tab.panel :name="$id">
            <!-- Panel content -->
        </flux:tab.panel>
    @endforeach
</flux:tab.group>
```

### flux:pagination (Pro Component)
Display a series of buttons to navigate through a list of items.

**Props:**
- `paginator`: The paginator instance to display (Laravel's paginate() or simplePaginate())

**Examples:**
```blade
<!-- Standard pagination -->
@php
    $orders = Order::paginate()
@endphp
<flux:pagination :paginator="$orders" />

<!-- Simple pagination (Previous/Next only) -->
@php
    $orders = Order::simplePaginate()
@endphp
<flux:pagination :paginator="$orders" />

<!-- With custom per page -->
@php
    $orders = Order::paginate(5)
@endphp
<flux:pagination :paginator="$orders" />
```

### Navigation Patterns

#### Active State Detection
Navigation components automatically detect the current page based on the `href` attribute. You can override this behavior using the `current` prop:

```blade
<!-- Auto-detection -->
<flux:navbar.item href="/dashboard">Dashboard</flux:navbar.item>

<!-- Manual control -->
<flux:navbar.item href="/dashboard" :current="request()->routeIs('dashboard.*')">Dashboard</flux:navbar.item>
```

#### Responsive Navigation
Combine layout components for responsive behavior:

```blade
<!-- Mobile: Collapsible sidebar, Desktop: Fixed sidebar -->
<flux:sidebar stashable class="lg:sticky">
    <flux:sidebar.toggle class="lg:hidden" />
    <!-- navigation -->
</flux:sidebar>

<!-- Mobile: Hamburger menu, Desktop: Full navbar -->
<flux:header>
    <flux:sidebar.toggle class="lg:hidden" />
    <flux:navbar class="hidden lg:flex">
        <!-- navigation items -->
    </flux:navbar>
</flux:header>
```

#### Nested Navigation
Use groups and dropdowns for hierarchical navigation:

```blade
<!-- Sidebar with groups -->
<flux:navlist>
    <flux:navlist.item href="/dashboard" icon="home">Dashboard</flux:navlist.item>
    
    <flux:navlist.group heading="Content" expandable>
        <flux:navlist.item href="/posts">Posts</flux:navlist.item>
        <flux:navlist.item href="/pages">Pages</flux:navlist.item>
        <flux:navlist.item href="/media">Media</flux:navlist.item>
    </flux:navlist.group>
    
    <flux:navlist.group heading="Settings" expandable :expanded="false">
        <flux:navlist.item href="/settings/general">General</flux:navlist.item>
        <flux:navlist.item href="/settings/users">Users</flux:navlist.item>
    </flux:navlist.group>
</flux:navlist>

<!-- Navbar with dropdowns -->
<flux:navbar>
    <flux:navbar.item href="/dashboard">Dashboard</flux:navbar.item>
    
    <flux:dropdown>
        <flux:navbar.item icon:trailing="chevron-down">Content</flux:navbar.item>
        <flux:navmenu>
            <flux:navmenu.item href="/posts">Posts</flux:navmenu.item>
            <flux:navmenu.item href="/pages">Pages</flux:navmenu.item>
            <flux:navmenu.item href="/media">Media</flux:navmenu.item>
        </flux:navmenu>
    </flux:dropdown>
</flux:navbar>
```

#### Integration with Laravel Routes
Use Laravel's route helpers for dynamic URLs and active states:

```blade
<!-- Named routes -->
<flux:navbar.item href="{{ route('dashboard') }}">Dashboard</flux:navbar.item>
<flux:navbar.item href="{{ route('users.index') }}">Users</flux:navbar.item>

<!-- Route model binding -->
<flux:navbar.item href="{{ route('projects.show', $project) }}">
    {{ $project->name }}
</flux:navbar.item>

<!-- Active state with route patterns -->
<flux:navbar.item 
    href="{{ route('settings.general') }}"
    :current="request()->routeIs('settings.*')"
>
    Settings
</flux:navbar.item>

<!-- Dynamic badges -->
<flux:navbar.item 
    href="{{ route('notifications.index') }}" 
    :badge="auth()->user()->unreadNotifications()->count()"
>
    Notifications
</flux:navbar.item>
```

## Form Components

### flux:input
A versatile input component supporting various types, sizes, and features like icons, keyboard shortcuts, and actions.

#### Props
- **wire:model** - Binds to Livewire property
- **type** - HTML input type (text, email, password, file, date). Default: `text`
- **label** - Label text displayed above the input
- **description** - Descriptive text displayed below the label
- **placeholder** - Placeholder text when empty
- **size** - Size options: `sm`, `xs`
- **variant** - Visual style: `filled` (default: `outline`)
- **disabled** - Prevents user interaction
- **readonly** - Makes input read-only
- **invalid** - Applies error styling
- **multiple** - For file inputs, allows multiple selection
- **mask** - Input mask pattern (e.g., `99/99/9999`)
- **icon** - Icon name for start of input
- **icon:trailing** - Icon name for end of input
- **kbd** - Keyboard shortcut hint
- **clearable** - Shows clear button when has content
- **copyable** - Shows copy button
- **viewable** - For passwords, shows visibility toggle
- **as** - Render as different element: `button` (default: `input`)
- **class:input** - CSS classes for input element

#### Slots
- **icon** / **icon:leading** - Custom content at start
- **icon:trailing** - Custom content at end

#### Examples
```blade
<!-- Basic input -->
<flux:input wire:model="email" type="email" placeholder="Enter email" />

<!-- With label and description -->
<flux:input 
    wire:model="username" 
    label="Username" 
    description="Choose a unique username"
/>

<!-- With icons -->
<flux:input wire:model="search" placeholder="Search..." icon="magnifying-glass" />
<flux:input wire:model="email" type="email" icon="envelope" />

<!-- With keyboard shortcut -->
<flux:input wire:model="search" placeholder="Quick search" kbd="⌘K" />

<!-- Password with toggle -->
<flux:input wire:model="password" type="password" viewable />

<!-- With clear button -->
<flux:input wire:model="search" clearable />

<!-- Copyable input -->
<flux:input value="API_KEY_123456" readonly copyable />

<!-- File input -->
<flux:input type="file" wire:model="avatar" label="Profile Picture" />

<!-- With mask -->
<flux:input wire:model="phone" mask="(999) 999-9999" placeholder="(555) 123-4567" />

<!-- As button (for search triggers) -->
<flux:input as="button" variant="filled" placeholder="Search..." icon="magnifying-glass" />

<!-- Small size -->
<flux:input wire:model="name" size="sm" />

<!-- Filled variant -->
<flux:input wire:model="email" variant="filled" />

<!-- With trailing icon -->
<flux:input wire:model="username" icon:trailing="check-circle" />

<!-- Custom icon slot -->
<flux:input wire:model="amount">
    <x-slot name="icon">
        <flux:icon.currency-dollar class="text-gray-400" />
    </x-slot>
</flux:input>
```

### flux:textarea
Multi-line text input with auto-resize capabilities.

#### Props
- **wire:model** - Binds to Livewire property
- **label** - Label text
- **description** - Help text
- **placeholder** - Placeholder text
- **rows** - Initial number of visible rows
- **resize** - Control resize behavior: `none`, `vertical`, `horizontal`, `both`
- **disabled** - Prevents interaction
- **readonly** - Makes read-only
- **invalid** - Applies error styling
- **monospace** - Uses monospace font

#### Examples
```blade
<!-- Basic textarea -->
<flux:textarea wire:model="message" placeholder="Enter your message..." />

<!-- With rows -->
<flux:textarea wire:model="description" rows="5" />

<!-- Non-resizable -->
<flux:textarea wire:model="bio" resize="none" />

<!-- Monospace for code -->
<flux:textarea wire:model="code" monospace rows="10" />

<!-- With label -->
<flux:textarea 
    wire:model="notes" 
    label="Additional Notes"
    description="Any special requirements"
/>
```

### flux:checkbox
Checkbox input for boolean values with support for custom styling and grouping.

#### Props
- **wire:model** - Binds checkbox state
- **label** - Label text
- **description** - Help text  
- **value** - Value when checked (for groups)
- **checked** - Default checked state
- **indeterminate** - Shows indeterminate state
- **disabled** - Prevents interaction
- **invalid** - Applies error styling

#### Examples
```blade
<!-- Single checkbox -->
<flux:checkbox wire:model="agree" label="I agree to the terms" />

<!-- With description -->
<flux:checkbox 
    wire:model="newsletter"
    label="Subscribe to newsletter"
    description="Get weekly updates"
/>

<!-- In a group -->
<flux:checkbox wire:model="permissions" value="read" label="Read" />
<flux:checkbox wire:model="permissions" value="write" label="Write" />
<flux:checkbox wire:model="permissions" value="delete" label="Delete" />

<!-- Indeterminate state -->
<flux:checkbox indeterminate label="Select all" />
```

### flux:checkbox.group
Groups multiple checkboxes with optional select-all functionality.

#### Props
- **wire:model** - Binds selected values array
- **label** - Group label
- **description** - Group description
- **variant** - Visual style: `default`, `cards` (Pro)
- **disabled** - Disables all checkboxes
- **invalid** - Applies error styling to all

#### Examples
```blade
<!-- Basic checkbox group -->
<flux:checkbox.group wire:model="notifications" label="Notifications">
    <flux:checkbox value="email" label="Email" checked />
    <flux:checkbox value="sms" label="SMS" />
    <flux:checkbox value="push" label="Push notifications" />
</flux:checkbox.group>

<!-- With descriptions -->
<flux:checkbox.group wire:model="features">
    <flux:checkbox 
        value="analytics" 
        label="Analytics"
        description="Track user behavior and conversions"
    />
    <flux:checkbox 
        value="reports" 
        label="Reports"
        description="Generate detailed reports"
    />
</flux:checkbox.group>

<!-- Card variant (Pro) -->
<flux:checkbox.group variant="cards" class="max-sm:flex-col">
    <flux:checkbox value="1" label="Option 1" icon="chart-bar" />
    <flux:checkbox value="2" label="Option 2" icon="users" />
</flux:checkbox.group>
```

### flux:checkbox.all
Special checkbox that controls all checkboxes in its group.

#### Props
- **label** - Text label
- **description** - Help text
- **disabled** - Prevents interaction

#### Example
```blade
<flux:checkbox.group>
    <flux:checkbox.all label="Select all" />
    <flux:checkbox value="1" label="Item 1" />
    <flux:checkbox value="2" label="Item 2" />
    <flux:checkbox value="3" label="Item 3" />
</flux:checkbox.group>
```

### flux:radio.group
Groups radio buttons for single-choice selection.

#### Props
- **wire:model** - Binds selected value
- **label** - Group label
- **description** - Group description  
- **variant** - Visual style: `default`, `segmented`, `cards`
- **invalid** - Applies error styling

#### Examples
```blade
<!-- Basic radio group -->
<flux:radio.group wire:model="plan" label="Select plan">
    <flux:radio value="basic" label="Basic" />
    <flux:radio value="pro" label="Pro" checked />
    <flux:radio value="enterprise" label="Enterprise" />
</flux:radio.group>

<!-- Segmented variant -->
<flux:radio.group wire:model="size" variant="segmented">
    <flux:radio label="S" value="small" />
    <flux:radio label="M" value="medium" />
    <flux:radio label="L" value="large" />
</flux:radio.group>

<!-- Cards variant with icons -->
<flux:radio.group variant="cards" class="flex-col">
    <flux:radio 
        value="standard" 
        icon="truck"
        label="Standard Shipping"
        description="5-7 business days"
    />
    <flux:radio 
        value="express" 
        icon="rocket"
        label="Express Shipping"
        description="2-3 business days"
    />
</flux:radio.group>
```

### flux:radio
Individual radio button within a group.

#### Props
- **label** - Label text
- **description** - Help text
- **value** - Value when selected
- **checked** - Default selected state
- **disabled** - Prevents interaction
- **icon** - Icon name (for segmented variant)

### flux:select
Dropdown selection component with native and custom variants.

#### Props
- **wire:model** - Binds selected value(s)
- **placeholder** - Text when nothing selected
- **label** - Label text (creates field wrapper)
- **description** - Help text
- **description:trailing** - Help text below select
- **badge** - Badge for label
- **size** - Size options: `sm`, `xs`
- **variant** - Style: `default` (native), `listbox`, `combobox`
- **multiple** - Allows multiple selection (listbox/combobox only)
- **filter** - If `false`, disables client-side filtering
- **searchable** - Adds search input (listbox/combobox only)
- **clearable** - Shows clear button (listbox/combobox only)
- **selected-suffix** - Text after count in multiple mode
- **clear** - When to clear search: `select` (default), `close`
- **disabled** - Prevents interaction
- **invalid** - Applies error styling

#### Examples
```blade
<!-- Native select -->
<flux:select wire:model="country" placeholder="Choose country...">
    <flux:select.option>United States</flux:select.option>
    <flux:select.option>Canada</flux:select.option>
    <flux:select.option>Mexico</flux:select.option>
</flux:select>

<!-- Custom listbox with search -->
<flux:select variant="listbox" searchable placeholder="Select users...">
    <flux:select.option value="1">John Doe</flux:select.option>
    <flux:select.option value="2">Jane Smith</flux:select.option>
</flux:select>

<!-- Multiple select with custom suffix -->
<flux:select 
    variant="listbox" 
    multiple 
    selected-suffix="items selected"
    wire:model="selectedItems"
>
    <!-- options -->
</flux:select>

<!-- Combobox with dynamic options -->
<flux:select variant="combobox" :filter="false">
    <x-slot name="input">
        <flux:select.input wire:model.live="search" />
    </x-slot>
    @foreach($this->filteredUsers as $user)
        <flux:select.option :value="$user->id">
            {{ $user->name }}
        </flux:select.option>
    @endforeach
</flux:select>

<!-- Options with icons -->
<flux:select variant="listbox">
    <flux:select.option>
        <div class="flex items-center gap-2">
            <flux:icon.user variant="mini" />
            Admin
        </div>
    </flux:select.option>
</flux:select>
```

### flux:select.option
Individual option within a select.

#### Props
- **value** - Option value
- **disabled** - Prevents selection

### flux:switch
Toggle switch for binary on/off settings.

#### Props
- **wire:model** - Binds toggle state
- **label** - Label text
- **description** - Help text
- **align** - Alignment: `right|start` (default), `left|end`
- **disabled** - Prevents interaction

#### Examples
```blade
<!-- Basic switch -->
<flux:field variant="inline">
    <flux:label>Enable notifications</flux:label>
    <flux:switch wire:model.live="notifications" />
</flux:field>

<!-- With shorthand -->
<flux:switch 
    wire:model="darkMode" 
    label="Dark mode"
    description="Use dark theme"
/>

<!-- Left-aligned switches -->
<flux:switch 
    label="Email alerts" 
    align="left" 
    wire:model="emailAlerts"
/>
```

### flux:field
Container component providing structure for form inputs with labels, descriptions, and errors.

#### Props
- **variant** - Layout style: `block` (default), `inline`

#### Slots
- **default** - Form control elements and associated components

#### Examples
```blade
<!-- Full field structure -->
<flux:field>
    <flux:label>Username</flux:label>
    <flux:description>Choose a unique username</flux:description>
    <flux:input wire:model="username" />
    <flux:error name="username" />
</flux:field>

<!-- Inline variant for checkboxes/switches -->
<flux:field variant="inline">
    <flux:checkbox wire:model="remember" />
    <flux:label>Remember me</flux:label>
</flux:field>
```

### flux:autocomplete (Pro)
Enhance input fields with autocomplete suggestions for better user experience and data entry.

#### Props
- **wire:model** - Binds to Livewire property
- **type** - HTML input type (text, email, password, file, date). Default: `text`
- **label** - Label text displayed above the input
- **description** - Descriptive text displayed below the label
- **placeholder** - Placeholder text when empty
- **size** - Size options: `sm`, `xs`
- **variant** - Visual style: `filled` (default: `outline`)
- **disabled** - Prevents user interaction
- **readonly** - Makes input read-only
- **invalid** - Applies error styling
- **multiple** - For file inputs, allows multiple selection
- **mask** - Input mask pattern (e.g., `99/99/9999`)
- **icon** - Icon name for start of input
- **icon:trailing** - Icon name for end of input
- **kbd** - Keyboard shortcut hint
- **clearable** - Shows clear button when has content
- **copyable** - Shows copy button
- **viewable** - For passwords, shows visibility toggle
- **as** - Render as different element: `button` (default: `input`)
- **class:input** - CSS classes for input element

#### Slots
- **icon** / **icon:leading** - Custom content at start
- **icon:trailing** - Custom content at end

#### Examples
```blade
<!-- Basic autocomplete -->
<flux:autocomplete wire:model="state" label="State of residence">
    <flux:autocomplete.item>Alabama</flux:autocomplete.item>
    <flux:autocomplete.item>Arkansas</flux:autocomplete.item>
    <flux:autocomplete.item>California</flux:autocomplete.item>
    <!-- ... more states -->
</flux:autocomplete>

<!-- With custom values -->
<flux:autocomplete wire:model="userId" label="Select user">
    <flux:autocomplete.item value="1">John Doe</flux:autocomplete.item>
    <flux:autocomplete.item value="2">Jane Smith</flux:autocomplete.item>
    <flux:autocomplete.item value="3" disabled>Mike Johnson (Inactive)</flux:autocomplete.item>
</flux:autocomplete>

<!-- Dynamic autocomplete with Livewire -->
<flux:autocomplete 
    wire:model="selectedCity"
    wire:keyup="searchCities"
    label="City"
    placeholder="Type to search..."
>
    @foreach($cities as $city)
        <flux:autocomplete.item value="{{ $city->id }}">
            {{ $city->name }}, {{ $city->state }}
        </flux:autocomplete.item>
    @endforeach
</flux:autocomplete>
```

### flux:autocomplete.item
Individual item within an autocomplete list.

#### Props
- **value** - Value to set when selected (defaults to text content)
- **disabled** - Prevents selection

### flux:date-picker (Pro)
A comprehensive date selection component with calendar interface.

#### Props
- **wire:model** - Binds selected date(s)
- **label** - Label text
- **description** - Help text
- **placeholder** - Placeholder text
- **mode** - Selection mode: `single`, `multiple`, `range`
- **format** - Date format string (e.g., `Y-m-d`)
- **min** - Minimum selectable date
- **max** - Maximum selectable date
- **disabled-dates** - Array of dates to disable
- **clearable** - Shows clear button
- **invalid** - Applies error styling
- **disabled** - Prevents interaction

#### Examples
```blade
<!-- Single date picker -->
<flux:date-picker 
    wire:model="birthday" 
    label="Date of Birth"
    placeholder="Select date"
    max="{{ now()->format('Y-m-d') }}"
/>

<!-- Date range picker -->
<flux:date-picker 
    wire:model="dateRange"
    mode="range"
    label="Select date range"
    placeholder="From - To"
/>

<!-- Multiple dates -->
<flux:date-picker 
    wire:model="holidays"
    mode="multiple"
    label="Select holidays"
/>

<!-- With disabled dates -->
<flux:date-picker 
    wire:model="appointment"
    label="Book appointment"
    :disabled-dates="$bookedDates"
    :min="now()->format('Y-m-d')"
/>
```

### flux:editor (Pro)
Rich text editor component for formatted content creation.

#### Props
- **wire:model** - Binds editor content
- **label** - Label text
- **description** - Help text
- **placeholder** - Placeholder text
- **toolbar** - Toolbar configuration array
- **height** - Editor height (e.g., `300px`, `auto`)
- **max-height** - Maximum height for auto-sizing
- **disabled** - Prevents editing
- **readonly** - Makes editor read-only
- **invalid** - Applies error styling
- **autofocus** - Focus on mount

#### Toolbar Options
- `bold`, `italic`, `underline`, `strike`
- `heading1`, `heading2`, `heading3`
- `bulletList`, `orderedList`
- `link`, `image`, `video`
- `code`, `codeBlock`, `blockquote`
- `align`, `color`, `highlight`
- `table`, `horizontalRule`
- `undo`, `redo`

#### Examples
```blade
<!-- Basic editor -->
<flux:editor 
    wire:model="content"
    label="Article content"
    placeholder="Start writing..."
/>

<!-- Custom toolbar -->
<flux:editor 
    wire:model="comment"
    label="Add comment"
    :toolbar="['bold', 'italic', 'link', 'bulletList', 'orderedList']"
    height="200px"
/>

<!-- Full-featured editor -->
<flux:editor 
    wire:model="post.body"
    label="Post content"
    description="You can use rich formatting"
    :toolbar="[
        'heading1', 'heading2', 'heading3', '|',
        'bold', 'italic', 'underline', 'strike', '|',
        'bulletList', 'orderedList', '|',
        'link', 'image', 'video', '|',
        'code', 'codeBlock', 'blockquote', '|',
        'table', 'horizontalRule', '|',
        'undo', 'redo'
    ]"
    height="auto"
    max-height="600px"
/>

<!-- Read-only preview -->
<flux:editor 
    wire:model="article.content"
    readonly
    :toolbar="false"
/>
```

## Form Validation Patterns

### Basic Validation
```blade
<!-- Component -->
<flux:input 
    wire:model="email" 
    label="Email"
    type="email"
    :invalid="$errors->has('email')"
/>

<!-- Livewire Component -->
public function rules()
{
    return [
        'email' => 'required|email',
    ];
}
```

### Real-time Validation
```blade
<flux:input 
    wire:model.live.debounce.500ms="username"
    label="Username"
    description="Must be unique"
/>

<!-- In Livewire component -->
public function updatedUsername($value)
{
    $this->validateOnly('username');
}
```

### Custom Validation Messages
```blade
<flux:field>
    <flux:label>Password</flux:label>
    <flux:input type="password" wire:model="password" />
    @error('password')
        <flux:error name="password">{{ $message }}</flux:error>
    @enderror
</flux:field>
```

### Form Submission Pattern
```blade
<form wire:submit="save">
    <div class="space-y-4">
        <flux:input 
            wire:model="name" 
            label="Name" 
            required
        />
        
        <flux:textarea 
            wire:model="message" 
            label="Message"
            rows="4"
        />
        
        <flux:checkbox 
            wire:model="agree"
            label="I agree to the terms"
        />
        
        <flux:button type="submit" variant="primary">
            Submit
        </flux:button>
    </div>
</form>
```

### Complex Form Layout
```blade
<div class="space-y-6">
    <!-- Personal Information -->
    <flux:fieldset>
        <flux:legend>Personal Information</flux:legend>
        
        <div class="grid grid-cols-2 gap-4">
            <flux:input label="First name" wire:model="firstName" />
            <flux:input label="Last name" wire:model="lastName" />
        </div>
        
        <flux:input 
            type="email" 
            label="Email" 
            wire:model="email"
            class="mt-4"
        />
    </flux:fieldset>
    
    <!-- Preferences -->
    <flux:fieldset>
        <flux:legend>Preferences</flux:legend>
        
        <flux:checkbox.group wire:model="notifications">
            <flux:checkbox value="email" label="Email notifications" />
            <flux:checkbox value="sms" label="SMS alerts" />
            <flux:checkbox value="push" label="Push notifications" />
        </flux:checkbox.group>
    </flux:fieldset>
    
    <!-- Submit -->
    <div class="flex gap-4">
        <flux:button type="submit" variant="primary">Save</flux:button>
        <flux:button type="button" variant="ghost">Cancel</flux:button>
    </div>
</div>
```

### Form Wizard with Steps

Implement multi-step forms:

```blade
<div x-data="{ step: 1 }">
    <!-- Progress indicator -->
    <flux:breadcrumbs>
        <flux:breadcrumbs.item :active="step >= 1">
            Personal Info
        </flux:breadcrumbs.item>
        <flux:breadcrumbs.item :active="step >= 2">
            Contact Details
        </flux:breadcrumbs.item>
        <flux:breadcrumbs.item :active="step >= 3">
            Review
        </flux:breadcrumbs.item>
    </flux:breadcrumbs>

    <!-- Step content -->
    <div x-show="step === 1">
        <!-- Personal info fields -->
    </div>
    
    <!-- Navigation -->
    <flux:button 
        @click="step++"
        :disabled="!$wire.canProceed"
    >
        Next
    </flux:button>
</div>
```# Flux UI Documentation - Part 4: Display & Feedback Components

## Data Display Components

### Table Component

The `<flux:table>` component displays structured data in a condensed, searchable format with support for pagination, sorting, and responsive design.

#### Basic Structure

```blade
<flux:table>
    <flux:table.columns>
        <flux:table.column>Name</flux:table.column>
        <flux:table.column>Email</flux:table.column>
        <flux:table.column>Status</flux:table.column>
    </flux:table.columns>
    <flux:table.rows>
        <flux:table.row>
            <flux:table.cell>John Doe</flux:table.cell>
            <flux:table.cell>john@example.com</flux:table.cell>
            <flux:table.cell>Active</flux:table.cell>
        </flux:table.row>
    </flux:table.rows>
</flux:table>
```

#### Table Props

| Prop | Type | Description |
|------|------|-------------|
| `paginate` | Laravel Paginator | Pagination instance for data |
| `class` | String | Additional CSS classes |
| `data-flux-table` | String | Styling/identification attribute |

#### Column Props

| Prop | Type | Values | Description |
|------|------|--------|-------------|
| `align` | String | `start`, `center`, `end` | Column alignment |
| `sortable` | Boolean | - | Enable column sorting |
| `sorted` | Boolean | - | Current sort state |
| `direction` | String | `asc`, `desc` | Sort direction |

#### Cell Props

| Prop | Type | Values | Description |
|------|------|--------|-------------|
| `align` | String | `start`, `center`, `end` | Cell alignment |
| `variant` | String | `default`, `strong` | Cell styling variant |

#### Livewire Integration Example

```php
use Livewire\WithPagination;
use Livewire\Component;

class OrdersTable extends Component
{
    use WithPagination;
    
    public $sortBy = 'created_at';
    public $sortDirection = 'desc';
    
    public function sort($column)
    {
        if ($this->sortBy === $column) {
            $this->sortDirection = $this->sortDirection === 'asc' ? 'desc' : 'asc';
        } else {
            $this->sortBy = $column;
            $this->sortDirection = 'asc';
        }
    }
    
    public function orders()
    {
        return Order::query()
            ->with(['customer', 'products'])
            ->orderBy($this->sortBy, $this->sortDirection)
            ->paginate(10);
    }
    
    public function render()
    {
        return view('livewire.orders-table', [
            'orders' => $this->orders()
        ]);
    }
}
```

```blade
{{-- livewire/orders-table.blade.php --}}
<flux:table :paginate="$orders">
    <flux:table.columns>
        <flux:table.column 
            sortable 
            :sorted="$sortBy === 'order_number'"
            :direction="$sortDirection"
            wire:click="sort('order_number')"
        >
            Order #
        </flux:table.column>
        <flux:table.column 
            sortable 
            :sorted="$sortBy === 'customer_name'"
            :direction="$sortDirection"
            wire:click="sort('customer_name')"
        >
            Customer
        </flux:table.column>
        <flux:table.column align="center">Status</flux:table.column>
        <flux:table.column align="end">Total</flux:table.column>
    </flux:table.columns>
    
    <flux:table.rows>
        @foreach ($orders as $order)
            <flux:table.row wire:key="order-{{ $order->id }}">
                <flux:table.cell variant="strong">
                    {{ $order->order_number }}
                </flux:table.cell>
                <flux:table.cell>
                    <div class="flex items-center gap-2">
                        <flux:avatar 
                            size="sm" 
                            :src="$order->customer->avatar_url" 
                            :name="$order->customer->name"
                        />
                        {{ $order->customer->name }}
                    </div>
                </flux:table.cell>
                <flux:table.cell align="center">
                    <flux:badge :color="$order->status_color">
                        {{ $order->status_label }}
                    </flux:badge>
                </flux:table.cell>
                <flux:table.cell align="end" variant="strong">
                    ${{ number_format($order->total, 2) }}
                </flux:table.cell>
            </flux:table.row>
        @endforeach
    </flux:table.rows>
</flux:table>
```

#### Responsive Behavior

Tables automatically adapt to smaller screens by:
- Horizontal scrolling on mobile devices
- Maintaining column widths for readability
- Touch-friendly interaction areas

### Card Component

The `<flux:card>` component serves as a container for related content such as forms, alerts, or data lists.

#### Basic Usage

```blade
<flux:card>
    <flux:heading>Card Title</flux:heading>
    <flux:text>Card content goes here.</flux:text>
</flux:card>
```

#### Card Props

| Prop | Type | Values | Description |
|------|------|--------|-------------|
| `size` | String | `sm`, default | Card size variant |
| `class` | String | - | Additional CSS classes |
| `data-flux-card` | String | - | Root element styling |

#### Card Variants

##### Small Card
```blade
<flux:card size="sm" class="space-y-4">
    <flux:heading size="lg">Compact Content</flux:heading>
    <flux:text>Ideal for notifications or quick info.</flux:text>
</flux:card>
```

##### Data List Card
```blade
<flux:card class="space-y-6">
    <flux:heading>User Statistics</flux:heading>
    
    <div class="grid grid-cols-2 gap-4">
        <div>
            <flux:text variant="dim">Total Users</flux:text>
            <flux:heading size="xl">1,234</flux:heading>
        </div>
        <div>
            <flux:text variant="dim">Active Today</flux:text>
            <flux:heading size="xl">456</flux:heading>
        </div>
    </div>
</flux:card>
```

#### Livewire Integration

```php
class UserStatsCard extends Component
{
    public $stats;
    
    public function mount()
    {
        $this->stats = [
            'total_users' => User::count(),
            'active_today' => User::whereDate('last_active', today())->count(),
            'new_this_week' => User::whereDate('created_at', '>=', now()->startOfWeek())->count(),
        ];
    }
    
    public function render()
    {
        return view('livewire.user-stats-card');
    }
}
```

### Badge Component

The `<flux:badge>` component highlights information like status, category, or count.

#### Basic Usage

```blade
<flux:badge>Default</flux:badge>
<flux:badge color="green">Active</flux:badge>
<flux:badge color="red" size="sm">Error</flux:badge>
```

#### Badge Props

| Prop | Type | Values | Description |
|------|------|--------|-------------|
| `color` | String | `zinc`, `red`, `orange`, `amber`, `yellow`, `lime`, `green`, `emerald`, `teal`, `cyan`, `sky`, `blue`, `indigo`, `violet`, `purple`, `fuchsia`, `pink`, `rose` | Badge color |
| `size` | String | `sm`, default, `lg` | Badge size |
| `variant` | String | `pill` | Pill-shaped badge |
| `icon` | String | Icon name | Icon before text |
| `icon:trailing` | String | Icon name | Icon after text |
| `icon:variant` | String | `outline`, `solid`, `mini`, `micro` | Icon style |
| `as` | String | Element tag | Render as different element |
| `inset` | String | `top`, `bottom`, `left`, `right` | Negative margins |

#### Advanced Examples

##### Status Badges with Icons
```blade
<flux:badge color="green" icon="check-circle">
    Completed
</flux:badge>

<flux:badge color="yellow" icon="clock" variant="pill">
    In Progress
</flux:badge>

<flux:badge color="red" icon:trailing="x-mark" as="button" wire:click="remove">
    Error
</flux:badge>
```

##### Dynamic Badges in Tables
```blade
@foreach ($users as $user)
    <flux:table.cell>
        <flux:badge 
            :color="$user->isActive() ? 'green' : 'zinc'"
            :icon="$user->isActive() ? 'check' : 'x-mark'"
        >
            {{ $user->status }}
        </flux:badge>
    </flux:table.cell>
@endforeach
```

### Avatar Component

The `<flux:avatar>` component displays user images or initials with support for badges, tooltips, and stacking.

#### Basic Usage

```blade
{{-- Image avatar --}}
<flux:avatar src="/path/to/image.jpg" />

{{-- Initials avatar --}}
<flux:avatar name="John Doe" />

{{-- Icon avatar --}}
<flux:avatar icon="user" />
```

#### Avatar Props

| Prop | Type | Values | Description |
|------|------|--------|-------------|
| `src` | String | URL | Image source |
| `name` | String | - | Generate initials from name |
| `icon` | String | Icon name | Display icon |
| `size` | String | `xs`, `sm`, default, `lg`, `xl` | Avatar size |
| `circle` | Boolean | - | Make fully circular |
| `color` | String | Color name or `auto` | Background color |
| `color:seed` | String | - | Seed for consistent colors |
| `badge` | String/Number | - | Badge content |
| `tooltip` | String | - | Hover tooltip |
| `href` | String | URL | Make clickable link |
| `as` | String | Element tag | Render as different element |

#### Sizes
- `xs`: 24px
- `sm`: 32px
- default: 40px
- `lg`: 48px
- `xl`: 64px

#### Advanced Examples

##### Avatar with Badge
```blade
<flux:avatar 
    src="/users/jane.jpg" 
    name="Jane Smith"
    badge="5"
    tooltip="5 new messages"
/>

{{-- Custom badge content --}}
<flux:avatar name="John Doe">
    <flux:badge slot="badge" color="green" size="sm">
        <flux:icon.check class="size-2" />
    </flux:badge>
</flux:avatar>
```

##### Stacked Avatars
```blade
<div class="flex -space-x-2">
    @foreach ($team->members->take(5) as $member)
        <flux:avatar 
            :src="$member->avatar_url" 
            :name="$member->name"
            :tooltip="$member->name"
            class="ring-2 ring-white dark:ring-zinc-900"
        />
    @endforeach
    
    @if ($team->members->count() > 5)
        <flux:avatar 
            color="zinc"
            class="ring-2 ring-white dark:ring-zinc-900"
        >
            +{{ $team->members->count() - 5 }}
        </flux:avatar>
    @endif
</div>
```

##### Auto-Generated Colors
```blade
{{-- Consistent colors based on user data --}}
@foreach ($users as $user)
    <flux:avatar 
        :name="$user->name"
        color="auto"
        :color:seed="$user->email"
    />
@endforeach
```

### Data Integration Patterns

#### Laravel Collections

Flux components work seamlessly with Laravel collections:

```php
// Controller or Livewire component
$users = User::with(['roles', 'lastActivity'])
    ->orderBy('created_at', 'desc')
    ->get()
    ->map(function ($user) {
        return [
            'id' => $user->id,
            'name' => $user->name,
            'email' => $user->email,
            'role' => $user->roles->first()?->name ?? 'User',
            'status' => $user->isOnline() ? 'online' : 'offline',
            'status_color' => $user->isOnline() ? 'green' : 'zinc',
            'last_seen' => $user->lastActivity?->diffForHumans() ?? 'Never',
        ];
    });
```

```blade
{{-- Blade template --}}
@foreach ($users as $user)
    <flux:card class="p-4">
        <div class="flex items-center justify-between">
            <div class="flex items-center gap-3">
                <flux:avatar 
                    :name="$user['name']" 
                    color="auto"
                    :badge="$user['status'] === 'online' ? '●' : null"
                />
                <div>
                    <flux:heading size="sm">{{ $user['name'] }}</flux:heading>
                    <flux:text variant="dim">{{ $user['email'] }}</flux:text>
                </div>
            </div>
            <div class="text-right">
                <flux:badge :color="$user['status_color']" size="sm">
                    {{ ucfirst($user['status']) }}
                </flux:badge>
                <flux:text variant="dim" size="sm">
                    {{ $user['last_seen'] }}
                </flux:text>
            </div>
        </div>
    </flux:card>
@endforeach
```

#### Real-time Updates with Livewire

```php
class UserDashboard extends Component
{
    public $users;
    public $filter = 'all';
    
    protected $listeners = ['userUpdated' => 'refreshUsers'];
    
    public function mount()
    {
        $this->refreshUsers();
    }
    
    public function refreshUsers()
    {
        $query = User::query();
        
        if ($this->filter === 'active') {
            $query->where('last_active', '>=', now()->subMinutes(5));
        } elseif ($this->filter === 'inactive') {
            $query->where('last_active', '<', now()->subMinutes(5));
        }
        
        $this->users = $query->get();
    }
    
    public function setFilter($filter)
    {
        $this->filter = $filter;
        $this->refreshUsers();
    }
    
    public function render()
    {
        return view('livewire.user-dashboard');
    }
}
```

#### Filtering and Searching

```blade
<div class="space-y-4">
    {{-- Filter badges --}}
    <div class="flex gap-2">
        <flux:badge 
            :color="$filter === 'all' ? 'blue' : 'zinc'"
            as="button"
            wire:click="setFilter('all')"
        >
            All Users ({{ $users->count() }})
        </flux:badge>
        <flux:badge 
            :color="$filter === 'active' ? 'blue' : 'zinc'"
            as="button"
            wire:click="setFilter('active')"
        >
            Active ({{ $users->where('status', 'online')->count() }})
        </flux:badge>
        <flux:badge 
            :color="$filter === 'inactive' ? 'blue' : 'zinc'"
            as="button"
            wire:click="setFilter('inactive')"
        >
            Inactive ({{ $users->where('status', 'offline')->count() }})
        </flux:badge>
    </div>
    
    {{-- Data display --}}
    <flux:table>
        <!-- Table content -->
    </flux:table>
</div>
```

### Best Practices

1. **Performance**: Use `wire:key` for dynamic lists to help Livewire track DOM elements
2. **Accessibility**: Always provide meaningful text alternatives for avatars and badges
3. **Responsive Design**: Test table layouts on mobile devices and consider card-based layouts for complex data on small screens
4. **Loading States**: Implement skeleton loaders or loading indicators for data-heavy components
5. **Empty States**: Always handle empty data sets with meaningful messages

### Component Composition

Flux components are designed to work together. Common patterns include:

```blade
{{-- User list with avatars and badges --}}
<flux:card>
    <flux:table>
        <flux:table.rows>
            @foreach ($users as $user)
                <flux:table.row>
                    <flux:table.cell>
                        <div class="flex items-center gap-3">
                            <flux:avatar 
                                :src="$user->avatar" 
                                :name="$user->name"
                                size="sm"
                            />
                            <div>
                                <div class="font-medium">{{ $user->name }}</div>
                                <flux:badge 
                                    :color="$user->role_color" 
                                    size="sm"
                                >
                                    {{ $user->role }}
                                </flux:badge>
                            </div>
                        </div>
                    </flux:table.cell>
                </flux:table.row>
            @endforeach
        </flux:table.rows>
    </flux:table>
</flux:card>
```

## Feedback Components

### Toast
The Toast component provides user feedback through temporary notification messages.

**Basic Usage:**
```blade
{{-- Include in layout file --}}
<flux:toast />

{{-- Trigger from Livewire component --}}
Flux::toast('Success! Your changes have been saved.');
```

**Props:**
- `position`: Sets toast position on screen
  - Values: `"top left"`, `"top center"`, `"top right"`, `"bottom left"`, `"bottom center"`, `"bottom right"`
  - Default: `"bottom right"`
- `duration`: Display duration in milliseconds
  - Default: 5000ms

**Variants:**
```php
// Success variant
Flux::toast(variant: 'success', 'Operation completed successfully!');

// Warning variant
Flux::toast(variant: 'warning', 'Please review your input.');

// Danger variant
Flux::toast(variant: 'danger', 'An error occurred.');
```

**Livewire Integration:**
```php
public function save()
{
    // Save logic...
    Flux::toast('Profile updated successfully!');
}
```

### Modal
Modal dialogs for focused user interactions and confirmations.

**Basic Usage:**
```blade
<flux:modal name="edit-profile">
    <flux:modal.header>
        <flux:modal.heading>Edit Profile</flux:modal.heading>
        <flux:modal.close />
    </flux:modal.header>
    
    <flux:modal.body>
        {{-- Modal content --}}
    </flux:modal.body>
    
    <flux:modal.footer>
        <flux:button variant="ghost" @click="$modal.close()">Cancel</flux:button>
        <flux:button type="submit">Save Changes</flux:button>
    </flux:modal.footer>
</flux:modal>
```

**Props:**
- `name`: Unique identifier for the modal (required)
- `variant`: Modal style
  - Values: `"default"`, `"flyout"`
- `size`: Modal width
  - Values: `"sm"`, `"md"`, `"lg"`, `"xl"`, `"2xl"`

**Trigger Mechanisms:**
```blade
{{-- Via Alpine.js --}}
<flux:button @click="$modal.show('edit-profile')">Edit Profile</flux:button>

{{-- Via Livewire --}}
<flux:button wire:click="$dispatch('modal:show', { name: 'edit-profile' })">Edit</flux:button>
```

**Dismissal Patterns:**
- Click close button
- Press Escape key
- Click outside modal (backdrop)
- Programmatically: `$modal.close()`

### Tooltip
Contextual information on hover or focus.

**Basic Usage:**
```blade
<flux:tooltip content="Delete this item">
    <flux:button variant="ghost">
        <flux:icon.trash />
    </flux:button>
</flux:tooltip>
```

**Props:**
- `content`: Tooltip text (required)
- `position`: Tooltip placement
  - Values: `"top"`, `"bottom"`, `"left"`, `"right"`
- `kbd`: Keyboard shortcut to display
  - Example: `kbd="⌘D"` or `kbd="Ctrl+D"`

**Keyboard Integration:**
```blade
<flux:tooltip content="Save document" kbd="⌘S">
    <flux:button>Save</flux:button>
</flux:tooltip>
```

### Callout (Alert Alternative)
Flux UI's alert/notification component for important messages and announcements.

**Basic Usage:**
```blade
<flux:callout>
    <flux:callout.icon name="information-circle" />
    <flux:callout.heading>Important Notice</flux:callout.heading>
    <flux:callout.description>
        Please review the updated terms of service.
    </flux:callout.description>
</flux:callout>
```

**Variants:**
```blade
{{-- Success --}}
<flux:callout variant="success">
    <flux:callout.heading>Success!</flux:callout.heading>
    <flux:callout.description>Your payment was processed.</flux:callout.description>
</flux:callout>

{{-- Warning --}}
<flux:callout variant="warning">
    <flux:callout.heading>Warning</flux:callout.heading>
    <flux:callout.description>Your subscription expires soon.</flux:callout.description>
</flux:callout>

{{-- Danger --}}
<flux:callout variant="danger">
    <flux:callout.heading>Error</flux:callout.heading>
    <flux:callout.description>Failed to save changes.</flux:callout.description>
</flux:callout>
```

**Props:**
- `variant`: Visual style
  - Values: `"default"`, `"success"`, `"warning"`, `"danger"`, or any Tailwind color
- `inline`: Compact layout with actions beside content
  - Values: `true`, `false`

**Actions:**
```blade
<flux:callout>
    <flux:callout.heading>Update Available</flux:callout.heading>
    <flux:callout.description>A new version is ready to install.</flux:callout.description>
    <flux:callout.actions>
        <flux:button size="sm">Update Now</flux:button>
        <flux:button variant="ghost" size="sm">Later</flux:button>
    </flux:callout.actions>
</flux:callout>
```

### Loading Spinner
Built-in loading indicator for async operations.

**Basic Usage:**
```blade
{{-- Standalone spinner --}}
<flux:icon.loading class="animate-spin" />

{{-- With custom size --}}
<flux:icon.loading class="animate-spin w-8 h-8" />

{{-- With custom color --}}
<flux:icon.loading class="animate-spin text-blue-500" />
```

**Button Loading States:**
```blade
{{-- Automatic loading state --}}
<flux:button wire:click="save">
    Save Changes
</flux:button>

{{-- Disable automatic loading --}}
<flux:button wire:click="save" :loading="false">
    Save Changes
</flux:button>

{{-- Custom loading indicator --}}
<flux:button wire:click="save">
    <span wire:loading.remove>Save Changes</span>
    <span wire:loading class="flex items-center gap-2">
        <flux:icon.loading class="animate-spin" />
        Saving...
    </span>
</flux:button>
```

### Progress (Not Native - Custom Implementation)
While Flux UI doesn't include a native progress component, you can create one using Flux styling:

```blade
{{-- Simple progress bar --}}
<div class="w-full bg-gray-200 dark:bg-gray-700 rounded-full h-2">
    <div class="bg-blue-600 h-2 rounded-full transition-all duration-300"
         style="width: {{ $progress }}%">
    </div>
</div>

{{-- With label --}}
<div class="space-y-2">
    <div class="flex justify-between text-sm">
        <span>Uploading...</span>
        <span>{{ $progress }}%</span>
    </div>
    <div class="w-full bg-gray-200 dark:bg-gray-700 rounded-full h-2">
        <div class="bg-blue-600 h-2 rounded-full transition-all duration-300"
             style="width: {{ $progress }}%">
        </div>
    </div>
</div>
```

## Livewire Event Integration

### Toast Events
```php
// From any Livewire component
$this->dispatch('flux:toast', [
    'variant' => 'success',
    'message' => 'Operation completed!'
]);

// Listen for toast events
public function showToast($variant, $message)
{
    Flux::toast(variant: $variant, $message);
}
```

### Modal Events
```php
// Show modal
$this->dispatch('modal:show', ['name' => 'edit-profile']);

// Close modal
$this->dispatch('modal:close', ['name' => 'edit-profile']);

// Listen for modal events
protected $listeners = [
    'modal:closed' => 'handleModalClosed'
];

public function handleModalClosed($name)
{
    if ($name === 'edit-profile') {
        $this->reset(['editingProfile']);
    }
}
```

### Alpine.js Integration
```javascript
// Access modal instance
Alpine.data('customComponent', () => ({
    openModal() {
        this.$modal.show('my-modal');
    },
    
    closeModal() {
        this.$modal.close();
    }
}));

// Toast via Alpine
Alpine.data('notifications', () => ({
    showSuccess(message) {
        Livewire.dispatch('flux:toast', {
            variant: 'success',
            message: message
        });
    }
}));
```

### Animation/Transition Options
All Flux feedback components use Tailwind CSS transitions and Alpine.js for smooth animations:

- **Toast**: Slides in from edge with fade effect
- **Modal**: Fade in backdrop with scale/slide modal content
- **Tooltip**: Fade in/out with slight scale
- **Callout**: Static by default, can add custom transitions

Custom transition example:
```blade
<div x-show="open"
     x-transition:enter="transition ease-out duration-300"
     x-transition:enter-start="opacity-0 transform scale-90"
     x-transition:enter-end="opacity-100 transform scale-100"
     x-transition:leave="transition ease-in duration-200"
     x-transition:leave-start="opacity-100 transform scale-100"
     x-transition:leave-end="opacity-0 transform scale-90">
    {{-- Content --}}
</div>
```

## Typography & Icons Components (Referenced in other sections)

While not documented as a separate section, the following typography and icon components are used throughout Flux UI:

### Typography Components

#### flux:heading
Used for headings with various sizes:
```blade
<flux:heading>Default Heading</flux:heading>
<flux:heading size="sm">Small Heading</flux:heading>
<flux:heading size="lg">Large Heading</flux:heading>
<flux:heading size="xl">Extra Large Heading</flux:heading>
```

#### flux:text
Used for text content with variants:
```blade
<flux:text>Regular text content</flux:text>
<flux:text variant="dim">Dimmed text for secondary content</flux:text>
<flux:text size="sm">Small text</flux:text>
```

### Icon Components

#### flux:icon
Icon components follow a pattern of `flux:icon.{icon-name}`:
```blade
<flux:icon.check class="size-4" />
<flux:icon.trash />
<flux:icon.loading class="animate-spin" />
<flux:icon.currency-dollar class="text-gray-400" />
```

### Utility Components

#### flux:separator
Used to create visual separation between content sections:
```blade
<flux:separator />
<flux:separator variant="subtle" />
```

#### flux:spacer
Used in layouts to push content to opposite ends:
```blade
<flux:header>
    <flux:brand />
    <flux:spacer />
    <flux:profile />
</flux:header>
```

These components are integral to the Flux UI system but are primarily documented through their usage in other component examples rather than as standalone sections.

## Additional Components

### Button
A versatile button component with multiple variants, sizes, and states.

**Basic Usage:**
```blade
<flux:button>Click me</flux:button>
<flux:button variant="primary">Primary</flux:button>
<flux:button variant="destructive">Delete</flux:button>
```

**Props:**
- **variant** - Button style variant
  - Values: `"primary"`, `"secondary"`, `"ghost"`, `"destructive"`, `"outline"`
  - Default: `"secondary"`
- **size** - Button size
  - Values: `"sm"`, `"base"`, `"lg"`
  - Default: `"base"`
- **icon** - Icon name to display (uses Heroicons)
- **icon-trailing** - Show icon after text instead of before
- **type** - HTML button type
  - Values: `"button"`, `"submit"`, `"reset"`
  - Default: `"button"`
- **disabled** - Disable the button
- **wire:click** - Livewire click handler
- **wire:loading** - Show loading state automatically

**Examples:**
```blade
<!-- Icon buttons -->
<flux:button icon="trash" variant="destructive" size="sm" />
<flux:button icon-trailing="arrow-right">
    Next Step
</flux:button>

<!-- Loading state -->
<flux:button wire:click="save" wire:loading.attr="disabled">
    <span wire:loading.remove>Save</span>
    <span wire:loading>Saving...</span>
</flux:button>

<!-- Button group -->
<div class="flex gap-2">
    <flux:button variant="primary">Save</flux:button>
    <flux:button variant="ghost">Cancel</flux:button>
</div>
```

### Brand
A brand/logo component for displaying company branding in headers and navigation.

**Basic Usage:**
```blade
<flux:brand href="/" logo="/img/logo.png" name="Acme Inc." />
```

**Props:**
- **href** - Link destination for the brand
- **logo** - Path to logo image
- **name** - Company/brand name (used as alt text and fallback)
- **class** - Additional CSS classes

**Examples:**
```blade
<!-- In header -->
<flux:header>
    <flux:brand href="/" logo="/logo.svg" name="My Company" />
    <flux:spacer />
    <flux:navbar>
        <!-- Navigation items -->
    </flux:navbar>
</flux:header>

<!-- Text-only brand -->
<flux:brand href="/" name="Acme Inc." class="text-xl font-bold" />
```

### Dropdown
A versatile dropdown menu component with positioning and alignment options.

**Basic Usage:**
```blade
<flux:dropdown>
    <flux:button>Options</flux:button>
    
    <flux:menu>
        <flux:menu.item wire:click="edit">Edit</flux:menu.item>
        <flux:menu.item wire:click="duplicate">Duplicate</flux:menu.item>
        <flux:menu.separator />
        <flux:menu.item wire:click="delete" variant="destructive">
            Delete
        </flux:menu.item>
    </flux:menu>
</flux:dropdown>
```

**Props:**
- **position** - Dropdown position relative to trigger
  - Values: `"top"`, `"right"`, `"bottom"`, `"left"`
  - Default: `"bottom"`
- **align** - Alignment along the position axis
  - Values: `"start"`, `"center"`, `"end"`
  - Default: `"start"`
- **offset** - Distance from trigger in pixels
  - Default: `8`

**Sub-components:**
- `flux:menu` - Container for menu items
- `flux:menu.item` - Individual menu option
- `flux:menu.separator` - Visual separator between items
- `flux:menu.submenu` - Nested submenu
- `flux:menu.checkbox` - Checkbox menu item
- `flux:menu.radio` - Radio menu item

**Examples:**
```blade
<!-- User menu dropdown -->
<flux:dropdown position="bottom" align="end">
    <flux:profile name="{{ auth()->user()->name }}" />
    
    <flux:menu>
        <flux:menu.item icon="user">Profile</flux:menu.item>
        <flux:menu.item icon="cog">Settings</flux:menu.item>
        <flux:menu.separator />
        <flux:menu.item icon="logout" wire:click="logout">
            Sign out
        </flux:menu.item>
    </flux:menu>
</flux:dropdown>

<!-- Dropdown with submenus -->
<flux:dropdown>
    <flux:button>File</flux:button>
    
    <flux:menu>
        <flux:menu.item>New</flux:menu.item>
        <flux:menu.submenu>
            <flux:menu.item>Export</flux:menu.item>
            <flux:menu>
                <flux:menu.item>PDF</flux:menu.item>
                <flux:menu.item>CSV</flux:menu.item>
            </flux:menu>
        </flux:menu.submenu>
    </flux:menu>
</flux:dropdown>
```

### Accordion (Not Native - Implementation Pattern)
While Flux UI doesn't include a native accordion component, you can create one using Alpine.js with Flux styling:

**Implementation:**
```blade
<div class="space-y-2" x-data="{ active: null }">
    <!-- Accordion Item 1 -->
    <div class="rounded-lg border border-zinc-200 dark:border-zinc-700">
        <button
            @click="active = active === 1 ? null : 1"
            class="flex w-full items-center justify-between px-4 py-3 text-left font-medium hover:bg-zinc-50 dark:hover:bg-zinc-800"
        >
            <span>What is Flux UI?</span>
            <flux:icon 
                :name="active === 1 ? 'chevron-up' : 'chevron-down'"
                class="size-4 transition-transform"
            />
        </button>
        <div 
            x-show="active === 1" 
            x-collapse
            class="border-t border-zinc-200 px-4 py-3 dark:border-zinc-700"
        >
            <flux:text>
                Flux UI is a modern component library for Laravel and Livewire applications.
            </flux:text>
        </div>
    </div>
    
    <!-- Accordion Item 2 -->
    <div class="rounded-lg border border-zinc-200 dark:border-zinc-700">
        <button
            @click="active = active === 2 ? null : 2"
            class="flex w-full items-center justify-between px-4 py-3 text-left font-medium hover:bg-zinc-50 dark:hover:bg-zinc-800"
        >
            <span>How do I install Flux UI?</span>
            <flux:icon 
                :name="active === 2 ? 'chevron-up' : 'chevron-down'"
                class="size-4"
            />
        </button>
        <div 
            x-show="active === 2" 
            x-collapse
            class="border-t border-zinc-200 px-4 py-3 dark:border-zinc-700"
        >
            <flux:text>
                Install Flux UI via Composer and follow the setup instructions in the documentation.
            </flux:text>
        </div>
    </div>
</div>
```

### Calendar (Not Native - Use Date Picker)
For calendar functionality, use the `flux:date-picker` component which includes a full calendar interface. For custom calendar displays, implement using the date picker's calendar view:

**Using Date Picker as Calendar:**
```blade
<!-- Date picker with calendar -->
<flux:date-picker 
    wire:model="selectedDate"
    placeholder="Select a date"
/>

<!-- Date range picker -->
<flux:date-picker 
    wire:model="dateRange"
    range
    placeholder="Select date range"
/>
```

**Custom Calendar Grid:**
```blade
<!-- Custom calendar implementation -->
<div class="rounded-lg border border-zinc-200 p-4 dark:border-zinc-700">
    <div class="mb-4 flex items-center justify-between">
        <flux:heading size="lg">{{ now()->format('F Y') }}</flux:heading>
        <div class="flex gap-1">
            <flux:button icon="chevron-left" size="sm" variant="ghost" />
            <flux:button icon="chevron-right" size="sm" variant="ghost" />
        </div>
    </div>
    
    <!-- Calendar grid -->
    <div class="grid grid-cols-7 gap-1 text-center text-sm">
        <!-- Day headers -->
        @foreach(['S', 'M', 'T', 'W', 'T', 'F', 'S'] as $day)
            <div class="p-2 font-medium text-zinc-500">{{ $day }}</div>
        @endforeach
        
        <!-- Calendar days -->
        @for($i = 1; $i <= 31; $i++)
            <button class="aspect-square rounded p-2 hover:bg-zinc-100 dark:hover:bg-zinc-800">
                {{ $i }}
            </button>
        @endfor
    </div>
</div>
```

### Chart (Not Native - Integration Pattern)
Flux UI doesn't include native charting components. Integrate with popular charting libraries using Flux's styling system:

**Chart.js Integration:**
```blade
<flux:card>
    <flux:heading>Revenue Overview</flux:heading>
    <div class="mt-4">
        <canvas 
            wire:ignore
            x-data="chart"
            x-init="initChart()"
            id="revenueChart"
            class="h-64 w-full"
        ></canvas>
    </div>
</flux:card>

<script>
document.addEventListener('alpine:init', () => {
    Alpine.data('chart', () => ({
        chart: null,
        initChart() {
            const ctx = document.getElementById('revenueChart').getContext('2d');
            
            // Use CSS variables for consistent theming
            const styles = getComputedStyle(document.documentElement);
            const accentColor = styles.getPropertyValue('--color-accent');
            
            this.chart = new Chart(ctx, {
                type: 'line',
                data: @json($chartData),
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: {
                                color: $flux.dark ? '#fff' : '#000'
                            }
                        }
                    }
                }
            });
            
            // Update chart on theme change
            window.addEventListener('flux:dark-mode-toggled', () => {
                this.chart.update();
            });
        }
    }));
});
</script>
```

### Context (Context Menus)
Context menus in Flux UI are implemented using the dropdown component with right-click triggers:

**Implementation:**
```blade
<div 
    x-data="{ showContext: false, x: 0, y: 0 }"
    @contextmenu.prevent="
        showContext = true;
        x = $event.clientX;
        y = $event.clientY;
    "
    @click.away="showContext = false"
    class="relative"
>
    <!-- Content that can be right-clicked -->
    <flux:card class="p-8">
        <flux:text>Right-click anywhere in this card for context menu</flux:text>
    </flux:card>
    
    <!-- Context menu -->
    <div
        x-show="showContext"
        x-transition
        :style="`position: fixed; left: ${x}px; top: ${y}px;`"
        class="z-50"
    >
        <flux:menu class="min-w-48 rounded-lg border border-zinc-200 bg-white shadow-lg dark:border-zinc-700 dark:bg-zinc-900">
            <flux:menu.item icon="pencil">Edit</flux:menu.item>
            <flux:menu.item icon="duplicate">Duplicate</flux:menu.item>
            <flux:menu.item icon="share">Share</flux:menu.item>
            <flux:menu.separator />
            <flux:menu.item icon="trash" variant="destructive">Delete</flux:menu.item>
        </flux:menu>
    </div>
</div>
```

### Command (Pro Component)
The Command palette provides a searchable interface for quick actions, similar to VS Code's command palette.

**Basic Usage:**
```blade
<flux:command
    wire:model="commandSearch"
    placeholder="Type a command or search..."
>
    <flux:command.items>
        <flux:command.item 
            wire:click="createPost"
            icon="document-plus"
        >
            Create New Post
        </flux:command.item>
        
        <flux:command.item 
            wire:click="openSettings"
            icon="cog"
            kbd="⌘,"
        >
            Settings
        </flux:command.item>
        
        <flux:command.separator />
        
        <flux:command.group heading="Recent Documents">
            @foreach($recentDocs as $doc)
                <flux:command.item wire:click="openDoc({{ $doc->id }})">
                    {{ $doc->title }}
                </flux:command.item>
            @endforeach
        </flux:command.group>
    </flux:command.items>
</flux:command>

<!-- Global keyboard shortcut -->
<div x-data @keydown.cmd.k.window="$flux.command.open()">
    <!-- Your app content -->
</div>
```

**Props:**
- **wire:model** - Search input binding
- **placeholder** - Search placeholder text
- **empty-text** - Text shown when no results found

**Features:**
- Keyboard navigation (arrow keys)
- Fuzzy search
- Command groups
- Keyboard shortcuts display
- Global keyboard trigger

These components are integral to the Flux UI system but are primarily documented through their usage in other component examples rather than as standalone sections.

## Theming & Customization

### CSS Variables & Color System

Flux UI uses CSS variables for its theming system, providing a flexible and adaptive color scheme that automatically adjusts for dark mode.

#### Core CSS Variables

Flux uses three primary CSS variables for accent colors:

1. **`--color-accent`** - Base accent color (used for primary button backgrounds, etc.)
2. **`--color-accent-content`** - Stronger variant for thinner elements like text
3. **`--color-accent-foreground`** - Color that sits on top of the accent color (typically white or black)

#### Defining Custom Accent Colors

```css
/* resources/css/app.css */
@theme {
  --color-accent: var(--color-red-500);
  --color-accent-content: var(--color-red-600);
  --color-accent-foreground: var(--color-white);
}

@layer theme {
  .dark {
    --color-accent: var(--color-red-500);
    --color-accent-content: var(--color-red-400);
    --color-accent-foreground: var(--color-white);
  }
}
```

These variables are adaptive - they automatically change values in dark mode without requiring utility classes like `dark:bg-accent-dark`.

### Base Color Customization

Flux ships with "zinc" (gray) as the default base color, but you can use any gray shade by redefining the CSS variables:

```css
@theme {
  --color-zinc-50: var(--color-slate-50);
  --color-zinc-100: var(--color-slate-100);
  --color-zinc-200: var(--color-slate-200);
  --color-zinc-300: var(--color-slate-300);
  --color-zinc-400: var(--color-slate-400);
  --color-zinc-500: var(--color-slate-500);
  --color-zinc-600: var(--color-slate-600);
  --color-zinc-700: var(--color-slate-700);
  --color-zinc-800: var(--color-slate-800);
  --color-zinc-900: var(--color-slate-900);
  --color-zinc-950: var(--color-slate-950);
}
```

### Dark Mode Implementation

#### Configuration

To enable Flux's dark mode controls, configure Tailwind CSS to use the selector strategy:

```css
/* resources/css/app.css */
@import "tailwindcss";
@import '../../vendor/livewire/flux/dist/flux.css';
@custom-variant dark (&:where(.dark, .dark *));
```

By default, Flux handles appearance by adding a `dark` class to the `html` element based on user preference.

#### JavaScript Controls

Flux provides two JavaScript utilities for dark mode:

1. **`$flux.appearance`** - Get/set user's color scheme preference
   - Values: `'light'`, `'dark'`, `'system'`
   - Persists preference in localStorage
   
2. **`$flux.dark`** - Get/set current color scheme
   - Values: `true` (dark mode), `false` (light mode)

#### Implementation Examples

**Toggle Button:**
```html
<flux:button x-data x-on:click="$flux.dark = ! $flux.dark">
    Toggle Dark Mode
</flux:button>
```

**Dropdown Menu:**
```html
<flux:dropdown x-data>
    <flux:button>
        <flux:icon.sun x-show="! $flux.dark" />
        <flux:icon.moon x-show="$flux.dark" />
    </flux:button>
    
    <flux:menu>
        <flux:menu.item x-on:click="$flux.appearance = 'light'">
            <flux:icon.sun /> Light
        </flux:menu.item>
        <flux:menu.item x-on:click="$flux.appearance = 'dark'">
            <flux:icon.moon /> Dark
        </flux:menu.item>
        <flux:menu.item x-on:click="$flux.appearance = 'system'">
            <flux:icon.computer /> System
        </flux:menu.item>
    </flux:menu>
</flux:dropdown>
```

**Toggle Switch:**
```html
<flux:switch x-data x-model="$flux.dark" label="Dark mode" />
```

**Segmented Radio Control:**
```html
<flux:radio.group x-data x-model="$flux.appearance">
    <flux:radio value="light" label="Light" />
    <flux:radio value="dark" label="Dark" />
    <flux:radio value="system" label="System" />
</flux:radio.group>
```

#### Manual Control

To disable automatic appearance handling:

1. Remove `@fluxAppearance` directive from your layout
2. Manually control appearance with JavaScript utilities

### Component Customization

#### Level 1: Tailwind Overrides

Use Tailwind classes directly on components. Use `!` modifier for specificity:

```html
<flux:button class="bg-zinc-800! hover:bg-zinc-700! text-white!">
    Custom Button
</flux:button>
```

#### Level 2: Global Style Overrides

Target components using `data-flux-*` attributes:

```css
/* resources/css/app.css */
[data-flux-button] {
    @apply bg-zinc-800 hover:bg-zinc-700 dark:bg-zinc-600 dark:hover:bg-zinc-500;
}

[data-flux-input] {
    @apply border-2 border-zinc-300 dark:border-zinc-600;
}
```

#### Level 3: Publishing Components

For complete control, publish component Blade files:

```bash
# Publish specific component
php artisan flux:publish

# Publish all components
php artisan flux:publish --all
```

Published components are placed in `resources/views/flux/` and take precedence over package components.

### Component Variants

#### Accent Props

Many components support an `:accent` prop to opt out of accent coloring:

```html
<!-- Uses accent color -->
<flux:tabs>
    <flux:tab>Tab 1</flux:tab>
</flux:tabs>

<!-- Uses base color -->
<flux:tabs :accent="false">
    <flux:tab>Tab 1</flux:tab>
</flux:tabs>
```

Components supporting `:accent` prop:
- `flux:tabs`
- `flux:link`
- `flux:navbar`
- `flux:badge` (when clickable)

#### Size Variants

Many components support size variants via the `size` prop:

```html
<flux:button size="sm">Small</flux:button>
<flux:button size="base">Default</flux:button>
<flux:button size="lg">Large</flux:button>
```

#### Variant Classes

Common variant patterns:

```html
<!-- Button variants -->
<flux:button variant="primary">Primary</flux:button>
<flux:button variant="secondary">Secondary</flux:button>
<flux:button variant="danger">Danger</flux:button>
<flux:button variant="ghost">Ghost</flux:button>

<!-- Input variants -->
<flux:input variant="filled" />
<flux:input variant="outline" />
```

### Responsive Design Utilities

Flux components are built with mobile-first responsive design. Key patterns:

#### Responsive Modals & Drawers

Flux modals automatically adapt to screen size:

```html
<flux:modal>
    <!-- Becomes full-screen on mobile -->
    <flux:modal.body>
        Content adapts to viewport
    </flux:modal.body>
</flux:modal>
```

#### Responsive Grid Layouts

Use Tailwind's responsive prefixes with Flux components:

```html
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
    <flux:card>Card 1</flux:card>
    <flux:card>Card 2</flux:card>
    <flux:card>Card 3</flux:card>
</div>
```

#### Responsive Navigation

```html
<flux:navbar class="flex flex-col sm:flex-row">
    <flux:navbar.item class="w-full sm:w-auto">
        Responsive Item
    </flux:navbar.item>
</flux:navbar>
```

### Advanced Theming Techniques

#### Custom Theme Creation

Create completely custom themes by defining all color variables:

```css
/* Custom Purple Theme */
@theme {
  /* Light mode */
  --color-accent: var(--color-purple-500);
  --color-accent-content: var(--color-purple-600);
  --color-accent-foreground: var(--color-white);
  
  /* Override specific component colors */
  --color-danger: var(--color-pink-500);
  --color-warning: var(--color-amber-500);
  --color-success: var(--color-emerald-500);
}

@layer theme {
  .dark {
    /* Dark mode overrides */
    --color-accent: var(--color-purple-400);
    --color-accent-content: var(--color-purple-300);
    --color-accent-foreground: var(--color-zinc-900);
  }
}
```

#### Dynamic Theme Switching

Implement runtime theme switching:

```javascript
// Alpine.js component for theme switcher
Alpine.data('themeSwitcher', () => ({
    themes: {
        blue: {
            accent: 'var(--color-blue-500)',
            content: 'var(--color-blue-600)',
            foreground: 'var(--color-white)'
        },
        green: {
            accent: 'var(--color-green-500)',
            content: 'var(--color-green-600)',
            foreground: 'var(--color-white)'
        },
        purple: {
            accent: 'var(--color-purple-500)',
            content: 'var(--color-purple-600)',
            foreground: 'var(--color-white)'
        }
    },
    
    setTheme(themeName) {
        const theme = this.themes[themeName];
        const root = document.documentElement;
        
        root.style.setProperty('--color-accent', theme.accent);
        root.style.setProperty('--color-accent-content', theme.content);
        root.style.setProperty('--color-accent-foreground', theme.foreground);
        
        // Persist preference
        localStorage.setItem('flux-theme', themeName);
    },
    
    init() {
        const savedTheme = localStorage.getItem('flux-theme') || 'blue';
        this.setTheme(savedTheme);
    }
}));
```

#### Color Space

Flux leverages Tailwind CSS 4's modern `oklch` color space for more vibrant and consistent colors across different displays.

### Best Practices

1. **Use CSS Variables** - Define theme colors in CSS rather than inline styles
2. **Respect Dark Mode** - Always define both light and dark variants
3. **Test Accessibility** - Ensure color contrasts meet WCAG guidelines
4. **Progressive Enhancement** - Start with Tailwind utilities, then customize as needed
5. **Maintain Consistency** - Use Flux's theme builder for cohesive color schemes

### Theme Builder

For the easiest theming experience, use Flux's interactive theme builder at [fluxui.dev/themes](https://fluxui.dev/themes) to:
- Preview themes in real-time
- Generate CSS variable definitions
- Export complete theme configurations

## Advanced Features & Best Practices

### Performance Optimization

#### Component Lazy Loading

Optimize initial page load by lazy loading heavy components:

```blade
<!-- Only load when visible -->
<div wire:init="loadHeavyComponent">
    @if($componentLoaded)
        <flux:data-table :data="$data" />
    @else
        <flux:spinner />
    @endif
</div>
```

#### Debouncing and Throttling

Optimize search and filter operations:

```blade
<!-- Debounce search input -->
<flux:input 
    wire:model.live.debounce.300ms="search"
    placeholder="Search..."
/>

<!-- Throttle scroll events -->
<div 
    x-data="{ scrolling: false }"
    @scroll.window.throttle.150ms="scrolling = true"
>
    <!-- Content -->
</div>
```

### Accessibility Guidelines

#### ARIA Labels and Descriptions

All Flux components support accessibility attributes:

```blade
<flux:button 
    aria-label="Delete item"
    aria-describedby="delete-help"
>
    <flux:icon name="trash" />
</flux:button>
<span id="delete-help" class="sr-only">
    This will permanently delete the item
</span>
```

#### Keyboard Navigation

Flux components implement proper keyboard navigation:

- **Tab** - Navigate between focusable elements
- **Space/Enter** - Activate buttons and links
- **Arrow Keys** - Navigate menus and lists
- **Escape** - Close modals and dropdowns

```blade
<!-- Keyboard shortcut hints -->
<flux:tooltip content="Save (⌘S)">
    <flux:button @keydown.cmd.s.window="save">
        Save
    </flux:button>
</flux:tooltip>
```

#### Screen Reader Support

Use semantic HTML and proper labeling:

```blade
<flux:field>
    <flux:label for="email">Email Address</flux:label>
    <flux:input 
        id="email"
        type="email"
        wire:model="email"
        aria-required="true"
        aria-invalid="@error('email') true @enderror"
        aria-describedby="email-error"
    />
    @error('email')
        <flux:error id="email-error">{{ $message }}</flux:error>
    @enderror
</flux:field>
```

### SEO Considerations

#### Dynamic Meta Tags

Implement dynamic meta tags with Livewire:

```php
// In your Livewire component
public function mount()
{
    $this->dispatch('meta:update', [
        'title' => $this->article->title,
        'description' => $this->article->excerpt,
        'image' => $this->article->featured_image
    ]);
}
```

```blade
<!-- In your layout -->
<head>
    @stack('meta')
    <script>
        window.addEventListener('meta:update', event => {
            document.title = event.detail.title;
            // Update other meta tags
        });
    </script>
</head>
```

#### Structured Data

Add schema markup to Flux components:

```blade
<article itemscope itemtype="https://schema.org/Article">
    <flux:card>
        <flux:heading itemprop="headline">
            {{ $article->title }}
        </flux:heading>
        <flux:text itemprop="description">
            {{ $article->excerpt }}
        </flux:text>
    </flux:card>
</article>
```

### Testing Strategies

#### Component Testing with Livewire

Test Flux components in Livewire:

```php
use Livewire\Livewire;

test('modal opens when triggered', function () {
    Livewire::test(UserProfile::class)
        ->call('openEditModal')
        ->assertDispatched('modal:open', id: 'edit-profile');
});

test('form validates required fields', function () {
    Livewire::test(ContactForm::class)
        ->set('email', '')
        ->call('submit')
        ->assertHasErrors(['email' => 'required']);
});
```

#### Browser Testing with Dusk

Test Flux UI interactions:

```php
public function testDropdownNavigation()
{
    $this->browse(function (Browser $browser) {
        $browser->visit('/dashboard')
            ->click('[data-flux-dropdown-trigger]')
            ->waitFor('[data-flux-dropdown-menu]')
            ->assertSee('Profile')
            ->click('[data-flux-menu-item="profile"]')
            ->assertPathIs('/profile');
    });
}
```

### Common Patterns

#### Form Wizard with Steps

Implement multi-step forms:

```blade
<div x-data="{ step: 1 }">
    <!-- Progress indicator -->
    <flux:breadcrumbs>
        <flux:breadcrumbs.item :active="step >= 1">
            Personal Info
        </flux:breadcrumbs.item>
        <flux:breadcrumbs.item :active="step >= 2">
            Contact Details
        </flux:breadcrumbs.item>
        <flux:breadcrumbs.item :active="step >= 3">
            Review
        </flux:breadcrumbs.item>
    </flux:breadcrumbs>

    <!-- Step content -->
    <div x-show="step === 1">
        <!-- Personal info fields -->
    </div>
    
    <!-- Navigation -->
    <flux:button 
        @click="step++"
        :disabled="!$wire.canProceed"
    >
        Next
    </flux:button>
</div>
```

#### Infinite Scroll

Implement infinite scrolling with Flux components:

```blade
<div 
    x-data="{ observer: null }"
    x-init="
        observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    @this.loadMore()
                }
            })
        })
        observer.observe($refs.trigger)
    "
>
    @foreach($items as $item)
        <flux:card>
            <!-- Item content -->
        </flux:card>
    @endforeach
    
    <div x-ref="trigger" wire:loading.class="hidden">
        <flux:spinner />
    </div>
</div>
```

### Migration Guide

#### From Other UI Libraries

Migrating from Bootstrap/Tailwind UI to Flux:

```blade
<!-- Before (Bootstrap) -->
<div class="modal fade" id="myModal">
    <div class="modal-dialog">
        <div class="modal-content">
            <!-- Content -->
        </div>
    </div>
</div>

<!-- After (Flux) -->
<flux:modal name="myModal">
    <!-- Content -->
</flux:modal>
```

#### Component Mapping

Common component replacements:

| Other Library | Flux Equivalent |
|--------------|-----------------|
| `btn btn-primary` | `flux:button` |
| `form-control` | `flux:input` |
| `alert alert-success` | `flux:toast type="success"` |
| `card` | `flux:card` |
| `nav nav-tabs` | `flux:tabs` |
| `breadcrumb` | `flux:breadcrumbs` |

### Pro Features Summary

Flux Pro includes these additional components:

1. **flux:autocomplete** - Advanced search with suggestions
2. **flux:date-picker** - Full-featured date selection
3. **flux:editor** - Rich text editing
4. **flux:command** - Command palette (like VS Code)
5. **flux:tabs** - Advanced tabbed navigation
6. **flux:pagination** - Data pagination
7. **flux:data-table** - Advanced data tables

### Best Practices Summary

1. **Component First** - Always check if Flux has a component before building custom
2. **Consistent Theming** - Use CSS variables for all color customizations
3. **Accessibility Always** - Every interactive element should be keyboard accessible
4. **Performance Matters** - Lazy load heavy components and debounce user input
5. **Test Everything** - Write tests for component interactions and state changes
6. **Dark Mode Ready** - Always consider dark mode when styling
7. **Mobile First** - Design for mobile and enhance for desktop
8. **Semantic HTML** - Use proper HTML elements for better SEO and accessibility

### Quick Reference

#### Component Hierarchy

```
flux:header
└── flux:navbar
    └── flux:navbar.item
        
flux:sidebar
├── flux:navlist
│   ├── flux:navlist.item
│   └── flux:navlist.group
└── flux:sidebar.toggle

flux:main
└── [Your content with Flux components]
```

#### Common Props

Most Flux components accept these common props:

- **class** - Additional CSS classes
- **variant** - Component style variant
- **size** - Component size (sm, base, lg)
- **disabled** - Disable interaction
- **wire:model** - Livewire data binding
- **wire:click** - Livewire method calls
- **x-data** - Alpine.js data
- **x-show/x-if** - Alpine.js conditionals

#### Event Reference

Common Flux events:

- `modal:open` - Open a modal by name
- `modal:close` - Close a modal
- `toast:show` - Display a toast notification
- `dropdown:toggle` - Toggle dropdown state
- `tab:change` - Switch active tab

This completes the comprehensive Flux UI documentation with all components, features, and best practices for building modern Laravel applications with Livewire and Flux UI.