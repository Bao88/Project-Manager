Project Manager
Using NextJS + TailwindCSS and Node Framework

# An Express + Typescript + Mocha + Nyc + Eslint + Nodemon + Prettier Template Generator

This is a template for expressjs + typescript projects. It bootstraps a template project with [some popular packages](#Configuration-Files) and some pre-configured [npm script commands](#NPM-Scripts).

The entry point of the app is `src/server.ts`

## NPM Scripts

### Development Commands

A `.env` file should be created first. In this template, `.env` file is used for creating environment variables in the local dev environment. This file is used for local dev only, it is NOT used in the deployed environment (e.g. test, staging, prod etc). How you want to build env variables in your CI/CD process is not in the scope of this template.

- `npm run dev` - start the app in development mode (it reads the local .env file)
- `npm run test:dev` - run tests locally (reads local .env)
- `npm run test:watch` - run tests locally (reads local .env) in watch mode
- `npm run lint` - run eslint
- `npm run format` - run prettier
- `npm run build:dev` - build typescript with source maps and comments in code are kept
- `npm run mocha` - a helper npm script for running customised mocha command e.g. test a single file `npm run mocha -- file-name-or-pattern`

### Production Commands

Production commands do not read the `.env` file. How you want to build environment variables in production environments is not in the scope of this template.

Do NOT use production commands in the local development environment. They might NOT work as expected because these commands may reply environment variables from the actual environments.

- `npm start` - start application
- `npm build` - compile typescript with no source maps and comments are removed from ts files
- `npm test` - run tests and coverage report

### NODE_PATH

`NODE_PATH` used in scripts are for improving the readability of `import` statements e.g. Relative paths like `import someModule from '../../../utils/module'` can be written as `import someModule from 'src/utils/module'`

## Quality Control

This project has been configured with three steps of code quality controls

### Pre-Commit Hook

`eslint --fix` is triggered before each commit. This command tries to fix linting errors when it is possible.

`eslint` has been configured to also check and fix formatting errors detected by `prettier`. (https://prettier.io/docs/en/integrating-with-linters.html)

### Pre-Push Hook

`npm run test:dev` is triggered before each push. Push will fail if tests fail or test coverage is below the threshold defined in `./.nycrc`.

`npm run audit` is triggered before each push. Push will fail if there are vulnerabilities in dependencies. You should run `npm audit fix` to fix the vulnerabilities and commit the changes before you push again.
