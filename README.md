# Ignore Scripts

This repository demonstrates the behavior of `npm install --ignore-scripts` as it applies to dependencies.

## The problem

I want to run my project's `npm install` ignoring anything I have written in the `preinstall` and `postinstall` scripts of `package.json`.
I cannot do this without also ignoring `scripts` defined in the `package.json` of my dependencies.

### node-sass
[node-sass](https://github.com/sass/node-sass/blob/master/package.json) has a `postinstall` script that builds/installs the package binary depending on the runtime environment.
If the `--ignore-scripts` option is used with `npm install`, `scripts` defined in **all** dependncies are ignored, preventing `node-sass` from being fully installed.

## Demonstration

### Successful installation

```bash
rm -rf node_modules
npm install
npm run node-sass
```
You should see `preinstall` and `postinstall` scripts execute

Sass file should be compiled to css

### Unsuccessful installation

```bash
rm -rf node_modules
npm install --ignore-scripts
npm run node-sass
```
You should *not* see `preinstall` or `postinstall` scripts execute.

`npm run node-sass` throws an error because the binary is not present