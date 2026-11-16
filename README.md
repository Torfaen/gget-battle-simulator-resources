# GGET 战斗模拟资源

本仓库提供本地战斗模拟的两份资源包。下载入口在 [资源发布页](https://github.com/Torfaen/gget-battle-simulator-resources/releases/tag/2026.11.16)。程序和开发文档在 [gget-battle-simulator](https://github.com/Torfaen/gget-battle-simulator)。

| 资源包 | 内容 |
| --- | --- |
| `battle-ui-assets.zip` | 机体棋子、角色和支援者头像、图标、地图背景及其索引 |
| `battle-runtime-data.zip` | 2.7.0 基础运行库、Android 客体文件、原版主表、已准备的基础和追加关卡数据 |

两个包都使用 `original_battle_reuse/artifacts/` 相对路径。将 ZIP 解压到源码目录之外的本地数据目录，再把环境变量 `GGET_BATTLE_DATA_DIR` 指向该目录。

```powershell
$env:GGET_BATTLE_DATA_DIR = 'D:\GGET-battle-local'
Expand-Archive -LiteralPath '.\battle-ui-assets.zip' -DestinationPath $env:GGET_BATTLE_DATA_DIR
Expand-Archive -LiteralPath '.\battle-runtime-data.zip' -DestinationPath $env:GGET_BATTLE_DATA_DIR
```

从代码仓库根目录启动窗口。首次启动还需要准备 Zig 和本地出击编队。Windows 独立运行依赖 QEMU，MuMu 续战使用模拟器内已安装的国际版 2.8.0。实机检查点、账号编队和游戏安装包由各自的本地环境提供。具体准备步骤见 [原版后端运行指南](https://github.com/Torfaen/gget-battle-simulator/blob/main/original_battle_reuse/README.md)。

```powershell
python -B original_battle_reuse/battle_ui.py
```

压缩包的文件数、体积和 SHA-256 见 [checksums.json](checksums.json)。
