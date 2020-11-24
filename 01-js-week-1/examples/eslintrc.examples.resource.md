# Ada Linting Configuration Files

## Command-line Node Project

This is the `.eslintrc.json` file we will use in terminal-based command line applications.

```json
{
  "env": {
    "browser": true,
    "es2021": true,
    "node": true
  },
  "extends": ["plugin:jest/recommended", "eslint:recommended"],
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["jest"],
  "rules": {
    "no-unused-vars": "warn",
    "no-var": "warn",
    "no-console": "off",
    "func-names": "off",
    "comma-dangle": ["warn", "only-multiline"],
    "quotes": [
      "error",
      "single",
      { "allowTemplateLiterals": true, "avoidEscape": true }
    ],
    "camelcase": "error"
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
  "extends": ["react-app", "plugin:jest/recommended", "plugin:jsx-a11y/recommended"],
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["jest", "jsx-a11y"],
  "rules": {
    "no-unused-vars": "warn",
    "no-var": "warn",
    "no-console": "off",
    "func-names": "off",
    "comma-dangle": ["warn", "only-multiline"],
    "quotes": [
      "error",
      "single",
      { "allowTemplateLiterals": true, "avoidEscape": true }
    ],
    "camelcase": "error"
  }
}
```