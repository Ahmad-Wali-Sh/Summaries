# Diasy UI 

`Summary by Ahmad Wali Sharify`

### A Tailwind CSS pre-built classes for UI components      

<br> 

# Installation
```
npm i -D daisyui@latest
```

**tailwind.css.config**
```javascript
module.exports = {
    //...
    plugins: [require('daisyui')],
}
```

<br>

# Customization 
You Have:
```html
<button class='btn'>Button</button>
```
you can customize it like:
```html
<button class='btn btn-primary btn-outline rounded-full px-16'>Button</button>
```
or:

**main.css**
```css
.btn {
  @apply rounded-full;
}
```

## This is how to change themes:

```html
function MyAwesomeThemeComponent() {
  const [theme, setTheme] = React.useState('light');
  const toggleTheme = () => {
    setTheme(theme === 'dark' ? 'light' : 'dark');
  };
  // initially set the theme and "listen" for changes to apply them to the HTML tag
  React.useEffect(() => {
    document.querySelector('html').setAttribute('data-theme', theme);
  }, [theme]);
  return (
    <label className="swap swap-rotate">
      <input onClick={toggleTheme} type="checkbox" />
      <div className="swap-on">DARKMODE</div>
      <div className="swap-off">LIGHTMODE</div>
    </label>
  );
}

```

<br>

# Config 

```javascript
module.exports = {
  //...

  // add daisyUI plugin
  plugins: [require("daisyui")],

  // daisyUI config (optional - here are the default values)
  daisyui: {
    themes: false, // true: all themes | false: only light + dark | array: specific themes like this ["light", "dark", "cupcake"]
    darkTheme: "dark", // name of one of the included themes for dark mode
    base: true, // applies background color and foreground color for root element by default
    styled: true, // include daisyUI colors and design decisions for all components
    utils: true, // adds responsive and modifier utility classes
    rtl: false, // rotate style direction from left-to-right to right-to-left. You also need to add dir="rtl" to your html tag and install `tailwindcss-flip` plugin for Tailwind CSS.
    prefix: "", // prefix for daisyUI classnames (components, modifiers and responsive class names. Not colors)
    logs: true, // Shows info about daisyUI version and used config in the console when building your CSS
  },

  //...
}

```

<br>

# Colors 

> - primary
> - primary-focus
> - primary-content
> - secondary
> - secondary-focus
> - secondary-content
> - accent
> - accent-focus
> - accent-content
> - neutral
> - neutral-focus
> - neutral-content
> - base-100, 200, 300
> - base-content
> - info
> - info-content
> - success
> - success-content
> - warning
> - warning-content
> - error
> - error-content

<br>

# Themes 

```javascript 

module.exports = {
  //...
  daisyui: {
    themes: ["light", "dark", "cupcake"],
  },
}

// <html data-theme="cupcake"></html>

module.exports = {
  //...
  daisyui: {
    themes: [
      "light",
      "dark",
      "cupcake",
      "bumblebee",
      "emerald",
      "corporate",
      "synthwave",
      "retro",
      "cyberpunk",
      "valentine",
      "halloween",
      "garden",
      "forest",
      "aqua",
      "lofi",
      "pastel",
      "fantasy",
      "wireframe",
      "black",
      "luxury",
      "dracula",
      "cmyk",
      "autumn",
      "business",
      "acid",
      "lemonade",
      "night",
      "coffee",
      "winter",
    ],
  },
}

// to create own theme:
module.exports = {
  //...
  daisyui: {
    themes: [
      {
        mytheme: {
          "primary": "#a991f7",
          "secondary": "#f6d860",
          "accent": "#37cdbe",
          "neutral": "#3d4451",
          "base-100": "#ffffff",
        },
      },
      "dark",
      "cupcake",
    ],
  },
}
// you can use theme generator at https://daisyui.com/theme-generator/

```

# Links 

https://daisyui.com/
