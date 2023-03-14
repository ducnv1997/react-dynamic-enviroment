# react-dynamic-environment 🎛

Load environment variables dynamically in production for your React applications created with CRA (Create-React-App).

A wrapper version of [react-dotenv](https://www.npmjs.com/package/react-dotenv)


# Installation

```sh
npm install react-dynamic-environment
```

# Usage

## 1. Set up your project

Open your project's `package.json` file and:

1. Add an `.env` file to your project root (or just load from the system environment variables).
1. Add the `react-dynamic-environment` NPM command to your `start`, `build` (and your `serve` commands).
1. Add the `react-dynamic-environment.whitelist` property to `package.json` to specify which variables you need exposed. (Required only if your project does not have a .env file during build)

### Example

**package.json**:
```js
{
  "name": "my-react-app",
  "version": "0.1.0",
  "dependencies": {
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-dynamic-environment": "^0.1.0",
    "react-scripts": "3.4.3",
    "serve": "^11.3.2"
  },
  "scripts": {
    "start": "react-dynamic-environment && react-scripts start", // <-- append command
    "build": "react-dynamic-environment && react-scripts build", // <-- append command
    "serve": "react-dynamic-environment && serve build", // <-- append command
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": "react-app"
  },
  "browserslist": {
    "production": [">0.2%", "not dead", "not op_mini all"],
    "development": ["last 1 chrome version", "last 1 firefox version", "last 1 safari version"]
  },
  // Add the react-dynamic-environment configuration
  "react-dynamic-environment": {
    "whitelist": ["API_URL"]
  }
}
```

## 2. Run your project

```sh
npm start
```

Now your project have the environment variables loaded **globally** in the `window.env` property.

## 3. Read the environment variables

You can access the environment variables from your code in two ways:

### A. Using the `react-dynamic-environment` library

```jsx
import React from "react";
import env from "react-dynamic-environment";

export function MyComponent() {
  return <div>{env.API_URL}</div>;
}
```

### B. Using the `window.env` global variable

```jsx
import React from "react";

export function MyComponent() {
  return <div>{window.env.API_URL}</div>;
}
```