# ui5-task-transpile-gen
UI5tooling task for transpiling ES6 to ES5 including Async Await

Task for [ui5-builder](https://github.com/SAP/ui5-builder), enabling ES6 support.

## Install

```bash
npm install ui5-task-transpile-gen --save-dev
```

## Usage

1. Define the dependency in `$yourapp/package.json`:

```json
"devDependencies": {
    // ...
    "ui5-task-transpile-gen": "*"
    // ...
},
"ui5": {
  "dependencies": [
    // ...
    "ui5-task-transpile-gen",
    // ...
  ]
}
```

> As the devDependencies are not recognized by the UI5 tooling, they need to be listed in the `ui5 > dependencies` array. In addition, once using the `ui5 > dependencies` array you need to list all UI5 tooling relevant dependencies.

2. configure it in `$yourapp/ui5.yaml`:

```yaml
builder:
  customTasks:
  - name: ui5-task-transpile-gen
    afterMiddleware: replaceVersion
  bundles:
  - bundleDefinition:
      name: namespace/appname/Component-preload.js
      defaultFileTypes:
      - ".js"
      - ".json"
      - ".xml"
      - ".html"
      - ".library"
      sections:
      - mode: raw
        filters:
        - namespace/appname/regenerator-runtime/runtime.js
      - mode: preload
        filters:
        - namespace/appname/manifest.json
        - namespace/appname/controller/**
        - namespace/appname/Component.js
        - namespace/appname/i18n/**
        - namespace/appname/model/**
        - namespace/appname/util/**
        - namespace/appname/view/**
        - namespace/appname/libs/**
        - namespace/appname/test/**
        resolve: false
        sort: true
        declareModules: false
    bundleOptions:
      optimize: true
      usePredefineCalls: true
```
