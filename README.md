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
      plugins: [
        require('tailwindcss'),
        require('autoprefixer'),
      ],
    },
  },
}

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

   purge: ['./src/**/*.{js,jsx,ts,tsx}', './public/index.html'],
    darkMode: false, // or 'media' or 'class'
    theme: {
      extend: {},
    },
    variants: {
      extend: {},
    },
    plugins: [],
  }
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
  import React from 'react';
  import ReactDOM from 'react-dom';

 import './index.css';
  import App from './App';
  import reportWebVitals from './reportWebVitals';

  ReactDOM.render(
    <React.StrictMode>
      <App />
    </React.StrictMode>,
    document.getElementById('root')
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
        // "singleQuote": true,
        "printWidth": 100,
        // "tabWidth": 4,
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
  "[javascript]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "vscode.typescript-language-features"
  },
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
    "source.fixAll.tslint": true,
    "source.organizeImports": true
  },
  "eslint.alwaysShowStatus": true,
  //terminal
  "terminal.integrated.fontSize": 16,
  "terminal.integrated.fontWeight": "normal",
  "terminal.integrated.fontFamily": "MesloLGS NF, Operator Mono Lig, Victor Mono, Fira Code",
  "workbench.iconTheme": "vscode-icons",
  // terminal customization
  "workbench.colorCustomizations": {
    "terminal.background": "#031c2b",
    "terminal.foreground": "#bb71b5",
    "terminalCursor.background": "#FAC03B",
    "terminalCursor.foreground": "#FAC03B",
    "terminal.ansiBlack": "#1D2021",
    "terminal.ansiBlue": "#0D6678",
    "terminal.ansiBrightBlack": "#665C54",
    "terminal.ansiBrightBlue": "#0D6678",
    "terminal.ansiBrightCyan": "#8BA59B",
    "terminal.ansiBrightGreen": "#95C085",
    "terminal.ansiBrightMagenta": "#8F4673",
    "terminal.ansiBrightRed": "#FB543F",
    "terminal.ansiBrightWhite": "#FDF4C1",
    "terminal.ansiBrightYellow": "#FAC03B",
    "terminal.ansiCyan": "#8BA59B",
    "terminal.ansiGreen": "#95C085",
    "terminal.ansiMagenta": "#8F4673",
    "terminal.ansiRed": "#FB543F",
    "terminal.ansiWhite": "#A89984",
    "terminal.ansiYellow": "#FAC03B"
  },
  "editor.formatOnPaste": true,
  "terminal.integrated.defaultProfile.windows": "PowerShell",
  "workbench.colorTheme": "Learn with Sumit Theme",//Theme
  "security.workspace.trust.untrustedFiles": "open",
  "files.associations": {
    "*.json": "json",
    "*.js": "javascript"
  },
  "tabnine.experimentalAutoImports": true,
  "window.zoomLevel": 1,
  "code-runner.clearPreviousOutput": true,
  "code-runner.runInTerminal": false,
  "code-runner.showExecutionMessage": false,
  "code-runner.saveFileBeforeRun": true,
  "code-runner.defaultLanguage": "JavaScript",
  "bracketPairColorizer.highlightActiveScope": true,
  "turboConsoleLog.includeFileNameAndLineNum": false,
  "turboConsoleLog.logMessagePrefix": "",
  "turboConsoleLog.quote": "`",
  "terminal.integrated.cursorStyle": "line",
  "terminal.integrated.cursorBlinking": true,
  "eslint.format.enable": true,
  "tailwindCSS.emmetCompletions": true,
  "tailwindCSS.includeLanguages": {
    "javascript": "javascript",
    "html": "HTML"
  },
  "editor.quickSuggestions": {
    "strings": true
  },
  "javascript.updateImportsOnFileMove.enabled": "always",
  "files.autoSave": "afterDelay",
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  }
}

```

### Thanks
