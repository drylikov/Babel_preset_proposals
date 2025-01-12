# Babel preset proposals

A Babel 7 preset to manage experimental proposal plugin dependencies and usage, providing default configuration for plugins which have mandatory options, and ensuring that proposal plugins which affect one another are used in the correct order and have appropriate options set.

## Install

```sh
npm install babel-preset-proposals
```

## Options

### `absolutePaths`

`boolean`, defaults to `false`.

Use absolute paths in `plugins` config - use this option if you're creating a Babel configuration which will be used outside of the module resolution scope of where you're generating it.

### `all`

`boolean`, defaults to `false`.

Enable all plugins which haven't been otherwise configured.

### `loose`

`boolean`

Sets the `loose` option for all plugins which are enabled and have a `loose` option - primarily intended for flipping plugin `loose` options to `true`, since they default to `false`.

### Plugin Options

`boolean` or an `Object`, defaults to `false`.

To enable a plugin, pass its option as `true`:

```json
{
  "presets": [
    ["babel-preset-proposals", {
      "classProperties": true,
      "decorators": true,
      "exportDefaultFrom": true,
      "exportNamespaceFrom": true
    }]
  ]
}
```

If the plugin takes options, you can pass an options Object for it.

```json
{
  "presets": [
    ["babel-preset-proposals", {
      "decorators": {"legacy": true}
    }]
  ]
}
```

| Preset option | Babel Plugin Docs |
| ------------- | ----------------- |
| `functionBind` | [`@babel/plugin-proposal-function-bind`](https://babeljs.io/docs/en/babel-plugin-proposal-function-bind) |
| `exportDefaultFrom` | [`@babel/plugin-proposal-export-default-from`](https://babeljs.io/docs/en/babel-plugin-proposal-export-default-from) |
| `logicalAssignmentOperators` | [`@babel/plugin-proposal-logical-assignment-operators`](https://babeljs.io/docs/en/babel-plugin-proposal-logical-assignment-operators)
| `pipelineOperator` | [`@babel/plugin-proposal-pipeline-operator`](https://babeljs.io/docs/en/babel-plugin-proposal-pipeline-operator) |
| `doExpressions` | [`@babel/plugin-proposal-do-expressions`](https://babeljs.io/docs/en/babel-plugin-proposal-do-expressions) |
| `decorators` | [`@babel/plugin-proposal-decorators`](https://babeljs.io/docs/en/babel-plugin-proposal-decorators) |
| `functionSent` | [`@babel/plugin-proposal-function-sent`](https://babeljs.io/docs/en/babel-plugin-proposal-function-sent) |
| `exportNamespaceFrom` | [`@babel/plugin-proposal-export-namespace-from`](https://babeljs.io/docs/en/babel-plugin-proposal-export-namespace-from) |
| `numericSeparator` | [`@babel/plugin-proposal-numeric-separator`](https://babeljs.io/docs/en/babel-plugin-proposal-numeric-separator) |
| `throwExpressions` | [`@babel/plugin-proposal-throw-expressions`](https://babeljs.io/docs/en/babel-plugin-proposal-throw-expressions) |
| `dynamicImport` | [`@babel/plugin-syntax-dynamic-import`](https://babeljs.io/docs/en/babel-plugin-syntax-dynamic-import) |
| `importMeta` | [`@babel/plugin-syntax-import-meta`](https://babeljs.io/docs/en/babel-plugin-syntax-import-meta) |
| `classStaticBlock` | [`@babel/plugin-proposal-class-static-block`](https://babeljs.io/docs/en/babel-plugin-proposal-class-static-block) |
| `classProperties` | [`@babel/plugin-proposal-class-properties`](https://babeljs.io/docs/en/babel-plugin-proposal-class-properties) |

If a plugin _requires_ configuration and you enable it with a `true` option, this preset will provide default options:

| Preset option | Default plugin options |
| ------------- | ---------------------- |
| `decorators` | `{decoratorsBeforeExport: false}` |
| `pipelineOperator` | `{proposal: 'minimal'}` |

## API

### `validateOptions(options?: Object): String[]`

The validation this plugin performs on its options is exported if you need to use it in tooling which accepts user configuration, as you may want to report option validation issues yourself rather than letting Babel blow up.

It returns an Array of error messages, which will be empty if options were valid.

## Versioning

Proposal plugins will never be stable, so this package will always be at a 0.X version and will make breaking changes as necessary, so lock it to the specific 0.X version you're using.
