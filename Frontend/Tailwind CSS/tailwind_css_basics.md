# Tailwind CSS

`Summary by Ahmad Wali Sharify`

### a "Utility First" CSS framework to rapidly build modern websites without ever leaving your HTML

### Main Benefits:

- You aren't wasting energy inventing class names.
- your CSS stops Growing
- Making changes feels safer. because it is locally, not global
- Responsive Design like md: sm: and more
- Hover, Focus, dark and other states  
  <br>

# Integration With React Vite

First create your Vite Project.

then:

```
npm install -D tailwindcss postcss autoprefixer
```

then generate the config file for your tailwind CSS:

```
npx tailwindcss init -p
```

and then change config:

‍‍‍‍‍‍‍‍‍*tailwind.config*

```javascript title="css.css"
module.exports = {
  content: ["./src/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

then add these to your index.css:

_main.css_

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

# Utilites

Tailwind CSS has a configuration file gives you more control over the patterns and names Tailwind looks for.
utilities have a pattern of syntax. text-{size}.

Tailwind CSS has a command-line tool that generates only the classes you used.

```
npx tailwindcss -o build.css --minify
```

also Tailwind provides a set of defaults for things like sizing and colors.

but you can use arbitrary values like: m-[104px]

<br>

# Preflights

When you install Tailwind CSS, you import:

- **@tailwind base**: contains Tailwind's reset stylesheet called Preflight.

- **@tailwind components**: is quite small, that has box classes.
- **@tailwind utilities**: is the bulk point of Tailwind CSS

disable preflight like this:

_tailwind.config_

```javascript
module.exports = {
  corePlugins: {
    preflight: false,
  }
```

<br>

# Reusing Styles

You should know how to manage duplication in Tailwind CSS.

You can use your own technology and system to manage Tailwind CSS duplication.

In React you can use:

```jsx
const MyApp = () => {
  const title = () => {
    return "text-6xl font-bold";
  };
  return <Component className={title}>Cool Text</Component>;
};
```

## **@apply** property:

it lets you use Tailwind CSS classes in the definition of other CSS selector.

_main.css_

```css
@layer components {
  .title {
    @apply text-6xl font-bold;
  }
  .subtitle {
    @apply text-4xl font-semibold;
  }
  .subsubtitle {
    @apply text-lg font-medium italic;
  }
}
```

_index.html_

```html
<div class="title text-5xl">Title</div>
```

<br>

# Hover, Focus, Other States

Every Utility class in Tailwind CSS can be applied conditionally by adding a `modifier` in the beginning.

> bg-sky-700 hover:bg-sky-800

They Are:

> :hover, :focus, :first-child, :required, :visited,
> :focus-within, :focus-visible, :first, :last, :odd,
> :even, :invalid, :disabled, :placeholder, :file,
> :selection, :print:hidden
> ::before, ::after, ::placeholder, ::selection

it can be stacked:

> dark:md:hover:bg-fuchsia-600

<br>

# Reponsive Design

Every Utility Class can be conditional at different breakpoints.

> Five Breakpoints:
>
> - sm > 640px
> - md > 768 px
> - lg > 1024 px
> - xl > 1280px
> - 2xl > 1536px

Example:

```html
<img class="w-16 md:w-32 lg:w-48" />
```

## Working Mobile-First:

By default, Tailwind uses a mobile-first breakpoints.
you need to use `unprefixed version` of utility for mobile!

start from mobile, then sm, md and etc.

_tailwind.config.js_

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
    theme:
      {screens:
          {'tablet': '640px',
          // => @media (min-width: 640px) { ... }
          'laptop': '1024px',// => @media (min-width: 1024px) { ... }
          'desktop': '1280px',// => @media (min-width: 1280px) { ... }},
      }
}
```

<br>

# Dark Mode

To use Dark Mode:

Toggling dark mode manually by adding class:

_tailwind.config.js_

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  darkMode: "class",
};
```

> dark mode will be applied if html container tag has class='dark'

<br>

# Adding Custom Styles

Customizing your theme:

want to change color palette, spacing scale, typography, scale and breakpoints, use theme.

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  theme: {
    screens: {
      sm: "480px",
      md: "768px",
      lg: "976px",
      xl: "1440px",
    },
    colors: {
      blue: "#1fb6ff",
      pink: "#ff49db",
      orange: "#ff7849",
      green: "#13ce66",
      "gray-dark": "#273444",
      gray: "#8492a6",
      "gray-light": "#d3dce6",
    },
    fontFamily: {
      sans: ["Graphik", "sans-serif"],
      serif: ["Merriweather", "serif"],
    },
    extend: {
      spacing: {
        128: "32rem",
        144: "36rem",
      },
      borderRadius: {
        "4xl": "2rem",
      },
      colors: {
        tone: {
          50: "#fdf8f6",
          100: "#f2e8e5",
          200: "#eaddd7",
          300: "#e0cec7",
          400: "#d2bab0",
          500: "#bfa094",
          600: "#a18072",
          700: "#977669",
          800: "#846358",
          900: "#43302b",
        },
        prime: "#fdasd2",
        second: "#asdfsdf",
        success: "#dfsaf12",
        error: "red",
        white: "white",
      },
    },
  },
};
```

<br>

# Tailwind Utilites CSS Cheat Sheet

## https://nerdcave.com/tailwind-cheat-sheet
