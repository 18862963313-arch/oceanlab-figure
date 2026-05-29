# oceanlab-figure

**OceanLab Figure** — 海洋论文/报告配图工具箱（**路由入口 Skill**）

用户**只安装这一个 Skill**；Agent 按数据域自动分流到分支 Skill 执行。

## 家族结构

```
OceanLab Figure（品牌 · 本目录 = 路由）
├── oceanlab-physocean    物理海洋观测     ★ 首发
├── oceanlab-seafloor     海底地形地貌     ✅ GitHub
└── （后续按数据域扩展）
```

完整索引：[OCEANLAB-FIGURE-FAMILY.md](../OCEANLAB-FIGURE-FAMILY.md)

**Repository:** https://github.com/18862963313-arch/oceanlab-figure

## Install

```bash
# 三个目录必须同级安装
cp -r oceanlab-figure oceanlab-physocean oceanlab-seafloor ~/.cursor/skills/
```

对话中触发 **`oceanlab-figure`** 或「OceanLab 配图 / 期刊图 / GEBCO / θ–S」即可；路由 Skill 会加载对应分支。

## 本目录内容

| 文件 | 作用 |
|------|------|
| `SKILL.md` | 路由规则 — **先读这个** |
| `references/routing.md` | 路由表 + 边界 case |
| `README.md` | 本说明 |

**不含** plotting 脚本 — 脚本在 `oceanlab-physocean/` 与 `oceanlab-seafloor/`。

## 分支速查

| 要什么 | 分支 |
|--------|------|
| CTD、θ–S、断面、Argo、gsw、玫瑰图 | `oceanlab-physocean` |
| GEBCO、测线、海底地形 | `oceanlab-seafloor` |

## License

MIT — branch skills carry their own LICENSE files.

*OceanLab · Figure 配图工具箱*
