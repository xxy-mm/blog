# using tailwind in vite react app

## install

- init react project using vite

```bash
npm create vite@latest my-project -- --template react
cd my-project
```

- install tailwindcss

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

> the `-p` argument tells tailwind to generate a `postcss.config.js`

- configure your template paths

```js
// tailwind.config.js

/** @type {import('tailwindcss').Config} */
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

- add the tailwind directives to your css

```css
/* ./src/index.css */

@tailwind base;
@tailwind components;
@tailwind utilities;
```

> vscode will complain no such directives, just ignore the error, it does not matter

- install vscode extension `Tailwind CSS IntelliSense` for tailwind intellisense.

- if you're using prettier, you can optionally install `prettier-plugin-tailwindcss` as a dev dependency then add the config below:

```json
// .prettierrc

{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```

> this will sort your class names, but it's not recommended to use this plugin when 'auto format on save' is turned on, since you will lose the focus of the editing class name.

- if you're also using eslint, to make eslint compatible with prettier, you an install `eslint-config-prettier` as a dev dependency and add rules below to your eslint config.

```js
// eslintrc.js

module.exports = {
  ...
  extends: [
    ...
    "prettier", // add this line
  ],
}
```

- one problem using tailwindcss is the class names are usually too long, which makes the code unreadable. Fortunately, vscode has a plugin to resolve this: `Tailwind Fold`. Just install the plugin and start coding!
