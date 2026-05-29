# OceanLab Figure — Routing Reference

> Agent loads this when the main router table in `SKILL.md` is insufficient.  
> Authoritative family doc: [OCEANLAB-FIGURE-FAMILY.md](../../OCEANLAB-FIGURE-FAMILY.md)

## Decision flow

```
User request
    │
    ├─ CTD / θ–S / section / Argo / gsw / GO-SHIP / buoy obs?
    │       └─► oceanlab-physocean/SKILL.md
    │
    ├─ GEBCO / bathymetry / survey track / MBES coverage?
    │       └─► oceanlab-seafloor/SKILL.md
    │
    ├─ Both (e.g. cruise Fig.1)?
    │       └─► Run each branch → composite with panel labels a/b/…
    │
    └─ Offshore wind site screening?
            └─► offshore-wind-metocean-assessment (Assess · 蓝色工程支线 · 非主路线)
```

## Edge cases

| Case | Route |
|------|-------|
| Station map with CTD stations on GEBCO | **seafloor** draws basemap; **physocean** supplies station overlay spec (`station-map-style.md`) |
| Satellite SSH/SSS gridded context only | **seafloor** or Tier-C context panel; label product |
| User says "oceanlab figure" without detail | Ask: 观测温盐 vs 海底地形 vs 两者 composite |
| User asks for CTD on seafloor skill | Redirect to **physocean** via router |

## Path resolution

When installed as sibling skills:

```
~/.cursor/skills/
├── oceanlab-figure/      ← router (this)
├── oceanlab-physocean/   ← branch
└── oceanlab-seafloor/    ← branch
```

In monorepo development:

```
_other/Vibecoding/
├── oceanlab-figure/
├── oceanlab-physocean/
└── oceanlab-seafloor/
```

Branch paths are **relative to router directory**: `../oceanlab-physocean/SKILL.md`, `../oceanlab-seafloor/SKILL.md`.
