# 领域驱动设计 DDD

本文内容摘自：

- [阿里技术专家详解 DDD 系列- Domain Primitive](https://developer.aliyun.com/article/716908)
- [阿里技术专家详解DDD系列 第二弹 - 应用架构](https://developer.aliyun.com/article/719251)

## Domain Primitive

Primitive 不从任何其他事物发展而来，初级的形成或生长的早期阶段

贫血模型代码的问题：

1. **接口的清晰度** 贫血模型参数名在编译时丢失，留下的仅仅是一个参数类型的列表
2. **数据验证和错误处理** 贫血模型重复度太高
3. **业务代码的清晰度** 贫血模型胶水代码太多
4. **可测试性** 贫血模型参数越多，测试越难

解决方案

1. **将隐性的概念显性化** Make Implicit Concepts Explicit
2. **将 隐性的 上下文 显性化** Make Implicit Context Explicit
3. **封装 多对象 行为** Encapsulate Multi-Object Behavior

使用 DP 将隐形的业务逻辑独立出来。

1. **接口的清晰度** 对象式的入参
2. **数据验证和错误处理** 把数据验证的工作量前置到了调用方，而调用方本来就是应该提供合法数据
3. **业务代码的清晰度** 在刨除了数据验证代码、胶水代码之后，剩下的都是核心业务逻辑
4. **可测试性** 参数数量变少

## 架构的设计标准

- 独立于框架 架构不应该依赖某个外部的库或框架，不应该被框架的结构所束缚。
- 独立于UI 前台展示的样式可能会随时发生变化（今天可能是网页、明天可能变成console、后天是独立app），但是底层架构不应该随之而变化。
- 独立于底层数据源 无论今天你用MySQL、Oracle还是MongoDB、CouchDB，甚至使用文件系统，软件架构不应该因为不同的底层数据储存方式而产生巨大改变。
- 独立于外部依赖 无论外部依赖如何变更、升级，业务的核心逻辑不应该随之而大幅变化。
- 可测试 无论外部依赖了什么数据库、硬件、UI或者服务，业务的逻辑应该都能够快速被验证正确性。
