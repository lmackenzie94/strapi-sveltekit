# Strapi + SvelteKit = ❤️

## Notes

-   initially, trying to query content (ex. posts) at `http://localhost:1337/posts`n will be forbidden
    -   need to set rules & permissions for specific rules.
    -   ex. Settings > Roles > Public (✅ count, ✅ find, ✅ findone) will allow these read-only actions to unauthenticated users.

**Create SvelteKit Project**

-   make a 'frontend' folder and `npm init svelte@next`
-   clear out `src/lib/` and `src/routes/`
-   create `src/routes/index.svelte`

**Install Tailwind**

-   `npx svelte-add tailwindcss` (why svelte-add?)

    ***

-   `__layout.svelte` is a special file that adds a layout to every page.
    -   can have multiple (i.e. within subdirectories)
-   fetch blog posts using _SvelteKit Endpoints_
    -   Endpoints in SvelteKit are files ending with .js (or .ts for TypeScript) that export functions corresponding to HTTP methods. These endpoint files become API routes in our application.

**Dynamic Routing**

-   If we enclose a string in brackets ([]) in a filename of a route, that becomes a parameter.
    -   `src/routes/blog/[post].svelte`, the route maps to `/blog/ANY_STRING` where ANY_STRING will be the value of the post parameter.

**Authentication & Authorization**

-   Strapi allows us to configure third-party providers like Google, but we'll stick to the good ol' email and password sign-in.
-   create a store in src/lib/user.ts that will house the User to access the User in any component.
-   to persist the user store, we need to re-fetch the User every time the page reloads. We need a `load` function in `__layout.svelte` since it is present on every page.
