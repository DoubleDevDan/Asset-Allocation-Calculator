# Asset Allocation Calculator - Vue.js Web App

This repository contains a small web application built using Vue.js that serves as a simple asset allocation calculator. The app allows users to determine how many BTC and ETH they should buy to maintain a 70/30 split of their total available funds ($X).

## Table of Contents

- [Introduction](#introduction)
- [Project Setup](#project-setup)
  - [Installing the Project](#installing-the-project)
  - [Compile and Hot-Reload for Development](#compile-and-hot-reload-for-development)
  - [Type-Check, Compile and Minify for Production](#type-check-compile-and-minify-for-production)
  - [Run End-to-End Tests with Playwright](#run-end-to-end-tests-with-playwright)
  - [Lint with ESLint](#lint-with-eslint)
- [Running Storybook](#running-storybook)
- [Project Documentation](#project-documentation)
  - [Spike: Technical Stack / Package Selection](#spike-technical-stack--package-selection)
  - [ Implemenation: App Development Process](#implemenation-app-development-process)
    - [Vue.js](#vuejs)
    - [Storybook](#storybook)
    - [Pinia](#pinia)
    - [MUI](#mui)
    - [Currency Conversion](#currency-conversion)
    - [Testing](#testing)
- [Take Home Assignment - JustWorks](#take-home-assignment-justworks)
- [Wireframe](#wireframe)
- [Currency Conversion](#currency-conversion)

## Introduction

The goal of this project is to create a simple asset allocation calculator web app using Vue.js.

## Project Setup

### Installing the Project

To begin working with the asset allocation calculator, follow these steps:

1. Clone this repository to your local machine.
2. Ensure you have Node.js and npm installed on your system.
3. Open a terminal and navigate to the project's root directory.
4. Install the required dependencies by running the following command:

   ```sh
   npm install
   ```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Run End-to-End Tests with [Playwright](https://playwright.dev)

```sh
# Install browsers for the first run
npx playwright install

# When testing on CI, must build the project first
npm run build

# Runs the end-to-end tests
npm run test:e2e
# Runs the tests only on Chromium
npm run test:e2e -- --project=chromium
# Runs the tests of a specific file
npm run test:e2e -- tests/example.spec.ts
# Runs the tests in debug mode
npm run test:e2e -- --debug
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

### Running Storybook

To explore Vue components and get a better understanding of how the app's UI components are designed and structured, we will use Storybook, an interactive development environment for UI components. To run Storybook, execute the following command:

```sh
npm run storybook
```

Visit the provided URL in your web browser to interact with the Storybook environment and view the different Vue components in action.

## Project Documentation

### Spike: Technical Stack / Package Selection

Before diving into the JustWorks take-home assignment, it was essential to gain some knowledge of the technologies that would be required to build the app. The following technologies were researched / used while building the asset allocation calculator:

- **Vue.js**

  - https://vuejs.org/guide/introduction.html

  - Vue.js is a progressive JavaScript framework used for building user interfaces. It emphasizes declarative rendering and component-based architecture, making it easy to create interactive and reusable UI components.

  - I chose to use v3.3 of Vue.js for this project because it is the latest stable release of Vue.js and provides the most up-to-date features and functionality.

- **Vite**

  - https://vitejs.dev/guide/

  - Vite is a fast build tool that enhances the development experience with Vue.js projects. It leverages native ES modules to provide rapid development and hot module replacement without relying on a bundler during development.
  - https://github.com/vitejs/vite-plugin-vue/tree/main/packages/plugin-vue-jsx
  - Vite also provides a plugin for Vue.js JSX support. This plugin allows you to use JSX in Vue.js components

- **Storybook**

  - https://storybook.js.org/docs/vue/get-started/introduction

  - Storybook is an open-source tool for developing UI components in isolation. It allows you to browse a component library, view the different states of each component, and interactively develop and test components. Leveraging Storybook not only gives additional functionality and documentation to the assignment, but also adds some structure to the application.

  - The decision was made to build the UI following a Component-Driven Development (CDD) methodology. It’s a process that builds UIs from the “bottom-up”, starting with components and ending with screens. CDD helps you scale the amount of complexity you’re faced with as you build out the UI. It also allows focus on the small details of the UI, which will be important translating the high-fidelity mocks into a fully functional UI.

  - Storybook also helps with catching accessibility issues early on in the development process. It provides a11y tools that can be used to test the accessibility of the UI components.

    ```sh
    npm add --dev @storybook/addon-a11y
    ```

  - Storybook also gives some testing coverage to the project giving it the ability to run testing through Storybook's 'test runner'. This standalone utility is powered by Playwright and allows you to run tests against your Storybook stories.

    ```sh
    npm add --dev @storybook/test-runner
    ```

  - **yarn**

    - https://yarnpkg.com/

    - Yarn is a package manager for JavaScript. Most of the documentation for the technologies used in this project leveraged yarn for installing dependencies, so yarn was the intiial package manager for this project. However, when encountering an issue with a dependency, it was required to use npm to install the dependency to resolve the issue ( https://github.com/storybookjs/storybook/issues/22431 ). Using yarn's import functionality, we should have been able to import the dependencies installed with npm into yarn's lockfile.

      ```sh
      yarn import
      ```

    - However, this functionality was not working as expected, either providing the below erro after multiple attempts to rebuild the lockfile the decision was made to use npm to install all dependencies for the sake of time. This is something that could be revisited in the future.
      `error Failed to import from package-lock.json, source file(s) corrupted`

  - **degit**

    - https://github.com/Rich-Harris/degit

    - While working through the documentation on Storybook for how to set up a Vue.js project, I came across a tool called degit. degit is a CLI tool that allows you to clone a git repository without the git history. They leveraged this tool to create a Vue.js template that can be used to quickly set up a Vue.js project with Storybook.

  - **pinia**

    - https://github.com/vuejs/pinia

    - While working through the Vue Storybook documentation, I was exposed to pinia. Pinia is a Vue.js state management library that provides a similar API to Vuex but uses the new Vue 3 API. It is a lightweight alternative to Vuex that leverages the new Composition API to provide a more intuitive and type-safe way of managing state in Vue.js applications.

    - pinia has a dependency on 'vue-demi', which is a set of helpers that allows you to use Vue 2.x APIs in Vue 3.x. It is a temporary solution until all Vue 2.x APIs are ported to Vue 3.x. This dependency was broken in the Vue Storybook template, the solution was to manually install it which remedied the issue.

      ```sh
      npm add vue-demi
      ```

- **MUI**

  - https://mui.com/getting-started/usage/
  - https://github.com/vuematerial/vue-material

  - My current go-to for building UIs is Material UI. It is a React UI framework that provides a set of React components that implement Google's Material Design specification. It is a great framework for building UIs quickly and efficiently.
  - However, since this project is built using Vue.js, I decided to use the Vue Material library, which provides a set of Vue components that implement the Material Design specification.

### Implemenation: App Development Process

#### Vue.js

The first step in the process was to setup the Vue.js project. This was done by leveraging

```sh
npm init vue@latest
```

per the Vue.js documentation. This command creates a new Vue.js project using the latest version of Vue.js. It also provides the option to add additional features to the project, such as TypeScript, Progressive Web App (PWA) support, and Router support. For this project, I chose to add TypeScript support to the project. The script's README can be found at README_2.md.

## Take Home Assignment - JustWorks

The take-home assignment for JustWorks involves building an asset allocation calculator as a small web app. The app's primary functionality is to allow users to input a specific amount ($X) they want to allocate between BTC and ETH using a 70/30 split. Based on this input, the app will calculate how many units of BTC and ETH the user should buy.

For this assignment, focus on creating the best possible user experience and don't be constrained by the wireframe provided. Feel free to showcase your skills and creativity in designing the app.

See assets/asset_allocation_exercise.txt

## Wireframe

A wireframe illustrating a possible layout for the asset allocation calculator is available in the "assets/asset_allocation_wireframe.png" file. Please note that this wireframe is not a high-fidelity mock and serves only as a basic guideline for the app's layout.

## Currency Conversion

To perform any necessary currency conversion, the following exchange rates endpoint was provided:

` https://api.coinbase.com/v2/exchange-rates?currency=USD
 [//]`
