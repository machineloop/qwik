# Starters

This folder stores "starter" projects for the CLI. The idea is that during the CLI execution, the developer can choose a particular starter app and combine it with a specific server and features.

All starters are based off of `starters/apps/base`, to include the `package.json` and `tsconfig.json`. Depending on the options the user selects, their starter merges into the `base` app.

## Developer

Here are steps to try out the CLI in local environment.

1. From root, build CLI:

   ```
   # npm build.cli
   ```

1. Run CLI:

   ```
   # node ./packages/create-qwik/dist/create-qwik.cjs
   🐰 Let's create a Qwik app 🐇

   ✔ Where would you like to create your new project? … ./qwik-app

   ✔ Select a starter › Basic App (QwikCity)

   ✔ Would you like to install npm dependencies? … yes

   ✔ Installing npm dependencies...


   🦄  Success!  Project created in qwik-app directory

   🐰 Next steps:
      cd qwik-app
      npm start

   🔌 Integrations? Add Netlify, Cloudflare, Tailwind...
      npm run qwik add
   ```

1. Change to generated location
   ```
   cd qwik-app
   npm install
   npm start
   ```
   
### Testing new starters locally using npm-link:

1. Starting at root of the project, change directory to local qwik package, then run `npm link`:

   ```
   cd packages/qwik
   npm link
   ```
1. Generate a test project (ie.. qwik-app), either using regular CLI or following steps under [#Developer](README.md#developer) heading above.
1. Change directory into new qwik project, then run `npm link qwik`:
   ```
   cd qwik-app
   npm link qwik
   ```
1. Then run `npm install </path/to/packages/qwik>`, modify the PATH to match the relative location of qwik package on disk:
   ```
   npm install ../packages/qwik
   ```
1. Test your new starter adapter, you should see your new option when executing:
   ```
   npm run qwik add
   ``` 
1. When finished testing with linked qwik test build, remove the link using the following command:
   ```
   npm rm --global qwik
   ```

## Publishing `create-qwik` CLI Package

The starter CLI is published at the same time as `@builder.io/qwik`. When published, the CLI will update the `base` app's package.json to point to the published version of Qwik.

The base app's package.json's devDependencies are updated with:

```json
{
  "devDependencies": {
    "@builder.io/qwik": "<QWIK_VERSION_BEING_PUBLISHED>",
    "typescript": "<SAME_AS_ROOT_PACKAGE>",
    "vite": "<SAME_AS_ROOT_PACKAGE>"
  }
}
```
