# RemixYarnInvestigation

The following are the steps taken to reproduce this repository

# Setup Workspace and nx remix project

```sh
# Setup nx workspace
npx create-nx-workspace remix-yarn-investigation

# ✔ Which stack do you want to use? · react
# ✔ What framework would you like to use? · none
# ✔ Integrated monorepo, or standalone project? · integrated
# ✔ Application name · app-react
# ✔ Which bundler would you like to use? · vite
# ✔ Test runner to use for end to end (E2E) tests · playwright
# ✔ Default stylesheet format · css
# ✔ Set up CI with caching, distribution and test deflaking · skip
# ✔ Would you like remote caching to make your build faster? · skip


# Open Project
cd remix-yarn-investigation
# or
code -r remix-yarn-investigation

# Generate remix project
yarn nx add @nx/remix
npx nx generate @nx/remix:application --directory=apps/app-remix --name=app-remix --e2eTestRunner=playwright --projectNameAndRootFormat=as-provided --no-interactive


# Running tasks works
yarn nx run app-remix:lint
yarn nx run app-remix:typecheck
yarn nx run app-remix:build
yarn nx run app-remix:test
yarn nx run app-remix:serve
yarn nx run app-remix:start
yarn nx run app-remix-e2e:e2e

```

# Upgrade yarn from 1 to berry/4

```sh
yarn --version # @1.22.21 by default
corepack enable
```

add the following line to the `package.json` file

```json
  "packageManager": "yarn@4.1.0",
```

run yarn to upgrade

```sh
yarn
```

add the followiung to a `.yarnrc.yml` file in the workspace root

```yml
nodeLinker: node-modules
enableGlobalCache: false
```

add the following line to the `.gitignore` file in the workspace root

```sh
# Yarn files
.yarn
!.yarn/cache
!.yarn/patches
!.yarn/plugins
!.yarn/releases
!.yarn/sdks
!.yarn/versions
```

# Running remix tasks no longer works

```sh
yarn nx run app-remix:lint # failed can't find eslint
yarn nx run app-remix:typecheck # success
yarn nx run app-remix:build # success
yarn nx run app-remix:test # failed can't find vitest
yarn nx run app-remix:serve # failed with message about package composition
yarn nx run app-remix:start # success
yarn nx run app-remix-e2e:e2e # failed with message about package composition

```
