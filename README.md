## フォルダ構成

```
C:.
├───.vscode
│       launch.json
│       tasks.json
│       
├───dist
│       
├───src
│       index.ts
│
│   .gitignore
│   package-lock.json
│   package.json
│   README.md
│   tsconfig.json
```

## 手順

1. node の初期化

    ```
    npm init
    ```

1. 必要モジュールインストール
    ```
    npm install --save-dev typescript @types/node
    ```

1. 初期設定
    1. `/package.json`

        `scripts` に `build` タスクを追加

        ```
        {
          "name": "skelton",
          "version": "1.0.0",
          "description": "",
          "main": "index.js",
          "devDependencies": {
            "typescript": "^5.0.4"
          },
          "scripts": {
            "build": "tsc --build tsconfig.json"
          },
          "author": "Akinari Tsugo",
          "license": "MIT"
        }
        ```

    1. `/tsconfig.json`

        ```
        npx tsc --init
        ```

        ```
        {
          "compilerOptions": {
            "target": "es2016",
            "module": "commonjs",
            "sourceMap": true,
            "outDir": "./dist",
            "allowSyntheticDefaultImports": true,
            "esModuleInterop": true,
            "strict": true, 
            "skipLibCheck": true
          },
          "include": [
            "./src/**/*"
          ],
          "exclude": [
            "node_modules",
            "**/*.spec.ts"
          ]
        }
        ```

    1. `/.vscode/launch.json`

        ```
        {
          "version": "0.2.0",
          "configurations": [
            {
              "type": "node",
              "request": "launch",
              "name": "プログラムの起動",
              "program": "${workspaceFolder}/dist/index.js",
              "outFiles": [
                "${workspaceFolder}/dist/**/*.js"
              ],
              "preLaunchTask": "npm: build"
            }
          ]
        }
        ```

    1. `/.vscode/tasks.json`

        ```
        {
          "version": "2.0.0",
          "tasks": [
            {
              "type": "npm",
              "script": "build",
              "problemMatcher": [],
              "group": {
                "kind": "build",
                "test": true
              },
              "label": "npm: build",
              "detail": "tsc --build"
            }
          ]
        }
        ```


