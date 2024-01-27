# Import SVG as react component using vite

## install plugin

```sh
npm i -D vite-plugin-svgr
```

## update vite config

```ts
// vite.config.ts
import { defineConfig } from "vite";
import svgr from "vite-plugin-svgr";
// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    // ... other plugins
    svgr(),
  ],
});
```

## add plugin's type definition or you'll get a type error

You only have to add one line onto the top of the `vite-env.d.ts` in the `src` folder.

```ts
//vite-env.d.ts
/// <reference types="vite-plugin-svgr/client" />
```

## import svg and start coding

note the `?react` suffix.

```tsx
import Star from "~/assets/star.svg?react";

export const Demo = () => <Star />;
```
