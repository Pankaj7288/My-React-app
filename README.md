# My-React-app

## Getting Started with Create React App

The most common approach is to use Create React App:

```sh
npx create-react-app my-project
cd my-project
```

## Setting up Tailwind CSS

Tailwind CSS requires Node.js 12.13.0 or higher.
Install Tailwind and its peer-dependencies using yarn:

```sh
yarn add -D tailwindcss@npm:@tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```

## Install and configure CRACO

Since Create React App doesn’t let you override the PostCSS configuration natively, we also need to install CRACO to be able to configure Tailwind:

```sh
yarn add @craco/craco
```

Once it’s installed, update your `scripts` in your `package.json` file to use `craco` instead of `react-scripts` for all scripts except `eject`:

```json

"scripts": {
     "start": "craco start",
     "build": "craco build",
     "test": "craco test",
     "eject": "react-scripts eject"
    },

```

Next, create a `craco.config.js` at the root of our project and add the `tailwindcss` and `autoprefixer` as PostCSS plugins:

```js
// craco.config.js
module.exports = {
  style: {
    postcss: {
      plugins: [require("tailwindcss"), require("autoprefixer")],
    },
  },
};
```

## Create your configuration file

Next, generate your `tailwind.config.js` file:

```sh
npx tailwindcss-cli@latest init
```

This will create a minimal `tailwind.config.js` file at the root of your project.
Next, configure your `tailwind.config.js` file:

```js
// tailwind.config.js
module.exports = {
  purge: ["./src/**/*.{js,jsx,ts,tsx}", "./public/index.html"],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
};
```

## Include Tailwind in your CSS

Open the `./src/index.css` file that Create React App generates for you by default and use the `@tailwind` directive to include Tailwind’s `base`, `components`, and `utilities` styles, replacing the original file contents:

```css
/* ./src/index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Finally, ensure your CSS file is being imported in your `./src/index.js` file:

```js
// src/index.js
import React from "react";
import ReactDOM from "react-dom";

import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById("root")
);

// ...
```

## Linting Setup

In order to lint and format your React project automatically according to popular airbnb style guide, I recommend you to follow the instructions below.

### Install Dev Dependencies

```sh
yarn add -D prettier
yarn add -D babel-eslint
npx install-peerdeps --dev eslint-config-airbnb
yarn add -D eslint-config-prettier eslint-plugin-prettier
```

### Create Linting Configuration file manually

Create a `.eslintrc` file in the project root and enter the below contents:

```json
{
  "extends": [
    "airbnb",
    "airbnb/hooks",
    "eslint:recommended",
    "prettier",
    "plugin:jsx-a11y/recommended"
  ],
  "parser": "babel-eslint",
  "parserOptions": {
    "ecmaVersion": 8
  },
  "env": {
    "browser": true,
    "node": true,
    "es6": true,
    "jest": true
  },
  "rules": {
    "react/react-in-jsx-scope": 0,
    "react-hooks/rules-of-hooks": "error",
    "no-console": 0,
    "react/state-in-constructor": 0,
    "indent": 0,
    "linebreak-style": 0,
    "react/prop-types": 0,
    "jsx-a11y/click-events-have-key-events": 0,
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [".js", ".jsx"]
      }
    ],
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 100,
        "tabWidth": 4,
        "semi": true,
        "endOfLine": "auto"
      }
    ]
  },
  "plugins": ["prettier", "react", "react-hooks"]
}
```

## Editor Settings

Follow the below settings for VS Code -

Create a new folder called ".vscode" inside the project root folder
Create a new file called "settings.json" inside that folder.
Paste the below json in the newly created settings.json file and save the file.

```json
{
  // editor
  "workbench.colorTheme": "Learn with Sumit Theme", //Theme
  "editor.fontSize": 20,
  "editor.fontFamily": "Operator Mono Lig, Victor Mono, Fira Code",
  "editor.fontLigatures": true,
  "editor.wordWrap": "on",
  "editor.minimap.enabled": false,
  "editor.tokenColorCustomizations": {
    "textMateRules": [
      {
        "scope": "comment",
        "settings": {
          "fontStyle": "italic"
        }
      }
    ]
  },
  // cursor
  "editor.cursorSmoothCaretAnimation": true,
  "editor.cursorBlinking": "expand",
  // config related to code formatting
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "[javascript]": {
    "editor.formatOnSave": false,
    "editor.defaultFormatter": null
  },
  "[javascriptreact]": {
    "editor.formatOnSave": false,
    "editor.defaultFormatter": null
  },
  "javascript.validate.enable": false, //disable all built-in syntax checking
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.fixAll.tslint": true,
    "source.organizeImports": true
  },
  "eslint.format.enable": true,
  "eslint.alwaysShowStatus": true,

  // emmet
  "emmet.triggerExpansionOnTab": true,
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },

  //tailwindCSS

  "tailwindCSS.emmetCompletions": true,
  "tailwindCSS.includeLanguages": {
    "javascript": "javascript",
    "html": "HTML"
  },
  //others
  "javascript.updateImportsOnFileMove.enabled": "always",
  "files.autoSave": "afterDelay"
}
```

### Thanks
