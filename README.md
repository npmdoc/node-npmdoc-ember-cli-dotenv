# api documentation for  [ember-cli-dotenv (v1.2.0)](https://github.com/fivetanley/ember-cli-dotenv#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-ember-cli-dotenv.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-ember-cli-dotenv) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-ember-cli-dotenv.svg)](https://travis-ci.org/npmdoc/node-npmdoc-ember-cli-dotenv)
#### Expose .env variables in Ember applications

[![NPM](https://nodei.co/npm/ember-cli-dotenv.png?downloads=true)](https://www.npmjs.com/package/ember-cli-dotenv)

[![apidoc](https://npmdoc.github.io/node-npmdoc-ember-cli-dotenv/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-ember-cli-dotenv_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-ember-cli-dotenv/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-ember-cli-dotenv/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-ember-cli-dotenv/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Stanley Stuart"
    },
    "bugs": {
        "url": "https://github.com/fivetanley/ember-cli-dotenv/issues"
    },
    "dependencies": {
        "dotenv": "^1.0.0",
        "exists-sync": "0.0.3"
    },
    "description": "Expose .env variables in Ember applications",
    "devDependencies": {
        "broccoli-asset-rev": "^2.1.2",
        "ember-cli": "1.13.8",
        "ember-cli-babel": "^5.1.3",
        "ember-cli-htmlbars": "^1.0.0",
        "ember-cli-htmlbars-inline-precompile": "^0.3.1",
        "ember-cli-inject-live-reload": "^1.3.1",
        "ember-cli-qunit": "^1.0.1",
        "ember-resolver": "^2.0.2",
        "ember-try": "~0.0.8"
    },
    "directories": {
        "doc": "doc",
        "test": "tests"
    },
    "dist": {
        "shasum": "11aab75ee3d98305799778dad58072fca97c57f1",
        "tarball": "https://registry.npmjs.org/ember-cli-dotenv/-/ember-cli-dotenv-1.2.0.tgz"
    },
    "ember-addon": {
        "configPath": "tests/dummy/config"
    },
    "engines": {
        "node": ">= 0.10.0"
    },
    "gitHead": "efd9ff017202148336c51b8264b4a95d3d82f1a1",
    "homepage": "https://github.com/fivetanley/ember-cli-dotenv#readme",
    "keywords": [
        "ember-addon",
        "dotenv"
    ],
    "license": "MIT",
    "maintainers": [
        {
            "name": "fivetanley",
            "email": "stanley@stan.li"
        }
    ],
    "name": "ember-cli-dotenv",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/fivetanley/ember-cli-dotenv.git"
    },
    "scripts": {
        "build": "ember build",
        "start": "ember server",
        "test": "ember try:testall"
    },
    "version": "1.2.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module ember-cli-dotenv](#apidoc.module.ember-cli-dotenv)
1.  [function <span class="apidocSignatureSpan">ember-cli-dotenv.</span>config (environment)](#apidoc.element.ember-cli-dotenv.config)
1.  [function <span class="apidocSignatureSpan">ember-cli-dotenv.</span>included (app)](#apidoc.element.ember-cli-dotenv.included)
1.  string <span class="apidocSignatureSpan">ember-cli-dotenv.</span>name



# <a name="apidoc.module.ember-cli-dotenv"></a>[module ember-cli-dotenv](#apidoc.module.ember-cli-dotenv)

#### <a name="apidoc.element.ember-cli-dotenv.config"></a>[function <span class="apidocSignatureSpan">ember-cli-dotenv.</span>config (environment)](#apidoc.element.ember-cli-dotenv.config)
- description and source-code
```javascript
config = function (environment){
  var path = require('path');
  var fs = require('fs');
  var dotenv = require('dotenv');
  var existsSync = require('exists-sync');
  var project = this.project;
  var loadedConfig;
  var config = {};
  var hasOwn = Object.prototype.hasOwnProperty;

  var configFilePath,
      dotEnvPath = this.app && this.app.options.dotEnv && this.app.options.dotEnv.path;

  if (dotEnvPath) {
    // path is defined
    if (typeof dotEnvPath === 'string') {
      configFilePath = dotEnvPath;
    } else {
      if (dotEnvPath[environment]) {
        configFilePath = dotEnvPath[environment];
      }
    }
  }

  if (!configFilePath) {
    configFilePath = path.join(project.root, '.env');
  }

  if (existsSync(configFilePath) && dotenv.config({path: configFilePath})) {
    loadedConfig = dotenv.parse(fs.readFileSync(configFilePath));
  } else {
    loadedConfig = {};
  }

  var app = this.app;
  if (!this.app) {
    return;
  }
  if (app.options.dotEnv && hasOwn.call(app.options.dotEnv, 'allow')){
    console.warn("[EMBER-CLI-DOTENV] app.options.allow has been deprecated. Please use clientAllowedKeys instead. Support will be
 removed in the next major version");
  }
  var allowedKeys = (app.options.dotEnv && (app.options.dotEnv.clientAllowedKeys || app.options.dotEnv.allow) || []);

  allowedKeys.forEach(function(key){
    config[key] = loadedConfig[key];
  });

  return config;
}
```
- example usage
```shell
...
  }
}

if (!configFilePath) {
  configFilePath = path.join(project.root, '.env');
}

if (existsSync(configFilePath) && dotenv.config({path: configFilePath})) {
  loadedConfig = dotenv.parse(fs.readFileSync(configFilePath));
} else {
  loadedConfig = {};
}

var app = this.app;
if (!this.app) {
...
```

#### <a name="apidoc.element.ember-cli-dotenv.included"></a>[function <span class="apidocSignatureSpan">ember-cli-dotenv.</span>included (app)](#apidoc.element.ember-cli-dotenv.included)
- description and source-code
```javascript
included = function (app){
  this.app = app;
  this._super.included.apply(this, arguments);
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
