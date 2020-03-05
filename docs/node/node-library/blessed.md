# Blessed 图形化命令行界面

Blessed的文档在README文件中，阅读体验不佳。可参考[独立文档站点](https://lightyears1998.github.io/blessed-docs/)。

- 原项目chjj/blessed已暂停维护，可考虑使用neo-blessed。
- blessed能处理两字符宽度的中文字体。
- 需要使用非缓冲的IO，与Nodemon不兼容。
- [基本机制](https://github.com/chjj/blessed/blob/master/README.md#mechanics)
  - 支持Tags、支持颜色。
  - 支持Contents。

## 常用搭配

- neo-blessed -> blessed <https://github.com/embarklabs/neo-blessed>
- term.js
- node-pty -> pty.js（仅支持至v8） <https://github.com/Microsoft/node-pty>
