---
sidebar_position: 1
---

Add this to `vite.config.ts`. This allow you to use absolute path such as `import DataViewer from "@components/DataViewer/DataViewer";`.

```ts
  resolve: {
    alias: {
      "@components": "/src/components",
      "@layouts": "/src/layouts",
      "@pages": "/src/pages",
    },
  },
```

Add this to the `tsconfig.json`. This allow the editor (such as VSCode editor) to recognize the import statement when you use absolute path instead of relative path. Without this, the import will still work, but VSCode will give curly red line below the path statement.

```js
{
  "compilerOptions": {
    /* for VSCode to recorgnize import/export with absolute paths*/
    "baseUrl": "./src",
    "paths": {
      "@components/*": ["components/*"],
      "@layouts/*": ["layouts/*"],
      "@pages/*": ["pages/*"]
    }
  }
}
```

Therefore, whenever you write an import statement with absolute path such as

```js
`import DataViewer from "@components/DataViewer/DataViewer";`;
```

it will resolve to

```js
`import DataViewer from ".src/components/DataViewer/DataViewer";`;
```
