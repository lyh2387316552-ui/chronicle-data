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
│   └── 魔宠表.xlsx   # 魔宠
├── icon/           # 游戏图标资源 (技能/装备/宝石/魔宠/职业天赋)
├── videos/         # 技能演示视频
└── data/
    └── tables.json # 自定义数据表 (如技能养成表, 网页"数据表"页自动展示)
```

## 更新流程

1. **更新表格**:直接把新的 `.xlsx` 覆盖到 `data-sources/` 对应文件(保留同名),或运行网站仓库的 `tools/一键同步.bat` 从本地策划目录自动复制
2. `git add -A && git commit -m "update" && git push`
3. 网站仓库运行 `tools/一键同步.bat`(自动 pull 本仓库 → 生成网页数据 → 推送网站仓库)
4. GitHub Pages 1~2 分钟后自动更新

## 网页资源引用

网页通过 GitHub Pages 直接引用本仓库的静态资源:

- 图标: `https://lyh2387316552-ui.github.io/chronicle-data/icon/...`
- 视频: `https://lyh2387316552-ui.github.io/chronicle-data/videos/...`
- 数据表: `https://lyh2387316552-ui.github.io/chronicle-data/data/tables.json`
