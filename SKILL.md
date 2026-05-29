---
name: oceanlab-figure
description: >-
  OceanLab Figure family router — publication-grade ocean figure workflows. Install this ONE skill;
  it auto-routes to branch skills by data domain. Routes to oceanlab-physocean for CTD, T-S,
  hydrographic sections, Argo, gsw, GO-SHIP, buoy roses; to oceanlab-seafloor for GEBCO bathymetry,
  MBES survey maps, track coverage, seafloor context panels. Use when the user asks for 海洋论文配图,
  OceanLab Figure, 期刊图, CTD, θ-S, 温盐断面, GEBCO, 海底地形, bathymetry, survey map, or
  journal-ready ocean figure exports. NOT for ROMS/FVCOM model output or offshore wind screening.
---

# OceanLab Figure (`oceanlab-figure`) — Router

**Brand:** OceanLab Figure — publication-grade ocean figure workflows  
**Role:** **Meta / router skill only** — do not implement plotting here; load the correct **branch skill** and follow it end-to-end.

## First move: route, then load branch

1. Read [../OCEANLAB-FIGURE-FAMILY.md](../OCEANLAB-FIGURE-FAMILY.md) if routing is ambiguous.
2. Pick branch from table below.
3. **Read and follow the branch `SKILL.md` in full** — treat it as the active skill for this task.
4. If the request spans branches (e.g. GEBCO basemap + θ–S), run each branch separately, then merge panels in a composite step.

## Routing table

| User intent (keywords) | Branch skill | Path |
|------------------------|--------------|------|
| CTD, θ–S, T-S, 温盐断面, 混合层, gsw, TEOS-10, Argo, GO-SHIP, CCHDO, buoy 时序/玫瑰/stick/谱, 物理海洋观测 | **`oceanlab-physocean`** | [`../oceanlab-physocean/SKILL.md`](../oceanlab-physocean/SKILL.md) |
| GEBCO, 海底地形, 测深图, 测线覆盖, MBES, survey map, bathymetry, 站位底图, seafloor context | **`oceanlab-seafloor`** | [`../oceanlab-seafloor/SKILL.md`](../oceanlab-seafloor/SKILL.md) |
| 场址风浪流筛查, ERA5 工程 memo | `offshore-wind-metocean-assessment` — **Assess · 蓝色工程支线**（非 Figure；见 OCEANLAB-TOOLBOX.md） |
| 公众号排版 | **`md2wechat`** | (separate skill) |

## Branch summary

| Branch | 中文 | Default journal | Status |
|--------|------|-----------------|--------|
| `oceanlab-physocean` | 物理海洋观测 | JPO (`jpo-ams`) | **家族首发 MVP** |
| `oceanlab-seafloor` | 海底地形地貌 | L&O (`aslo-lo`) | MVP · 待发布 |

## Install (one entry point)

Copy router **and** branch folders together (sibling paths required):

```bash
cp -r oceanlab-figure oceanlab-physocean oceanlab-seafloor ~/.cursor/skills/
# or project-level: .agents/skills/
```

User invokes **`oceanlab-figure`** only. Agent loads branch skills from sibling directories.

If branch folder missing, tell user to install the full OceanLab Figure pack (three folders above).

## Shared family rules

- **One branch = one data chain** — no万能 `plot_ocean()`.
- **Figure contract before code** — branch skills define contract templates.
- **No jet / wrong depth axis / silent QC drops** — see branch anti-patterns.
- **Composite figures** — each panel from its branch; document panel provenance in caption.

## When NOT to use OceanLab Figure

- ROMS / FVCOM / NEMO model output fields → mode-specific workflow (not in family MVP).
- Certified IHO nautical charts → not supported.
- Social infographics (9:16 cards) → `md2wechat` / `tata-infographic`.
- Generic Nature cell biology figures → `nature-figure` if available.

## Example routing

| User says | Route to |
|-----------|----------|
| 「Argo 画 θ–S，JPO 单栏」 | `oceanlab-physocean` |
| 「GEBCO 拉南海北部，L&O 海底地形」 | `oceanlab-seafloor` |
| 「航次 Fig.1：左 GEBCO 站位，右 θ–S」 | seafloor (panel a) + physocean (panel b) |
| 「帮我做海上风电场址筛查」 | `offshore-wind-metocean-assessment`（蓝色工程 · 按需） |

## References (router level)

| File | When |
|------|------|
| [../OCEANLAB-FIGURE-FAMILY.md](../OCEANLAB-FIGURE-FAMILY.md) | Family structure, publish order, shared assets |
| [references/routing.md](references/routing.md) | Duplicate routing table + edge cases |
