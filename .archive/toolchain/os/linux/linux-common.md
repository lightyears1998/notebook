# Linux常识

[发行版目录](https://en.wikipedia.org/wiki/Linux_distribution)

## 硬件基础

组件和设备都是文件。

- 芯片组 北快南慢
- 硬盘
  - IDE(Master/Slave) `/dev/hda`
  - SATA/USB/SCSI `/dev/sda`
- 当前鼠标 `/dev/mouse`
- 当前CDROM `/dev/cdrom`

### MBR(Master Boot Record)磁盘分区

- 分区最小单位：柱面
- 默认分区表支持4组分区信息：主分区、拓展分区（硬盘限制） `/dev/sda1` ~ `/dev/sda4`
- 拓展分区用于记录额外的分区信息，不能格式化用于记录数据，额外分区称为“逻辑分区”。
- 拓展分区是唯一的（操作系统限制）。
- 逻辑分区自`/dev/sda5`始，无论默认分区表4组分区是否全部存在。
- 主分区Primary, 拓展分区Extended, 逻辑分区Logical

## 目录树

常见挂载点：

- `/`
- `/usr`
- `/home`
- `/var`

常见目录：

- 个人文件夹 `/home/usrname`
- man文档 `/usr/share/doc/`
- info文档 `/usr/share/info/`
