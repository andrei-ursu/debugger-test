# _**Boots - Enable Node.js Visual Studio Code Debugger**_

## Steps

### 1. Create a .vscode folder in the root of the project if it does not exist <br>

### 2. Create a launch.json file in the .vscode folder following this example: <br>
    
```Json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "DEBUG",
            "preLaunchTask": "npm: build",
            "cwd": "${workspaceRoot}",
            "program": "${workspaceRoot}/build/server.js",
            "outFiles": [
                "${workspaceRoot}/build/**.js"
            ],
            "env": {
                "ENV_CONFIG_PATH": "config/env/local/config.yaml",
                "ENV_SECRETS_PATH": "config/env/local/secrets.json"
            },
            "sourceMaps": true
        }
    ]
}
```

* The _**preLaunchTask**_ property is a script that can be run before the debugger starts, in the example above, the build process is triggered for the project.
* The _**program**_ property is the path to the output script of the build process _(e.g.: server.js)_
* The _**outFiles**_ property is the path to all of the .js files from the output of the build process
* The _**env**_ property is where environment variables can be provided, in the example they were taken from the _npm run dev_ script in package.json

### 3. Add a new property in the webpack config file _(e.g.: webpack/server.js)_ <br>

At the end of the module.exports object add the following property:
```JavaScript 
devtool: 'source-map'
```

The source-maps provide a mapping between the original and the transformed source code. This allows us add breakpoints in the original(non-built) code that will get triggered.