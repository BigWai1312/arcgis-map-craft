# ArcGIS 精细制图 / ArcGIS Map Craft

作者：**BigWai1312**

面向 Codex 的 ArcGIS Pro 专题制图 Skill，适用于报告、论文和汇报中的市域、区县、乡镇、规划分区及村级图件。涵盖 DEM 与山体阴影、水系与道路、分级配色、紧凑版式、双列图例、经纬度图廓、字体和导出检查。

这是供 Codex 读取的制图规范，不是 ArcGIS 插件或独立制图程序。实际制图需要使用者自己的 ArcGIS Pro、有效许可、本地数据，以及能运行 ArcPy 的环境。600 dpi、字体、阴影等参数可随具体任务调整。

## 安装

### 方法一：让 Codex 安装

在支持 Skills 的 Codex 中发送：

```text
$skill-installer 从 GitHub 仓库 BigWai1312/arcgis-map-craft 安装 Skill。
Skill 位于仓库根目录，安装名称为 arcgis-map-craft。
```

如果已经安装，不要重复安装；更新方法见后文。

### 方法二：使用 ZIP

从本仓库 Releases 下载 `arcgis-map-craft.zip`，解压后将整个 `arcgis-map-craft` 文件夹放到个人 Skills 目录。当前 Codex 官方文档推荐的 Windows 路径为：

```text
%USERPROFILE%\.agents\skills\arcgis-map-craft\SKILL.md
%USERPROFILE%\.agents\skills\arcgis-map-craft\agents\openai.yaml
```

只供单个项目使用时，可以放到该项目的 `.agents/skills/arcgis-map-craft/`。不要多嵌套一层同名目录。如果现有环境已经从 `.codex/skills/` 发现这个 Skill，继续维护现有安装即可，不要再装一份同名 Skill。

安装或修改后，在下一轮对话尝试调用；未出现时重启 Codex。

## 使用

在消息中明确写上 `$arcgis-map-craft`，并给出数据位置、字段、单位、输出位置及 ArcPy 环境。支持 Skill 选择器的界面，也可搜索“ArcGIS 精细制图”。只写 Skill 名不会自动知道你的数据放在哪里。

例如，先制作一张样图：

```text
$arcgis-map-craft
用 ArcGIS Pro 做一张乡镇专题图，先出一张样图供我确认。
数据目录：<本地数据目录>
乡镇面：<图层路径>；连接字段：<乡镇编码>
指标表：<表格路径>；指标字段：<字段名>；单位：<单位>
DEM：<栅格路径>；水系：<图层路径>；道路：<图层路径>
ArcPy Python：<ArcGIS Pro 的 python.exe 路径>
输出目录：<本地输出目录>
水系用蓝色，专题色避开蓝色；中文宋体，英文数字 Times New Roman。
中心城区放大图放左上，指北针放右上，双列图例放右下。
加经纬度图廓，地形适当夸张，边界加悬浮阴影。
输出可编辑 APRX、相关本地数据、预览 PNG 和 600 dpi JPG。
不要改源数据，不要插入 Word。
```

也可以只修改现有工程：

```text
$arcgis-map-craft
检查 <APRX路径>，保留数据和分级阈值，只调整版式。
收窄留白，图名和完整双列图例放进图框内，统一字体和比例尺。
另存为新工程，先导出预览让我看。
```

在离线生产电脑上手工出图时，可以这样要求：

```text
$arcgis-map-craft
根据 <字段表或数据说明> 写一份 ArcGIS Pro 手工制图教程。
逐图写清连接字段、分级阈值、图例文字、RGB、线宽、透明度、
图层顺序和图廓整饰，标出可从上一张图复制的公共图层。
只写 Markdown，不运行制图，不修改数据。
```

离线指图件使用本地数据、不依赖在线底图；本 Skill 不提供离线 AI 模型。运行 Codex 仍需其可用的模型服务。

## 后续更新

作者维护时，以 GitHub 仓库的工作副本为准，修改 `SKILL.md`；界面名称等元数据位于 `agents/openai.yaml`，说明位于 `README.md`。

```powershell
git add SKILL.md README.md agents/openai.yaml
git commit -m "Update cartography guidance"
git push origin main
```

GitHub 发布不会自动覆盖其他电脑上已安装的 Skill。测试新版时，将这三个文件同步到现有安装目录；有本地自定义内容时先保留副本。供他人下载时，重新打包含顶层 `arcgis-map-craft/` 的 ZIP，并在 Releases 发布新版本，例如 `v1.0.1`。后续常规更新使用新提交，不需要改写历史。

## 文件与隐私

- `SKILL.md`：核心制图规范。
- `agents/openai.yaml`：显示名称与默认调用提示。
- `README.md`：安装、使用和更新说明。

保留作者账号署名；不包含实际项目数据、项目名称、私人邮箱、个人绝对路径或凭据。使用示例中的路径均为占位符。

安装目录及 Skill 调用方式参考 [Codex 官方 Skills 文档](https://developers.openai.com/codex/skills/)。
