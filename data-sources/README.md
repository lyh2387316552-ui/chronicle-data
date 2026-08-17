# 📁 data-sources 数据源目录

> 表格文件直接平铺在本目录（不要文件夹包装），JSON 技能数据按文件夹存放。更新数据 = 覆盖对应文件后 `git push`，再运行网站侧 `一键同步.bat`。

## 数据源放置说明

| 文件/文件夹 | 内容 | 支持格式 |
|---|---|---|
| `Skill/` | 主动技能（战斗数据） | `Basic_Information-*.json` |
| `SkillModule/` | 主动技能模块（伤害/冷却等） | `module-*.json` |
| `Stunt/` | 被动技能（战斗数据） | `baseStuntInfo-*.json` |
| `StuntModule/` | 被动技能模块 | `module-*.json` |
| `属性表.xlsx` | 词缀 + 属性数据 | Excel/CSV |
| `装备表.xlsx` | 装备数据（LegendEquip + Modifier 子表） | Excel/CSV |
| `技能养成相关.xlsx` | 辅助宝石 + 技能库（SkillGem / SkillActive 子表） | Excel/CSV |
| `战斗技能相关表.xlsx` | 技能标签字典（SkillMainTag + SkillNormalTag 子表） | Excel/CSV |
| `魔宠表.xlsx` | 魔宠数据（Pet / PetStar 子表） | Excel/CSV |

> 说明：`技能养成相关.xlsx` 同时供给辅助宝石和技能库两类数据；`属性表.xlsx` 同时供给词缀和属性两类数据。

## 使用步骤（更新数据）

1. 把新的表格文件**直接覆盖**到对应位置（保留同名文件名）
2. `git add -A && git commit -m "update tables" && git push`
3. 在网站仓库双击 `tools\一键同步.bat`：自动 pull 本仓库 → 生成网页数据 → 推送网站仓库 → 线上自动更新

## Excel 子表自动查找规则

系统自动按子表名匹配（不区分大小写，取第一个命中的工作表）：

| 库 | 子表名（任一命中即可） | 字段规则 |
|---|---|---|
| 装备库 | `LegendEquip` / `装备` | name + desc999 → 装备名称；modifier1 + modifier2 → 词条ID |
| 装备库词条 | `Modifier` / `词条` | id → 词条ID；stunt / affix / attr → 战斗数据中的被动/词缀/属性效果 |
| 宝石库 | `SkillGem` / `宝石` | name → 名称；desc → 描述；skillAffix / stunt / attr → 映射词缀/被动/属性 |
| 技能库 | `SkillActive` / `技能` | skill / stunt → 映射战斗数据中的技能ID，读取效果描述与标签（mainTag / normalTag） |
| 技能标签 | `SkillMainTag` / `主标签` + `SkillNormalTag` / `常规标签` | 标签ID → 标签文本（如 1=攻击、2=法术；1=近战、3=火焰） |

## 词缀 / 属性表说明

- 系统自动查找 `属性表.xlsx` 中名字包含 "Modifier / Affix / 词缀" 的工作表作为词缀数据
- 含 `attrID / name / desc` 列的工作表作为属性数据
- 路径约定：以上相对路径均相对本仓库；网站仓库的 `tools/import-config.json` 指向本目录
