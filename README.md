# Asset Allocation Calculator - Vue.js Web App

This repository contains a small web application built using Vue.js that serves as a simple asset allocation calculator. The app allows users to determine how many BTC and ETH they should buy to maintain a 70/30 split of their total available funds ($X).<!-- pagebreak -->

## Table of Contents

- [Introduction](#introduction)
- [Project Setup](#project-setup)
- [Installing the Project](#installing-the-project)
- [Running Storybook](#running-storybook)
- [Project Documentation](#project-documentation)
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
   `bash
npm install
`

### Running Storybook

To explore Vue components and get a better understanding of how the app's UI components are designed and structured, we will use Storybook, an interactive development environment for UI components. To run Storybook, execute the following command:

`bash
 npm run storybook
 `

Visit the provided URL in your web browser to interact with the Storybook environment and view the different Vue components in action.

## Project Documentation

Before diving into the JustWorks take-home assignment, it was essential to gain some knowledge of the technologies that would be required to build the app. The following technologies were used to build the asset allocation calculator:

- Vue.js
  https://vuejs.org/guide/introduction.html

Vue.js is a progressive JavaScript framework used for building user interfaces. It emphasizes declarative rendering and component-based architecture, making it easy to create interactive and reusable UI components.

- Vite

  - https://vitejs.dev/guide/

  - Vite is a fast build tool that enhances the development experience with Vue.js projects. It leverages native ES modules to provide rapid development and hot module replacement without relying on a bundler during development.

- Storybook

  - https://storybook.js.org/docs/vue/get-started/introduction

  - Storybook is an open-source tool for developing UI components in isolation. It allows you to browse a component library, view the different states of each component, and interactively develop and test components. The decision was made to build the UI following a Component-Driven Development (CDD) methodology. It’s a process that builds UIs from the “bottom-up”, starting with components and ending with screens. CDD helps you scale the amount of complexity you’re faced with as you build out the UI. It also allows focus on the small details of the UI, which will be important translating the high-fidelity mocks into a fully functional UI.

- MUI

  - https://mui.com/getting-started/usage/
    https://www.creative-tim.com/vuematerial/getting-started

  - My current go-to for building UIs is Material UI. It is a React UI framework that provides a set of React components that implement Google's Material Design specification. It is a great framework for building UIs quickly and efficiently.
  - However, since this project is built using Vue.js, I decided to use the Vue Material library, which provides a set of Vue components that implement the Material Design specification.

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
