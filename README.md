# vuetify-optimized-deps
Small project to demonstrate a build issue with vuetify

## Issue

When using Vite with Vuetify 3.10.5 and adding `vuetify/components/*` to the `optimizeDeps.include` configuration, the **dev server** fails with the following error:

```
✘ [ERROR] Could not resolve "./VOverflowBtn.css"

    node_modules/vuetify/lib/components/VOverflowBtn/VOverflowBtn.js:5:7:
      5 │ import "./VOverflowBtn.css";
        ╵        ~~~~~~~~~~~~~~~~~~~~
```

**Note**: The production build (`npm run build`) succeeds, but the dev server (`npm run dev`) fails during the dependency optimization phase.

## Reproduction Steps

1. Install dependencies:
   ```bash
   npm install
   ```

2. Try to run the dev server:
   ```bash
   npm run dev
   ```

3. The dev server will fail with the error shown above during the dependency optimization phase.

## Configuration

The issue is caused by the following configuration in `vite.config.js`:

```javascript
optimizeDeps: {
  include: [
    'vuetify/components/*'
  ]
}
```

## Expected Behavior

Vite's dev server should be able to optimize Vuetify components when using wildcard patterns in `optimizeDeps.include`, or at least provide a clear error message about the unsupported pattern.

## Actual Behavior

The dev server fails with a CSS resolution error during the dependency optimization phase. The production build works fine, but development is blocked.

