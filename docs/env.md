# 环境配置

## 编译

1. 安装编译器

    ```sh
    npm i typescript -g
    ```

2. 初始化，生成 `tsconfig.json`

    ```sh
    tsc --init
    ```

    很多人都会报错，tsc不是可执行的命令，一般都是系统环境变量未自动更新，解决方案自行百度。

3. 编译

    通过 `tsc filename` 编译指定文件，不指定文件名，会从 `tsconfig.json` 中读取 `outDir` 和 `rootDir`

## 执行

`ts-node`，直接执行，无需编译

## 监听

安装 `nodemon`，并在 `package.json` 中添加

```json
"dev": "nodemon --watch src/ -e ts --exec ts-node ./src/app.ts"
```

* `--watch src/` 表示监听 `src` 文件夹下的文件变更
* `-e ts` 表示监听文件类型后缀为 `ts`
* `--exec ts-node ./src/app.ts` 表示执行命令，运行代码

## 浏览器运行

`Parcel` 支持浏览器运行 `TS` 文件。

1. 安装 `npm install parcel-bundler -D`
2. 添加启动项，修改 `package.json`

    ```json
      "scripts": {
        "start": "parcel ./index.html"
      }
    ```

## 1. parcel
