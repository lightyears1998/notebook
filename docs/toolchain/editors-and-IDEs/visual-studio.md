# Visual Studio

## C++

基本概念：

- 包含目录(`*.h`)、库目录(`*.lib`)和链接器的额外依赖项目(`library.lib`)。
- 每个版本的VS都有自己的平台工具集，平台工具集包含`MSVCRversion.dll`的调试版本`MSVC...d.dll`。可再发行组件包含平台工具集中的`MSVCRversion.dll`。如果使用了平台工具集相关的DLL，需要确定重新分发的DLL。

快捷操作：

- 可以在Property Manager新增属性表（Property Sheet），在新的属性表中定义用户宏（User Marco）。
