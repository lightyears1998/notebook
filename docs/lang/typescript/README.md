# TypeScript笔记

## 安装

```sh
yarn global add typescript
```

## 编译

```sh
tsc filename.ts
```

## 配置

tsconfig.json

```json
{
    "compilerOptions": {
        "target": "ESNext",
        "module": "CommonJS",
        "moduleResolution": "Node",
        "esModuleInterop": true,
        "resolveJsonModule": true,
        "outDir": "lib",
        "inlineSourceMap": true,
        "emitDecoratorMetadata": true,
        "experimentalDecorators": true
    },
    "include": [
        "src/**/*"
    ]
}
```
