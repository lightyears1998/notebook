# 典型线段树特性对比

| 树种 | 单点修改 | 单点查询 | 区间修改 | 区间和查询 | 区间最值查询 |
| --- | --- | --- | --- | --- | --- |
| 线段树（点修改） | O(Log(N)) | O(1) | 不支持 | O(Log(N)) | O(Log(N)) |
| **线段树（区间修改）** | O(Log(N)) | O(Log(N)) | O(Log(N)) | O(Log(N)) | O(Log(N)) |
| 张昆玮线段树 | O(1) | O(1) | 未实现 | O(Log(N))，常数小 | 未实现 |
| 张昆玮线段树（差分） | O(Log(N)) | 借助区间最值查询，O(Log(N)) | 未实现 | 未实现 | O(Log(N)) |