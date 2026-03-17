---
name: kongyo-ts-prettier-setup
description: Set up Prettier code formatter for TypeScript npm projects.
---

## kongyo-ts-prettier-setup

Prettier is an opinionated code formatter with support for many languages.

### Installation

```bash
npm install -D prettier
```

### Configuration

Create `.prettierrc.json`:

```json
{
  "semi": true
}
```

Create `.prettierignore`:

```
node_modules
dist
coverage
*.min.js
package-lock.json
```

### Package.json Scripts

```json
{
  "scripts": {
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "check:file": "prettier --check"
  }
}
```


