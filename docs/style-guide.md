# Style Guide

The intention of this document is to guide how we should write TypeScript and CSS/SASS. The document should be considered as work-in-progress and PR's with corrections etc. are much appreciated.

## Table of Contents

- [Language](#language)
- [React Component](#react-component)
- [Documentation](#documentation)
- [Importing](#importing)
- [TypeScript Style Guide](#typescript-style-guide)
- [React JS Style Guide](#react-js-style-guide)
- [CSS Modules & SASS](#css-modules--sass)
- [CSS Variables](#css-variables)
- [ESLint](#eslint)
- [Out-Commented Code](#out-commented-code)

## Language

Use US English spelling to be consistent with the other dev teams.

## React Component

We aim to only write functional components using hooks and memo. Here is a simple example of a functional component:

```tsx
import { memo, useState } from "react";
import styles from "./Example.module.scss"; // if using sass

interface ExampleProps = {
  /** Title of example. */
  title: string;
};

/**
 * This is an example component
 */
const Example = ({ title }: ExampleProps) => {
  const [count, setCount] = useState(0);

  return (
    <div className={styles.container}>
      <h1>{title}</h1>
      <button onClick={() => setCount(count + 1)}>
        count #{count}
      </button>
    </div>
  )
};

export default memo(Example);
```

> **Why not import React?**\
> It is not necessary to `import React` anymore as React 17 is using the new JSX Transform, as you can read [here](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html).
>
> **Why not FC (React.FC / React.FunctionalComponent)?**\
> It is discourages to use `React.FC` as mentioned here in the [React+TypeScript Cheatsheets](https://github.com/typescript-cheatsheets/react#function-components).

## Documentation

Every TS file should always contain inline documentation, we follow a combination of [ESDoc](https://esdoc.org/manual/tags.html) and [JSDoc](http://usejsdoc.org/). This makes it easy for every developer to see what the purpose of the file is. As an example see this simple class component:

```tsx
import { memo } from "react";
import styles from "./Header.module.scss";

interface UserProfileProps = {
  /** Full name of the user. */
  name: string;
};

/**
 * A component to show User details
 */
const UserProfile = ({ name }: UserProfileProps) => {
  return (
    <div className={styles.container}>
      {name}
    </div>
  )
};

export default memo(UserProfile);
```

## Importing

In order to have our code be much cleaner, more maintainable, and generally easier to write, we want to use absolute imports when importing files that are not siblings or children or within the same feature. Whether it be for our _JavaScript_ / _TypeScript_, or _SASS_. Basically that means whenever we would write `../` to import a file, we generally want to use absolute imports instead, but further down you can see examples for the exceptions.

### JS / TS

When setting up a new project, remember to edit the `tsconfig.json`/`jsconfig.json` file, and add `"baseUrl": "src"` to `compilerOptions`, like so:

```tsx
{
  "compilerOptions": {
    "baseUrl": "src"
  }
}
```

This allows us to import modules in a much cleaner way, using absolute paths instead of relative paths.

```tsx
// GOOD
import Header from "components/Header/Header";

// BAD
import Header from "../../../../../../components/Header/Header";
```

#### Exceptions (Siblings and Children)

As explained above, we want to use relative imports when it comes to importing sibling files, or children. For example when trying to import a components stylesheet.

```tsx
import styles from "./Header.module.scss";
```

Or, when importing sub-components.

```tsx
import CalendarHeader from "./components/CalendarHeader/CalendarHeader";
```

#### Exceptions (Features)

For features, we also do an exception, and prefer to use relative imports when we are importing files within a feature. This is important because we can end up with circular dependencies if we import files from the feature's own [barrel](https://basarat.gitbook.io/typescript/main-1/barrel). For example, if we have a file inside a Permission feature, then we would use the relative path to get it:

```tsx
import { PermissionDef } from "../types/permissionDef";
```

### SASS

In order to be able to do the same with your _SASS_ imports, you need to add the following to your `.env` file.

```bash
SASS_PATH=src
```

Then you'll be able to import other SASS files like so.

```scss
// GOOD
@import "styles/variables";

// BAD
@import "../../../../../styles/variables";
```

## TypeScript Style Guide

We are to some extent following the [JavaScript Style Guide by Airbnb](https://github.com/airbnb/javascript).

## React JS Style Guide

To a large extent we are following [Airbnb's React Style Guide](https://github.com/airbnb/javascript/tree/master/react), however we are doing a few things differently:

- **Extensions**: Use `.tsx` extension for components files and `.ts` for non-component files.

- **No index**: Do not name any files `index.tsx` except the root file, as it will make it difficult to perform a search for the file and the tabs in the IDE will say index.tsx, so it can be difficult to quickly locate which tab you want to edit.

- **Component/Function Naming**:
  - PascalCase for all components
  - camelCase for helper classes, configurations, globals, etc.

## CSS Modules & SASS

For React JS projects, we will mainly use [SASS](https://sass-lang.com/) as it allows us to specify global variables for the theme, such as colors, sizes, animations, etc.

We use [CSS Modules](https://github.com/css-modules/css-modules), so it is not necessary to define unique class names between components as all class names will automatically be made unique when injected into the DOM. However, when creating components, we should still try to be consistent, descriptive, and explicit in the naming so for example:

```tsx
<div className={styles.container}>
  <div className={styles.card}>{content}</div>
  <button
    className={cx(styles.button, {
      [styles.buttonActive]: isActive,
    })}
  >
    {buttonLabel}
  </button>
</div>
```

Note, that when we want to have multiple classes we can use [classnames (or cx)](https://github.com/JedWatson/classnames), as well as adding classes conditionally as seen in the example above.

## CSS Variables

If the project allows it, then consider using CSS Variables to specify global variables for themes, such as colors, spacing, etc.

## ESLint

In order to follow the style guidelines, we use ESLint together with `prettier` and `prettier-eslint`, which on save will automatically format your code or highlight any violations you might have made.

## Out-Commented Code

Don't leave out-commented code in the project. Or if you feel you really need to, also leave a comment saying why that code is there and why it might be needed again. But in general, delete commented out code. We use git, so you can always get old code from there.
