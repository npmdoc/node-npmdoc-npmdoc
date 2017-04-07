# api documentation for  [npmdoc (v2017.3.16)](https://github.com/kaizhu256/node-apidoc-lite)  [![npm package](https://img.shields.io/npm/v/npmdoc-npmdoc.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-npmdoc) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-npmdoc.svg)](https://travis-ci.org/npmdoc/node-npmdoc-npmdoc)
#### this zero-dependency package will auto-generate documentation for your npm-package with zero-config

[![NPM](https://nodei.co/npm/npmdoc.png?downloads=true)](https://www.npmjs.com/package/npmdoc)

[![apidoc](https://npmdoc.github.io/node-npmdoc-npmdoc/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-npmdoc_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-npmdoc/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-npmdoc/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-npmdoc/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "kai zhu",
        "email": "kaizhu256@gmail.com"
    },
    "bin": {
        "apidoc-lite": "lib.apidoc.js"
    },
    "bugs": {
        "url": "https://github.com/kaizhu256/node-apidoc-lite/issues"
    },
    "dependencies": {},
    "description": "this zero-dependency package will auto-generate documentation for your npm-package with zero-config",
    "devDependencies": {
        "electron-lite": "github:kaizhu256/node-electron-lite#alpha",
        "utility2": "github:kaizhu256/node-utility2#alpha"
    },
    "directories": {},
    "dist": {
        "shasum": "53529bf69294a934066ed910749bdecf70d0b703",
        "tarball": "https://registry.npmjs.org/npmdoc/-/npmdoc-2017.3.16.tgz"
    },
    "engines": {
        "node": ">=4.0"
    },
    "homepage": "https://github.com/kaizhu256/node-apidoc-lite",
    "keywords": [
        "api-doc",
        "apidoc",
        "doc",
        "documentation",
        "doxygen",
        "javadoc"
    ],
    "license": "MIT",
    "main": "lib.apidoc.js",
    "maintainers": [
        {
            "name": "kaizhu",
            "email": "kaizhu256@gmail.com"
        }
    ],
    "name": "npmdoc",
    "nameAlias": "apidoc",
    "nameAliasDeprecate": "api_doc apidocs api-doctor doctor-api npm-doc",
    "nameAliasPublish": "npmdoc",
    "nameOriginal": "apidoc-lite",
    "optionalDependencies": {},
    "os": [
        "darwin",
        "linux"
    ],
    "readme": "ERROR: No README data found!",
    "readmeParse": "1",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/kaizhu256/node-apidoc-lite.git"
    },
    "scripts": {
        "build-ci": "utility2 shReadmeTest build_ci.sh",
        "env": "env",
        "heroku-postbuild": "npm install 'kaizhu256/node-utility2#alpha' && utility2 shDeployHeroku",
        "postinstall": "if [ -f lib.apidoc.npm_scripts.sh ]; then ./lib.apidoc.npm_scripts.sh postinstall; fi",
        "start": "export PORT=${PORT:-8080} && export npm_config_mode_auto_restart=1 && utility2 start test.js",
        "test": "export PORT=$(utility2 shServerPortRandom) && utility2 test test.js"
    },
    "version": "2017.3.16"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module npmdoc](#apidoc.module.npmdoc)
1.  [function <span class="apidocSignatureSpan">npmdoc.</span>apidocCreate (options)](#apidoc.element.npmdoc.apidocCreate)
1.  [function <span class="apidocSignatureSpan">npmdoc.</span>apidocModuleDictAdd (options, moduleDict)](#apidoc.element.npmdoc.apidocModuleDictAdd)
1.  [function <span class="apidocSignatureSpan">npmdoc.</span>assert (passed, message)](#apidoc.element.npmdoc.assert)
1.  [function <span class="apidocSignatureSpan">npmdoc.</span>moduleDirname (module)](#apidoc.element.npmdoc.moduleDirname)
1.  [function <span class="apidocSignatureSpan">npmdoc.</span>nop ()](#apidoc.element.npmdoc.nop)
1.  [function <span class="apidocSignatureSpan">npmdoc.</span>objectSetDefault (arg, defaults, depth)](#apidoc.element.npmdoc.objectSetDefault)
1.  [function <span class="apidocSignatureSpan">npmdoc.</span>stringHtmlSafe (text)](#apidoc.element.npmdoc.stringHtmlSafe)
1.  [function <span class="apidocSignatureSpan">npmdoc.</span>templateRender (template, dict)](#apidoc.element.npmdoc.templateRender)
1.  object <span class="apidocSignatureSpan">npmdoc.</span>apidoc
1.  object <span class="apidocSignatureSpan">npmdoc.</span>local
1.  string <span class="apidocSignatureSpan">npmdoc.</span>__dirname
1.  string <span class="apidocSignatureSpan">npmdoc.</span>modeJs
1.  string <span class="apidocSignatureSpan">npmdoc.</span>templateApidocHtml
1.  string <span class="apidocSignatureSpan">npmdoc.</span>templateApidocMd



# <a name="apidoc.module.npmdoc"></a>[module npmdoc](#apidoc.module.npmdoc)

#### <a name="apidoc.element.npmdoc.apidocCreate"></a>[function <span class="apidocSignatureSpan">npmdoc.</span>apidocCreate (options)](#apidoc.element.npmdoc.apidocCreate)
- description and source-code
```javascript
apidocCreate = function (options) {
<span class="apidocCodeCommentSpan">/*
 * this function will create the apidoc from options.dir
 */
</span>    var elementCreate, module, moduleMain, readExample, tmp, trimLeft;
    elementCreate = function (module, prefix, key) {
    /*
     * this function will create the apidoc-element in the given module
     */
        var element;
        element = {};
        element.moduleName = prefix.split('.');
        // handle case where module is a function
        if (element.moduleName.slice(-1)[0] === key) {
            element.moduleName.pop();
        }
        element.moduleName = element.moduleName.join('.');
        element.id = encodeURIComponent('apidoc.element.' + prefix + '.' + key);
        element.typeof = typeof module[key];
        element.name = (element.typeof + ' <span class="apidocSignatureSpan">' +
            element.moduleName + '.</span>' + key)
            // handle case where module is a function
            .replace('>.<', '');
        if (element.typeof !== 'function') {
            return element;
        }
        // init source
        element.source = trimLeft(module[key].toString());
        if (element.source.length > 4096) {
            element.source = element.source.slice(0, 4096).trimRight() + ' ...';
        }
        element.source = (options.template === local.templateApidocHtml
            ? local.stringHtmlSafe(element.source)
            : element.source.replace((/'/g), '_'))
            .replace((/\([\S\s]*?\)/), function (match0) {
                // init signature
                element.signature = match0
                    .replace((/ *?\/\*[\S\s]*?\*\/ */g), '')
                    .replace((/,/g), ', ')
                    .replace((/\s+/g), ' ');
                return element.signature;
            })
            .replace(
                (/( *?\/\*[\S\s]*?\*\/\n)/),
                '<span class="apidocCodeCommentSpan">$1</span>'
            )
            .replace((/^function \(/), key + ' = function (');
        // init example
        options.exampleList.some(function (example) {
            example.replace(
                new RegExp('((?:\n.*?){8}\\.)(' + key + ')(\\((?:.*?\n){8})'),
                function (match0, match1, match2, match3) {
                    element.example = '...' + trimLeft(
                        options.template === local.templateApidocHtml
                            ?  local.stringHtmlSafe(match1) +
                                '<span class="apidocCodeKeywordSpan">' +
                                local.stringHtmlSafe(match2) +
                                '</span>' +
                                local.stringHtmlSafe(match3)
                            : match0.replace((/'/g), "'")
                    ).trimRight() + '\n...';
                }
            );
            return element.example;
        });
        element.example = element.example || 'n/a';
        return element;
    };
    readExample = function (file) {
    /*
     * this function will read the example from the given file
     */
        try {
            return ('\n\n\n\n\n\n\n\n' +
                local.fs.readFileSync(local.path.resolve(options.dir, file), 'utf8') +
                '\n\n\n\n\n\n\n\n').replace((/\r\n*/g), '\n');
        } catch (errorCaught) {
            return '';
        }
    };
    trimLeft = function (text) {
    /*
     * this function will normalize the whitespace around the text
     */
        var whitespace;
        whitespace = '';
        text.trim().replace((/^ */gm), function (match0) {
            if (!whitespace || match0.length < whitespace.length) {
                whitespace = match0;
            }
        });
        text = text.replace(new RegExp('^' + whitespace, 'gm'), '');
        // enforce 128 character column limit
        while ((/^.{128}[^\\\n]/m).test(text)) {
            text = text.replace((/^(.{128})([^\\\n]+)/gm), '$1\\\n$2');
        }
        return text;
    };
    // init options
    options.dir = local.moduleDirname(options.dir);
    local.objectSetDefault(options, {
        packageJson: JSON.parse(readExample('package.json ...
```
- example usage
```shell
...
    local.fs = require('fs');
    local.path = require('path');
    // run the cli
    if (module !== require.main || local.global.utility2_rollup) {
        break;
    }
    // jslint files
    process.stdout.write(local.apidocCreate({
        dir: process.argv[2],
        template: process.argv[3] === '--markdown'
            ? local.templateApidocMd
            : local.templateApidocHtml
    }));
    break;
}
...
```

#### <a name="apidoc.element.npmdoc.apidocModuleDictAdd"></a>[function <span class="apidocSignatureSpan">npmdoc.</span>apidocModuleDictAdd (options, moduleDict)](#apidoc.element.npmdoc.apidocModuleDictAdd)
- description and source-code
```javascript
apidocModuleDictAdd = function (options, moduleDict) {
<span class="apidocCodeCommentSpan">/*
 * this function will add the modules in moduleDict to options.moduleDict
 */
</span>    var isModule, tmp;
    ['child', 'prototype', 'grandchild', 'prototype'].forEach(function (element) {
        Object.keys(moduleDict).sort().forEach(function (prefix) {
            if (!(/^\w[\w\-.]*?$/).test(prefix)) {
                return;
            }
            Object.keys(moduleDict[prefix]).forEach(function (key) {
                if (!(/^\w[\w\-.]*?$/).test(key)) {
                    return;
                }
                // bug-workaround - buggy electron accessors
                try {
                    tmp = element === 'prototype'
                        ? {
                            module: moduleDict[prefix][key].prototype,
                            name: prefix + '.' + key + '.prototype'
                        }
                        : {
                            module: moduleDict[prefix][key],
                            name: prefix + '.' + key
                        };
                    if (!tmp.module ||
                            !(typeof tmp.module === 'function' ||
                            typeof tmp.module === 'object') ||
                            options.moduleDict[tmp.name] ||
                            options.circularList.indexOf(tmp.module) >= 0) {
                        return;
                    }
                    isModule = [
                        tmp.module,
                        tmp.module.prototype
                    ].some(function (dict) {
                        return Object.keys(dict || {}).some(function (key) {
                            try {
                                return typeof dict[key] === 'function';
                            } catch (ignore) {
                            }
                        });
                    });
                    if (!isModule) {
                        return;
                    }
                    options.circularList.push(tmp.module);
                    options.moduleDict[tmp.name] = tmp.module;
                } catch (ignore) {
                }
            });
        });
    });
}
```
- example usage
```shell
...
options.circularList = [];
tmp.forEach(function (element) {
    if (options.circularList.indexOf(element) < 0) {
        options.circularList.push(element);
    }
});
// init moduleDict child
local.apidocModuleDictAdd(options, options.moduleDict);
// init moduleDict lib
(function () {
    // optimization - isolate try-catch block
    try {
        options.libFileList = options.libFileList ||
            local.fs.readdirSync(options.dir + '/lib')
            .sort()
...
```

#### <a name="apidoc.element.npmdoc.assert"></a>[function <span class="apidocSignatureSpan">npmdoc.</span>assert (passed, message)](#apidoc.element.npmdoc.assert)
- description and source-code
```javascript
assert = function (passed, message) {
<span class="apidocCodeCommentSpan">/*
 * this function will throw the error message if passed is falsey
 */
</span>    var error;
    if (passed) {
        return;
    }
    error = message && message.message
        // if message is an error-object, then leave it as is
        ? message
        : new Error(typeof message === 'string'
            // if message is a string, then leave it as is
            ? message
            // else JSON.stringify message
            : JSON.stringify(message));
    throw error;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.npmdoc.moduleDirname"></a>[function <span class="apidocSignatureSpan">npmdoc.</span>moduleDirname (module)](#apidoc.element.npmdoc.moduleDirname)
- description and source-code
```javascript
moduleDirname = function (module) {
<span class="apidocCodeCommentSpan">/*
 * this function will return the __dirname of the module
 */
</span>    var result;
    if (!module || module.indexOf('/') >= 0 || module === '.') {
        return require('path').resolve(process.cwd(), module || '');
    }
    try {
        require(process.cwd() + '/node_modules/' + module);
    } catch (errorCaught) {
        try {
            require(module);
        } catch (ignore) {
        }
    }
    [
        new RegExp('(.*?/' + module + ')\\b'),
        new RegExp('(.*?/' + module + ')/[^/].*?$')
    ].some(function (rgx) {
        return Object.keys(require.cache).some(function (key) {
            result = rgx.exec(key);
            result = result && result[1];
            return result;
        });
    });
    return result || '';
}
```
- example usage
```shell
...
    // enforce 128 character column limit
    while ((/^.{128}[^\\\n]/m).test(text)) {
        text = text.replace((/^(.{128})([^\\\n]+)/gm), '$1\\\n$2');
    }
    return text;
};
// init options
options.dir = local.moduleDirname(options.dir);
local.objectSetDefault(options, {
    packageJson: JSON.parse(readExample('package.json'))
});
local.objectSetDefault(options, { env: {
    npm_package_homepage: options.packageJson.homepage,
    npm_package_name: options.packageJson.name,
    npm_package_version: options.packageJson.version
...
```

#### <a name="apidoc.element.npmdoc.nop"></a>[function <span class="apidocSignatureSpan">npmdoc.</span>nop ()](#apidoc.element.npmdoc.nop)
- description and source-code
```javascript
nop = function () {
<span class="apidocCodeCommentSpan">/*
 * this function will do nothing
 */
</span>    return;
}
```
- example usage
```shell
...
switch (local.modeJs) {



// run browser js-env code - post-init
case 'browser':
    // run tests
    local.nop(local.modeTest &&
        document.querySelector('#testRunButton1') &&
        document.querySelector('#testRunButton1').click());
    break;



// run node js-env code - post-init
...
```

#### <a name="apidoc.element.npmdoc.objectSetDefault"></a>[function <span class="apidocSignatureSpan">npmdoc.</span>objectSetDefault (arg, defaults, depth)](#apidoc.element.npmdoc.objectSetDefault)
- description and source-code
```javascript
objectSetDefault = function (arg, defaults, depth) {
<span class="apidocCodeCommentSpan">/*
 * this function will recursively set defaults for undefined-items in the arg
 */
</span>    arg = arg || {};
    defaults = defaults || {};
    Object.keys(defaults).forEach(function (key) {
        var arg2, defaults2;
        arg2 = arg[key];
        // handle misbehaving getter
        try {
            defaults2 = defaults[key];
        } catch (ignore) {
        }
        if (defaults2 === undefined) {
            return;
        }
        // init arg[key] to default value defaults[key]
        if (!arg2) {
            arg[key] = defaults2;
            return;
        }
        // if arg2 and defaults2 are both non-null and non-array objects,
        // then recurse with arg2 and defaults2
        if (depth > 1 &&
                // arg2 is a non-null and non-array object
                arg2 &&
                typeof arg2 === 'object' &&
                !Array.isArray(arg2) &&
                // defaults2 is a non-null and non-array object
                defaults2 &&
                typeof defaults2 === 'object' &&
                !Array.isArray(defaults2)) {
            // recurse
            local.objectSetDefault(arg2, defaults2, depth - 1);
        }
    });
    return arg;
}
```
- example usage
```shell
...
                typeof arg2 === 'object' &&
                !Array.isArray(arg2) &&
                // defaults2 is a non-null and non-array object
                defaults2 &&
                typeof defaults2 === 'object' &&
                !Array.isArray(defaults2)) {
            // recurse
            local.objectSetDefault(arg2, defaults2, depth - 1);
        }
    });
    return arg;
};

local.stringHtmlSafe = function (text) {
/*
...
```

#### <a name="apidoc.element.npmdoc.stringHtmlSafe"></a>[function <span class="apidocSignatureSpan">npmdoc.</span>stringHtmlSafe (text)](#apidoc.element.npmdoc.stringHtmlSafe)
- description and source-code
```javascript
stringHtmlSafe = function (text) {
<span class="apidocCodeCommentSpan">/*
 * this function will make the text html-safe
 */
</span>    // new RegExp('[' + '"&\'<>'.split('').sort().join('') + ']', 'g')
    return text.replace((/["&'<>]/g), function (match0) {
        return '&#x' + match0.charCodeAt(0).toString(16) + ';';
    });
}
```
- example usage
```shell
...
case 'decodeURIComponent':
    value = decodeURIComponent(value);
    break;
case 'encodeURIComponent':
    value = encodeURIComponent(value);
    break;
case 'htmlSafe':
    value = local.stringHtmlSafe(String(value));
    break;
case 'jsonStringify':
    value = JSON.stringify(value);
    break;
default:
    value = value[arg]();
    break;
...
```

#### <a name="apidoc.element.npmdoc.templateRender"></a>[function <span class="apidocSignatureSpan">npmdoc.</span>templateRender (template, dict)](#apidoc.element.npmdoc.templateRender)
- description and source-code
```javascript
templateRender = function (template, dict) {
<span class="apidocCodeCommentSpan">/*
 * this function will render the template with the given dict
 */
</span>    var argList, getValue, match, renderPartial, rgx, value;
    dict = dict || {};
    getValue = function (key) {
        argList = key.split(' ');
        value = dict;
        // iteratively lookup nested values in the dict
        argList[0].split('.').forEach(function (key) {
            value = value && value[key];
        });
        return value;
    };
    renderPartial = function (match0, helper, key, partial) {
        switch (helper) {
        case 'each':
            value = getValue(key);
            return Array.isArray(value)
                ? value.map(function (dict) {
                    // recurse with partial
                    return local.templateRender(partial, dict);
                }).join('')
                : '';
        case 'if':
            partial = partial.split('{{#unless ' + key + '}}');
            partial = getValue(key)
                ? partial[0]
                // handle 'unless' case
                : partial.slice(1).join('{{#unless ' + key + '}}');
            // recurse with partial
            return local.templateRender(partial, dict);
        case 'unless':
            return getValue(key)
                ? ''
                // recurse with partial
                : local.templateRender(partial, dict);
        default:
            // recurse with partial
            return match0[0] + local.templateRender(match0.slice(1), dict);
        }
    };
    // render partials
    rgx = (/\{\{#(\w+) ([^}]+?)\}\}/g);
    template = template || '';
    for (match = rgx.exec(template); match; match = rgx.exec(template)) {
        rgx.lastIndex += 1 - match[0].length;
        template = template.replace(
            new RegExp('\\{\\{#(' + match[1] + ') (' + match[2] +
                ')\\}\\}([\\S\\s]*?)\\{\\{/' + match[1] + ' ' + match[2] +
                '\\}\\}'),
            renderPartial
        );
    }
    // search for keys in the template
    return template.replace((/\{\{[^}]+?\}\}/g), function (match0) {
        getValue(match0.slice(2, -2));
        if (value === undefined) {
            return match0;
        }
        argList.slice(1).forEach(function (arg) {
            switch (arg) {
            case 'decodeURIComponent':
                value = decodeURIComponent(value);
                break;
            case 'encodeURIComponent':
                value = encodeURIComponent(value);
                break;
            case 'htmlSafe':
                value = local.stringHtmlSafe(String(value));
                break;
            case 'jsonStringify':
                value = JSON.stringify(value);
                break;
            default:
                value = value[arg]();
                break;
            }
        });
        return String(value);
    });
}
```
- example usage
```shell
...
            renderPartial = function (match0, helper, key, partial) {
switch (helper) {
case 'each':
    value = getValue(key);
    return Array.isArray(value)
        ? value.map(function (dict) {
            // recurse with partial
            return local.templateRender(partial, dict);
        }).join('')
        : '';
case 'if':
    partial = partial.split('{{#unless ' + key + '}}');
    partial = getValue(key)
        ? partial[0]
        // handle 'unless' case
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
