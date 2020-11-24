# Ada Linting Configuration Files

## Command-line Node Project

This is the `.eslintrc.json` file we will use in terminal-based command line applications.

```json
{
  "parser": "babel-eslint",
  "env": {
    "browser": true,
    "es2021": true,
    "node": true,
    "jest/globals": true
  },
  "extends": ["eslint:recommended", "plugin:jest/recommended"],
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["react-app", "react-app/jest"],
  "rules": {
    "no-unused-vars": "warn",
    "no-console": "off",
    "func-names": "off",
    "comma-dangle": ["only-multiline"]
  }
}
```

## React Linting File

```json
{
  "parser": "babel-eslint",
  "env": {
    "browser": true,
    "es2021": true,
    "node": true,
    "jest/globals": true
  },
  "extends": ["standard", "plugin:jest/recommended"],
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["jest"],
  "rules": {
    "no-unused-vars": "warn",
    "no-console": "off",
    "func-names": "off",
    "comma-dangle": ["only-multiline"]
  }
}
```