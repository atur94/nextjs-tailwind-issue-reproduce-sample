Reproduce steps

1. Create project with `npx create-next-app@latest my-project --experimental-app --typescript --eslint`
2. Install tailwind needed packages `npm install -D tailwindcss@latest postcss@latest autoprefixer@latest`
3. Initialize tailwind config files with: `npx tailwindcss init -p`
4. Remove all built in styles in `app/globals.css`
5. Add imports to `globals.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

6. Clean `app/page.tsx` and leave on simple `div`
7. Remove `app/page.module.css`
8. Replace content of `tailwind.config.js` with

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./app/**/*.{js,ts,jsx,tsx}", "./pages/**/*.{js,ts,jsx,tsx}", "./components/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

Simple scenario is set and ready to test

1. Add color class to `app/page.tsx` for example `bg-red-500`
2. Run app with `npm run dev`
3. Enter `localhost:3000`
4. Change background color class to something different(ex. `bg-red-600`) and save file
5. File `.next/static/css/app_globals_css.css` has updated and added class exists at the end of file
6. Background color on the page disappears because `css` file is not reloaded and new class does not exist in currently loaded file
7. Reload page manually - change should be now visible
8. Change background class again
9. Add anything to `app/globals.css` and save it, still css is not refreshed

After each step in the developer console message `[Fast Refresh] rebuilding` is printed. In the terminal, log below is printed

```
wait  - compiling...
event - compiled client and server successfully in 178 ms (332 modules)
```

Tested on chrome, firefox and microsoft edge.

## Workaround for chrome

1. Open developer console
2. Go to settings -> workspace
3. Add folder `~/.next/static/css`
4. After that step, all the css changes should be visible immidiately after fast refresh
