# TeachMeBro

一个用于《最终幻想 XIV》（国服）的 Dalamud 插件，提供**撤退 HUD 警告**功能 —— 监听聊天消息中的触发词，在全屏显示红色径向渐变闪烁蒙层，提醒玩家撤退或注意危险。

## 功能

- **撤退全屏警告** — 聊天中出现指定关键词（默认 `<se.6>`）时，屏幕显示红色径向渐变闪烁蒙层，持续约 3 秒。
- **地图过滤** — 可限定仅在特定地图（Territory ID）下触发，留空则不限制。
- **当前地图信息** — 主窗口显示所在地图 ID、地名、区域、副本名称等信息，方便配置过滤条件。
- **可自定义关键词** — 支持任意聊天关键词触发（如 `<se.6>`、`"集合"`、`"撤退"` 等）。

## 命令

| 命令 | 说明 |
|------|------|
| `/teachmebro` | 打开/关闭主窗口 |

在主窗口中可直接配置触发关键词和地图过滤条件。

## 安装

1. 确保已安装 [Dalamud (CN)](https://github.com/ottercorp/Dalamud)。
2. 将本仓库添加到 Dalamud 自定义插件仓库列表，或手动将编译后的 DLL 放入 `%APPDATA%\XIVLauncher\CN\installedPlugins\TeachMeBro\`。
3. 在游戏中通过 `/xlplugins` 启用。

## 配置

| 配置项 | 说明 |
|--------|------|
| 限定地图 ID | 仅在该地图（TerritoryType）下触发；留空则所有地图均可触发 |
| 触发关键词 | 聊天消息包含该字符串时触发警告（默认 `<se.6>`） |

## 构建

### Windows 本地构建

```bash
git clone <repo-url>
cd TeachMeBro
dotnet restore
dotnet build
```

在安装了 XIVLauncherCN 的 Windows 机器上可直接编译，无需额外配置。

### CI 自动构建

该仓库包含 `.github/workflows/build.yml`，兼容 GitHub Actions、Gitea/Forgejo Actions 等 CI。

Workflow 会自动完成以下操作：
1. 安装 7z 解压工具
2. 通过 `nuget.azure.cn` 镜像获取 NuGet 包（`DalamudPackager` 等）
3. 使用代理 `127.0.0.1:7890` 从 [Dalamud-DailyRoutines/Dalamud](https://github.com/Dalamud-DailyRoutines/Dalamud) 的 GitHub Release 下载完整的 Dalamud CN 运行时程序集（若本地未缓存）
4. 编译项目并上传产物

> 第一次运行后，程序集会缓存到 `~/.xlcore/dalamud/Hooks/dev/`，后续编译直接复用，无需重复下载。

## 许可

[MIT](LICENSE)
