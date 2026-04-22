---
name: kongyo-ts-prettier-setup
description: Set up Prettier code formatter for TypeScript npm projects with merge-safe defaults.
---

## kongyo-ts-prettier-setup

Set up Prettier for an existing or new TypeScript npm project.

Merge rules for existing projects:

- Do not overwrite existing scripts or ignore entries blindly.
- Add missing entries; keep existing behavior unless explicitly requested to replace.

### Target Project Scope

- Single package repo: edit the root `package.json`.
- Monorepo: edit the `package.json` in the workspace/package the user asked for.
- If the target package is not explicit, ask which workspace/package to update before editing.

### Installation

```bash
npm install -D prettier
```

If `prettier` is already in `devDependencies`, do not reinstall by default.
Reinstall or upgrade only when the user asks to pin/change the version.

### Configuration Files

Create `.prettierrc.json` if it does not exist:

```json
{
  "semi": true
}
```

If `.prettierrc.*` already exists, keep it as-is by default.
Only change existing Prettier options when at least one is true:

- The user explicitly requested a style change.
- A team/project style guide requires it.
- The current config is invalid JSON/YAML/TOML and must be fixed.

Create `.prettierignore` if it does not exist:

```
node_modules
dist
coverage
*.min.js
package-lock.json
```

If `.prettierignore` already exists, append only missing lines from the list above.

### Package.json Scripts

If `format` does not exist:

```json
{
  "scripts": {
    "format": "prettier --write .",
    "format:check": "prettier --check .",
    "check:file": "prettier --check"
  }
}
```

If `format` already exists for another formatter, keep it and add `format:prettier` instead:

```json
{
  "scripts": {
    "format": "<keep existing>",
    "format:prettier": "prettier --write .",
    "format:check": "prettier --check .",
    "check:file": "prettier --check"
  }
}
```

### Usage

Run full formatting:

- `npm run format` (or `npm run format:prettier` when `format` is already used)

Run repository check:

- `npm run format:check`

Run a single file check:

- `npm run check:file -- src/index.ts`

### Verification Notes

- If `package.json` already declares `prettier` but `node_modules` is not installed yet, run `npm install` before `format:check` / `check:file`.
- For `check:file`, pass an existing file path in the target package (for example `src/index.ts` or another tracked file).