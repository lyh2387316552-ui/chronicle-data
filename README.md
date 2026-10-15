# 古荒大陆编年史 - 数据与资源仓库

游戏数据与资源仓库,供 [chronicle 网站仓库](https://github.com/lyh2387316552-ui/chronicle) 使用。

## 目录结构

```
chronicle-data/
├── data-sources/   # 数据源 (JSON 技能数据按文件夹; 表格文件直接平铺在根)
│   ├── Skill/ SkillModule/ Stunt/ StuntModule/   # 游戏导出的技能 JSON
│   ├── 属性表.xlsx   # 词缀 + 属性
│   ├── 装备表.xlsx   # 装备
│   ├── 技能养成相关.xlsx  # 辅助宝石 + 技能库
│   ├── 战斗技能相关表.xlsx # 技能标签字典
│   ├── 魔宠表.xlsx   # 魔宠
│   └── 道具表.xlsx   # 道具 (仅 Item 子表；已按编年史展示规则过滤后再导出)
├── icon/           # 游戏图标资源 (技能/装备/宝石/魔宠/职业天赋/道具，统一 WebP)
│   ├── item/       # 道具图标 (仅保留被道具表引用到的图标)
│   └── zhuangbei/  # 装备图标 (仅保留被装备道具行 icon/spIcon 引用到的图标)
├── videos/         # 技能演示视频
└── data/
    └── tables.json # 自定义数据表 (如技能养成表, 网页"数据表"页自动展示)
```

## 更新流程

1. **更新表格**:直接把新的 `.xlsx` 覆盖到 `data-sources/` 对应文件(保留同名),或运行网站仓库的 `tools/一键同步.bat` 从本地策划目录自动复制
2. `git add -A && git commit -m "update" && git push`
3. 网站仓库运行 `tools/一键同步.bat`（自动 pull 本仓库 → 转换图片为 WebP → 生成网页数据 → 推送网站仓库）
4. GitHub Pages 1~2 分钟后自动更新

## 网页资源引用

网页通过 GitHub Pages 直接引用本仓库的静态资源:

- 图标: `https://lyh2387316552-ui.github.io/chronicle-data/icon/...`
- 视频: `https://lyh2387316552-ui.github.io/chronicle-data/videos/...`
- 数据表: `https://lyh2387316552-ui.github.io/chronicle-data/data/tables.json`

## 图片格式

`icon/` 中的图片统一保存为 `.webp`。新增图片可以先以 PNG/JPG 放入资源目录，网站仓库的 `tools/一键同步.bat` 会自动调用 `tools/convert-images.js` 转换并清理原格式文件。

## 道具表导出规则

`data-sources/道具表.xlsx`、`icon/item/` 与 `icon/zhuangbei/` 由网站仓库的 `tools/一键同步.bat`（`tools/copy-data.js`）从本地策划目录导出，导出时已按编年史展示规则裁剪：

- **道具表**：保留两类行——(1) `uesless != 1` 且 `itemType`（道具类型）为 `1`/`2`/`3` 的普通道具行；(2) `itemType = 4` 的普通装备行（其 `uesless` 为 `1`，仅供「普通装备」卡片按 `equip.id` 关联取图标，道具页展示时仍按 `itemType 1/2/3` 过滤，不会显示装备）。其余行不写入；源表头行（中文名/英文字段/类型）保持原样。
- **道具图标**：`icon/item/` 仅保留被上述普通道具行 `icon` 字段（`item/...` 路径）引用到的图标，未被引用的图标会被清理。
- **装备图标**：`icon/zhuangbei/` 仅保留被装备道具行（`itemType` 为 `4`/`5`）的 `icon`/`spIcon` 字段（`zhuangbei/...` 路径）引用到的图标，未被引用的图标会被清理。
