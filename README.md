<h1 align="center">Automatic Versioning Guide<h1>

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

- [Git](https://git-scm.com/)
- [Node.js](https://nodejs.org/en/)
- [Yarn](https://yarnpkg.com/)

# Configuration

### **[HuskyJS](https://typicode.github.io/husky/#/)**

1. Install `husky`

```shell
yarn add husky --dev
```

2. Enable Git hooks

```shell
yarn husky install
```

3. To automatically have Git hooks enabled after install, edit `package.json`

```js
// package.json

{
  "private": true, // <- your package is private, you only need postinstall
  "scripts": {
    "postinstall": "husky install"
  }
}
```

### **[Commitlint](https://commitlint.js.org/#/)**

1. Install `commitlint` [:link:](https://commitlint.js.org/#/guides-local-setup)

```shell
yarn add @commitlint/cli @commitlint/config-conventional --dev
```

2. Configure

```js
// commitlint.config.js

module.exports = {
  extends: ["@commitlint/config-conventional"],
};
```

3. Add hook

```shell
yarn husky add .husky/commit-msg 'yarn commitlint --edit $1'
```

4. Test simple usage
   For a first simple usage test of commitlint you can do the following:

```shell
npx commitlint --from HEAD~1 --to HEAD --verbose
```

### **[Semantic Release](https://semantic-release.gitbook.io/semantic-release/usage/installation)**

1. Install `semantic-release`

```shell
yarn add semantic-release --dev
```

2. Install `plugins` [:link:](https://semantic-release.gitbook.io/semantic-release/usage/plugins)

- Default plugins

  These four plugins are already part of semantic-release and are listed in order of execution. They do not have to be installed separately:

```shell
"@semantic-release/commit-analyzer"
"@semantic-release/release-notes-generator"
"@semantic-release/npm"
"@semantic-release/github"
```

- Additional plugins

```shell
yarn add @semantic-release/git @semantic-release/changelog --dev
```

3. semantic-release `configuration` [:link:](https://semantic-release.gitbook.io/semantic-release/usage/configuration)

- A .releaserc file, written in YAML or JSON, with optional extensions: `.yaml` / `.yml` / `.json` / `.js`

- :memo: [config file example](.releaserc.json)
- edite `package.json` and add `release script`

```js
// package.json

{
  // ...
  "scripts": {
    "release": "semantic-release"
  }
  // ...
}
```

4. `CI` configuration [:link:](https://semantic-release.gitbook.io/semantic-release/usage/ci-configuration)

   - [:link:](https://github.com/features/actions) GitHub Actions

   - :memo: [config file example](.github/workflows/automatic-releases.yml)

<div align="right">

[![semantic-release: angular](https://img.shields.io/badge/semantic--release-angular-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)

</div>

# Author

[<img src="https://avatars.githubusercontent.com/u/49655780?s=460&u=2370fd9f777a0de1fdbfcf79a3789a9b3327b1c3&v=4" width=100><br><sub>Robson Natanael :rocket:</sub>](https://www.robsonnatanael.com.br)

[![Linkedin Badge](https://img.shields.io/badge/-Robson-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/robsonnatanael)](https://www.linkedin.com/in/robsonnatanael)
[![Twitter Badge](https://img.shields.io/badge/-@robsonnatanael-1ca0f1?style=flat-square&labelColor=1ca0f1&logo=twitter&logoColor=white&link=https://twitter.com/robsonnatanael)](https://twitter.com/robsonnatanael)
