# Husky

**Before you start: your husky hooks might not work caused by various problems. You can uninstall it completely and remove the `.husky` directory, and try a brand new installation. It's the fastest way to resolve unclear problems.**

## Install husky

```bash
npm install --save-dev husky
```

## Setting up pre-commit hook

```sh
npx husky init
```

this will create a `pre-commit` hook in the `.husky` folder.
the content is like below:

```sh
npm test
```

you can replace it with your own scripts as needed. For example:

```sh
npm run lint
npm run build
npm test
```

Unless all tasks are completed without errors, no commit will be created.

## Setting up commitlint

- install packages

```bash
npm install --save-dev @commitlint/config-conventional @commitlint/cli
```

- create commit-msg git hook

```bash
echo 'npx --no -- commitlint --edit "$1"' > .husky/commit-msg
```

`$1` means the first argument passed into this command, in this case is the commit message we provided.

> npx doc: If any requested packages are not present in the local project dependencies, then they are installed to a folder in the npm cache, which is added to the PATH environment variable in the executed process. A prompt is printed (which can be suppressed by providing either --yes or --no)

- create a config file

```bash
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

## Additional hooks

You can add as many hooks as you wish to ensure the quality of your codebase, which are executed during the appropriate lifecycle.
