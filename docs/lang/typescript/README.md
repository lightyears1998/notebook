# TypeScript常识

## 安装编译器`tsc`

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
        "declaration": true,
        "emitDecoratorMetadata": true,
        "experimentalDecorators": true
    },
    "include": [
        "src/**/*"
    ]
}
```
