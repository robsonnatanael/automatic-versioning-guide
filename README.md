# Semantic Release Configuration

## devDependencies

> :warning: git installation is a prerequisite

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

4. `CI` configuration [:link:](https://semantic-release.gitbook.io/semantic-release/usage/ci-configuration)

- [:link:](https://github.com/features/actions) GitHub Actions

- :memo: [config file example](.github/workflows/automatic-releases.yml)

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
