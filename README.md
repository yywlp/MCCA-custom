# MCCA-custom

> **本仓库不是原项目，也不是官方分支。**
>
> 本项目**衍生自 [MaaXYZ/MCCA](https://github.com/MaaXYZ/MCCA)**（原作者 MaaXYZ），
> 基于其发布包 `MCCA-win-x86_64-v1.7.5`。原项目的著作权与所有荣誉归原作者及上游贡献者所有；
> 本仓库沿用上游的 [MIT License](LICENSE)，并完整保留原始版权与许可声明。
>
> 上游 `main` 分支自 2025-11-26 起未再更新。本仓库只是**由我个人继续维护、修复兼容性问题的衍生版本**：
> 仅针对游戏界面改版、运行库升级和本地环境做修补，不新增官方功能、不代表上游立场，
> 与 MaaXYZ 及 MCCA 官方无关联。相关问题请在本仓库提 issue，不要提到上游。
>
> 如原作者对本项目有任何意见（包括希望调整或下架），欢迎联系，我会配合处理。

> **本仓库是定制可运行版，不是上游源码仓库。** 基于 MCCA v1.7.5 资源包，
> GUI 已升级到 MFAAvalonia 2.16.4 / MaaFramework 5.14.3，pipeline 已迁移到 `[JumpBack]` 语法。

## 克隆后首次运行（必读）

仓库里是完整程序文件，无需编译，但**不是双击就能跑**，需要按顺序过一遍：

1. **检查环境**：先双击 `DependencySetup_依赖库安装_win.bat`。它会检测并安装
   VC++ 运行库和 **.NET 10 Desktop Runtime**（`MFAAvalonia.runtimeconfig.json` 要求 `net10.0`）。
   缺了 .NET 10 会直接闪退或报缺少运行时；已安装则跳过。
2. **启动模拟器**：打开 MuMu 12，确认 ADB 端口（默认 `127.0.0.1:16384`）。
3. **自动选择**：运行 `MFAAvalonia.exe`，在连接/设置里用「自动选择 / 自动检测」
   让 GUI 识别设备（ADB）与资源（官服）。首次会自动重建实例配置里的设备项。
4. **换机器时改路径**：`config/config.json` 与 `config/instances/default.json` 里的
   `AdbPath`、`Config.extras.mumu.path` 仍指向原来的 MuMu 安装目录，
   需要改成实际路径，或直接在 GUI 里重新自动选择。
5. **改了 pipeline 或选项要重启 GUI**：`resource/base/pipeline/*.json` 和 `interface.json`
   都会被缓存在内存里，不重启不会重新加载（新增的周本选项也要重启才会出现）。

## 本仓库相对上游的改动（个人维护部分）

- GUI 1.8.7 → 2.16.4；MaaFramework 5.0.0-beta.4 → 5.14.3
- 19 个 pipeline / 289 节点：`is_sub`、`interrupt` 迁移为 `[JumpBack]`
- 每日探索：掉落加成弹窗识别词 `开启` → `使用 / 确认 / 开启`（游戏按钮实际文案是「使用」）
- 每日免费礼包：商店改版后「礼包」从顶部标签移到左侧竖排菜单，
  `DailyGift.roi` → `[20,40,240,640]`，并放宽「免费」按钮搜索范围
- 限时贸易所：同步修正 `time_limited.roi`
- 每日签到：`签到.expected` → `^签到$`，避免把「已签到」当成可点按钮反复空点
- 周本：新增 GUI 选项「**周本是否已打完**」。周本全部关卡通关后，每周重置只需点一下
  「碎星虚影」入口卡片就能拿到本周报酬（卡片顶部 `600/600`），无需再进战斗。
  选「**是，已打完只领奖**」时，点完卡片自动关闭「获得物品」弹窗并返回首页，
  跳过后面找关卡、选关、战斗的全部节点；选「否，正常打（默认）」保持原有流程。
  同时把 `ActivityExploration_Exist` 的识别框移到新版卡片区域（旧框还指着左下角）。
- 配置迁移为新版多实例结构（`config/instances/default.json`），保留原有任务队列

运行日志、`debug/`、`temp/`、旧版程序备份与升级过程文件不入库（见 `.gitignore`）。

---

> **以下为上游 MCCA 的原始 README 内容，原样保留**（版权归 MaaXYZ）。
> 其中的下载地址、编译方式、交流群等信息均指向上游项目，请以
> [上游仓库](https://github.com/MaaXYZ/MCCA) 为准；本仓库的使用说明请以上面的「克隆后首次运行」为准。

基于全新架构的 交错战线 CrossCore 小助手。图像技术 + 模拟控制，解放双手！  
由 [MaaFramework](https://github.com/MaaXYZ/MaaFramework) 强力驱动！

## 功能介绍

目前已有的功能：

1. 启动游戏
2. 每日免费礼包
3. 每日探索(只使用自然回复的燃料)
4. 模拟军演(只打第一个，次数耗尽为止)
5. 基建(换班+好友换抽)
6. 周本(支持第一关(45微晶)、第五关(120微晶)。需提前配好一队)
7. 领取奖励(邮箱+每日+通行证)
8. 关闭游戏

## 使用说明

下载地址：<https://github.com/MaaXYZ/MCCA/releases>
1. MuMu模拟器需要关闭模拟器设置中的“后台挂机时保活运行”
2. 运行过程MaaPiCli窗口出现红字是正常的
3. 模拟器不能有中文路径
4. 模拟器窗口大小要16:9，最好建议是使用720p分辨率
5. 运行卡住请将debug文件夹中的maa.log发出来，并附带出错时的游戏截图

### Windows

- 对于绝大部分用户，请下载 `MCCA-win-x86_64-vXXX.zip`
- 若确定自己的电脑是 arm 架构，请下载 `MCCA-win-aarch64-vXXX.zip`
- 解压后运行 `MaaPiCli.exe` 即可


### macOS

- 若使用 Intel 处理器，请下载 `MCCA-macos-x86_64-vXXX.zip`
- 若使用 M1, M2 等 arm 处理器，请下载 `MCCA-macos-aarch64-vXXX.zip`
- 使用方式：

  ```bash
  chmod a+x MaaPiCli
  ./MaaPiCli
  ```

### Linux

~~用 Linux 的大佬应该不需要我教~~

## 图形化界面

- 如果需要使用图形化界面，请下载 `MCCA-win-x86_64-with-gui-vXXX.zip`，目前只支持Windows
- 图形化界面需要.NET8运行库，请自行安装
- 解压后运行`MFAWPF.exe`即可
- 本GUI由社区大佬[SweetSmellFox](https://github.com/SweetSmellFox)编写，相关项目见[MFAWPF](https://github.com/SweetSmellFox/MFAWPF)

## 其他说明

- 添加 `-d` 参数可跳过交互直接运行任务，如 `./MaaPiCli.exe -d`
- 反馈问题请附上日志文件 `debug/maa.log`，谢谢！


## How to build

**如果你要编译源码才看这节，否则直接 [下载](https://github.com/MaaXYZ/MCCA/releases) 即可**

0. 完整克隆本项目及子项目

    ```bash
    git clone --recursive https://github.com/MaaXYZ/MCCA.git
    ```

1. 下载 MaaFramework 的 [Release 包](https://github.com/MaaXYZ/MaaFramework/releases)，解压到 `deps` 文件夹中
2. 安装

    ```python
    python ./install.py
    ```

生成的二进制及相关资源文件在 `install` 目录下

## 开发相关

- [MaaFramework 快速开始](https://github.com/MaaXYZ/MaaFramework/blob/main/docs/zh_cn/1.1-%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B.md)

## Join us

- MCCA 交流群：950540737
- MaaFramework 开发交流 QQ 群: 595990173

## 鸣谢

本项目由 **[MaaFramework](https://github.com/MaaXYZ/MaaFramework)** 强力驱动！

