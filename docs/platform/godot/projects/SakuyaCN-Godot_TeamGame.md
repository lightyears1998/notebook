# SakuyaCN/Godot_TeamGame 放置类游戏秘境森林探险队

- <https://github.com/SakuyaCN/Godot_TeamGame>

SakuyaCN 是 GodoterCN 上面的大佬了，他的项目很有参考意义。

SakuyaCN 在 GodoterCN 上还有一些其他的教程，简单列出如下：

1. 加密游戏数据防止修改，不过目前还没有这方面的需求。
2. Bilibili 直播弹幕姬教程，基于官方的 WebSocket 协议。很有趣的样子。
3. [Godot TapTAp 反沉迷相关功能 SDK](https://godoter.cn/d/93-godot-androidgodotantiaddiction) [GitHub](https://github.com/SakuyaCN/GodotAndroidUtils)。想上架 TapTap 可以研究一下。
4. [战棋网格小教程](https://godoter.cn/d/74-tilemap) RayCast 的使用很典型。
5. [Godot Android Utils](https://godoter.cn/d/46-godot-androidgodotutils) 可以通过这个项目研究 Godot 与 Android 的桥接。
6. [Godot MMKV](https://github.com/SakuyaCN/Godot-MMKV) 可持久化的 Memory Key/value system。

虽说本篇的重点是学习秘境森林探险队，但我决定拿实现战棋网格小教程和MMKV作为练手的小项目。

- 战棋网格小教程 借这个教程稍微练习了新版的 Tween。
- [Godot-MMKV](https://github.com/SakuyaCN/Godot-MMKV/) 这个项目不简单。它使用 Godot Native，背靠腾讯开源的 MMKV 项目，能实现一个高性能的 KV 储存框架（微信同款）。Godot 这一侧是做了库的绑定。MMKV 的核心是 `mmap`，多线程还需要根据操作系统的实现加锁。日后有时间应该仔细学习一下 MMKV 的原理。
