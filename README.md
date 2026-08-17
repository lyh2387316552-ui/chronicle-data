# 古荒大陆编年史 - 数据与资源仓库

游戏数据与资源仓库,供 [chronicle 网站仓库](https://github.com/lyh2387316552-ui/chronicle) 使用。

## 目录结构

```
chronicle-data/
├── data-sources/   # 数据源表格 (Skill/Stunt/属性表/装备表/宝石表/技能表/技能标签/魔宠表)
├── icon/           # 游戏图标资源 (技能/装备/宝石/魔宠/职业天赋)
├── videos/         # 技能演示视频
└── data/
    └── tables.json # 自定义数据表 (如技能养成表, 网页"数据表"页自动展示)
```

## 更新流程

1. 本地修改/新增资源文件(游戏导出、策划表格更新)
2. `git add -A && git commit -m "update" && git push`
3. 网站仓库运行 `tools/一键同步.bat` 拉取最新数据并重新生成网页数据
4. 推送网站仓库后, GitHub Pages 自动更新

## 网页资源引用

网页通过 GitHub Pages 直接引用本仓库的静态资源:

- 图标: `https://lyh2387316552-ui.github.io/chronicle-data/icon/...`
- 视频: `https://lyh2387316552-ui.github.io/chronicle-data/videos/...`
- 数据表: `https://lyh2387316552-ui.github.io/chronicle-data/data/tables.json`
