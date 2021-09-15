# Folder Structure

This document describes how we structure our web project with the aim of creating a scalable and maintainable codebase.

## React JS

Almost everything in a React project is a component. But in order to increase readability of a project, and aid the developers in finding their way around the code, several folders on different levels should be created as explained in this document. So instead of referring to everything as components or classes, we have this very high level abstraction, where we have two parts:

- **features**: Code that is related to a specific feature, such as users, projects, etc.
- **shared**: Code that is generic or global, so it can be used across the features.

So, to break it down further, you will have the following folder structure:

---

src/

- [api/](#api)
- [components/](#components)
- [constants/](#constants)
- [features/](#features)
- [helpers/](#helpers)
- [layouts/](#layouts)
- [localization/](#localization)
- [routes/](#routes)
- [store/](#store)
- [storybook/](#storybook)
- [styles/](#styles)
- [types/](#types)

---

### Api

This folder contains the API instance with interceptors for requests and responses.

```bash
api/
    api.ts
```

### Components

This folder contains general or global components, meaning a component that can be used multiple places throughout the app, such as a button, modal, etc. They are usually quite configurable, and are used in combination with other global components to create specific components in a screen. All global components can be used alone or inside other components, and should not have any styling that relies on its parent/environment.

Each component can also consist of several subcomponents, which are either only relevant for the main component or a way to group several components of same type.

> **Naming**: To allow easy search for files, keep the names short and prefix the subcomponents with the full or partial name of the parent.

#### Example: Subcomponent only relevant for parent component

```bash
Breadcrumb/
    Breadcrumb.tsx
    components/
        BreadcrumbItem/
            BreadcrumbItem.tsx
```

Here the `BreadcrumbItem` must only be used in the Breadcrumb, simply to reduce complexity of the Breadcrumb file. If this structure is respected, then we know that modifying theses subcomponents, eg. `BreadcrumbItem`, will only affect the parent component. In some cases the subcomponents will also have its own set of subcomponents, where the same logic then applies.

#### Example: Subcomponents to group several similar components

```bash
Icon/
    Icon.tsx
    components/
        IconChevron/
        IconClose/
        ...
```

Here all the icons in the components folder are exported by the `Icon` component that functions as a [Higher Order Component (HOC)](https://reactjs.org/docs/higher-order-components.html), in order to reuse as much logic as possible, and keep each subcomponent neat and without logic. This means that you will never refer directly to a subcomponent. This also has the added advantage of import paths becoming shorter.

### Helpers

Reusable functions that are not part of the business logic should go in here. This could be functions that simply manipulates a string, calculates a number, and so on. Before writing any new functions from scratch, make it a habit to check if [Lodash](https://lodash.com/) already does it.

### Layouts

Some components will have no other purpose than purely specifying the layout of components. For example, a typical layout could consist of a side-panel, a navbar, and a content area. That layout might then be shared across several screens. So in order to reuse as much structure and styling as possible, components that are defining the layout should be placed in the `layouts` folder.

### Localization

Configurations and locale translation files should go into this folder. [React i18next](https://github.com/i18next/react-i18next) is used for translation of text. Whenever possible, use [NStack](https://nstack.io/) for hosting the localization, and use the [NStack JS SDK](https://github.com/nstack-io/javascript-sdk) for utilization.

### Features

We utilize a feature-first organization. This means that high level features such as users, projects, settings, etc get their own relatively isolated directory. Each of these features will have files grouped by type, so that it will be easy to navigate and get an immediate overview of what the feature contains.

The folders will usually be the same as what we have in the root of the project, so:

```bash
users/
  users.ts
  users.md
  api/
  components/
  constants/
  screens/
  helpers/
  logic/
  types/
```

The idea is that a feature should be able to be moved to a separate repository. To make it clearer what is public and what is private for a feature, you will add a [barrel](https://basarat.gitbook.io/typescript/main-1/barrel) that re-exports all of the internal functions and variables, that can be consumed by other parts of the project.

In addition, there should be a `markdown` file in the root of the feature folder, to explain what the feature is responsible for as well as how to use it with some examples.

#### Feature naming convention

To make it easier to find files in the feature, the files should be prefixed with the feature's name. For example, for constants in a `users` feature, we would name the file: `users.constants.ts`. This has the advantage that we can easily search for the files as the name is unique.

For more about naming convention, go to the [Style Guide](./style-guide.md).

#### Screens

All the screens for the feature will go here. The screens can contain general components and feature-specific components which are only relevant for this feature. The following structure resembles a tree structure, where the root is all the main screens (nodes) with links (branches) to their subcomponents and subscreens (nodes).

> **Naming**: All screens should be postfixed with "Screen", to allow easier file search and clarification.

```bash
HomeScreen/
    HomeScreen.tsx
    components/
        HomeHeader/
        HomeHero/
    partials/
        HomeSidebarMenu/
    screens/
        HomeDetailScreen.tsx
```

The screens can have subcomponents, eg. `HomeHeader` and `HomeHero`, these components are specific for this screen and its subscreens, and are not used in any other screens on the same level. This means, that if `HomeHero` was modified, it would only affect `HomeScreen` and potentially the subscreens, which removes the risk of breaking other screens in the rest of the app.

Each screen can have several subscreens, which are screens only accessible from the parent screen. In this example, the `HomeDetailScreen` could be a screen displayed when a certain item in the `HomeScreen` was clicked. As mentioned before, the `HomeDetailScreen` is allowed to use the subcomponents from the parent or its own subcomponents, if any.

#### Logic

The business logic for each features goes into this folder. The goal is to keep this folder as small as possible, as most business logic should be conducted in the backend and not in the frontend. However, sometimes it can be necessary to manipulate data before sending it to the API, or storing it in the redux store.

### Storybook

If [storybook](https://github.com/storybooks/storybook) is to be used in the project, then components that are only used in the stories, such as wrapper components, will be placed in the `storybook` folder.

### Styles

Global styling and configurations will be added to this folder. If the project uses Sass, then it will also contain the theme colors, breakpoints and fonts. The fonts should be added to a folder under the `styles` folder. If the project uses material-ui, the theme configuration will be added here.

### Types

The shared types for TypeScript will be added here:

```bash
types/
    api.types.ts
    table.types.ts
```

### Constants

The global constants and enums are defined in this folder. For example, an API event status could be defined as follows:

```tsx
export enum ResponseStatusEnum = {
  SUCCESS = 200,
  CREATED = 201,
};
```
