# GGET 战斗模拟资源

本仓库提供本地战斗模拟的资源包。轻量版 `setup.cmd` 会自动从发布页下载所需 ZIP，全量版随包提供这些资源。[资源发布页](https://github.com/Torfaen/gget-battle-simulator-resources/releases/tag/2026.11.16) · [战斗模拟主仓库](https://github.com/Torfaen/gget-battle-simulator)

| 资源包 | 内容 |
| --- | --- |
| `battle-ui-assets.zip` | 机体棋子、角色和支援者头像、图标、地图背景及其索引 |
| `battle-runtime-data.zip` | 2.7.0 基础运行库、Android 客体文件、原版主表、已准备的基础和追加关卡数据 |
| `gget-unit-portraits.zip` | 1,534 张机体立绘，用于编队和机体详情 |

也可以把三个 ZIP 手动解压到源码目录之外的同一本地数据目录，并把环境变量 `GGET_BATTLE_DATA_DIR` 指向该目录。

```powershell
$env:GGET_BATTLE_DATA_DIR = 'D:\GGET-battle-local'
Expand-Archive -LiteralPath '.\battle-ui-assets.zip' -DestinationPath $env:GGET_BATTLE_DATA_DIR
Expand-Archive -LiteralPath '.\battle-runtime-data.zip' -DestinationPath $env:GGET_BATTLE_DATA_DIR
Expand-Archive -LiteralPath '.\gget-unit-portraits.zip' -DestinationPath $env:GGET_BATTLE_DATA_DIR
```

从代码仓库根目录启动窗口。首次启动还需要准备 Zig 和本地出击编队。Windows 独立运行依赖 QEMU，MuMu 续战使用模拟器内已安装的国际版 2.8.0。实机检查点、账号编队和游戏安装包由各自的本地环境提供。具体准备步骤见 [原版后端运行指南](https://github.com/Torfaen/gget-battle-simulator/blob/main/original_battle_reuse/README.md)。

```powershell
python -B original_battle_reuse/battle_ui.py
```

压缩包的文件数、体积和 SHA-256 见 [checksums.json](checksums.json)。

## 启动更新

战斗模拟 v0.1.2 起，`setup.cmd` 会检查 [updates.json](updates.json)，按清单里的 SHA-256 只下载本机缺少或发生变化的文件。第一批更新包含棋子索引及核心战机和渣古Ⅰ的棋子图。[棋子更新 Release](https://github.com/Torfaen/gget-battle-simulator-resources/releases/tag/2026.11.16-koma.1)

发布更新时，先推送 `program.commit` 对应的程序提交，再上传 `resources.tag` 下的资源文件。清单的 `program.files` 列出该版本的程序文件及哈希，`resources.files` 列出相对于基础资源包的累计更新。资源条目记录本地相对路径、Release 附件名和哈希。验证所有链接和哈希后，增加 `revision` 并提交清单。
