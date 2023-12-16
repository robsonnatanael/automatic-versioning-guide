<h1 align="center">Automatic Versioning Guide</h1>

<p align="center">  
    <img alt="Version" src="https://img.shields.io/github/v/tag/robsonnatanael/automatic-versioning-guide">
    <img alt="Stars" src="https://img.shields.io/github/stars/robsonnatanael/automatic-versioning-guide">    
    <img alt="Issues" src="https://img.shields.io/github/issues/robsonnatanael/automatic-versioning-guide?logoColor=1DA1F2">  
  </p>
  <p align="center">
    <a href="#about">About</a> &#xa0; | &#xa0;
    <a href="#requirements">Requirements</a> &#xa0; | &#xa0;
    <a href="#configuration">Configuration</a> &#xa0; | &#xa0;
    <a href="https://github.com/robsonnatanael" target="_blank">Author</a>
  </p>

# About

This is a quick guide on how to implement automatic semantic versioning using husky.js, commitlint, semantic release and github actions.

# Requirements

- [git](https://git-scm.com/)
- [node.js](https://nodejs.org/en/)
- [yarn](https://yarnpkg.com/) or [npm*](https://www.npmjs.com/)

> **_NOTE:_**  If you choose to use npm, replace `yarn` with `npm run` in the command to install dependencies and when executing the release script in the [workflow](.github/workflows/releases.yml).

# Configuration

### **[HuskyJS](https://typicode.github.io/husky/#/)**

#### 1. Install `husky`

```bash
yarn add husky --dev
```

#### 2. Enable Git hooks

```bash
yarn husky install
```

#### 3. To automatically have Git hooks enabled after install, edit `package.json`

```js
// package.json

{
  "private": true, // <- your package is private, you only need postinstall
  ...
  "scripts": {
    ...
    "postinstall": "husky install"
  }
  ...
}
```

### **[Commitlint](https://commitlint.js.org/#/)**

#### 1. Install `commitlint` [:link:](https://commitlint.js.org/#/guides-local-setup)

```bash
yarn add @commitlint/cli @commitlint/config-conventional --dev
```

#### 2. Configure

```js
// commitlint.config.js

module.exports = {
  extends: ["@commitlint/config-conventional"],
};
```

#### 3. Add hook

```bash
yarn husky add .husky/commit-msg 'yarn commitlint --edit $1'
```

### **[Semantic Release](https://semantic-release.gitbook.io/semantic-release/usage/installation)**

#### 1. Install `semantic-release`

```bash
yarn add semantic-release --dev
```

#### 2. Install `plugins` [:link:](https://semantic-release.gitbook.io/semantic-release/usage/plugins)

- Default plugins

  These four plugins are already part of semantic-release and are listed in order of execution. They do not have to be installed separately:

  - [@semantic-release/commit-analyzer](https://github.com/semantic-release/commit-analyzer)
  - [@semantic-release/release-notes-generator](https://github.com/semantic-release/release-notes-generator)
  - [@semantic-release/npm](https://github.com/semantic-release/npm)
  - [@semantic-release/github](https://github.com/semantic-release/github)

- Additional plugins

```bash
yarn add @semantic-release/git @semantic-release/changelog --dev
```

#### 3. semantic-release `configuration` [:link:](https://semantic-release.gitbook.io/semantic-release/usage/configuration)

- Create a [.releaserc](.releaserc.json) file, written in YAML, with optional extensions:  `.yaml` / `.yml` / `.json` / `.js`
- :memo: [config file example](.releaserc.json)
- edite `package.json` and add `release script`

```js
// package.json

{
  ...
  "scripts": {
    ...
    "release": "semantic-release"
  }
  ...
}
```

#### 4. Set up Continuous Integration [:link:](https://semantic-release.gitbook.io/semantic-release/usage/ci-configuration)

Create a workflow with Continuous Integration processes to be executed whenever a new change is sent to the `main` branch, see an [example here](.github/workflows/releases.yml).

### Optional

Run linters against staged git files and don't let errors slip into your code base

#### 1. Install [lint-staged](https://github.com/lint-staged/lint-staged)

```bash
yarn add lint-staged --dev
```

#### 2. Set up the `pre-commit` git hook to run lint-staged

```bash
yarn husky add .husky/pre-commit 'npx lint-staged'
```

#### 3. Install some linters, like [ESLint](https://eslint.org/) and [Prettier](https://prettier.io/)

#### 4. Configure lint-staged to run linters and other tasks:
- see an [example file](.lintstagedrc)
