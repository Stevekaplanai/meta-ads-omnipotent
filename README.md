# meta-ads-omnipotent

A Claude skill for complete Meta advertising mastery. Three layers that build on each other:

| Layer | What it holds | Where it came from |
|---|---|---|
| **Part I — The Machine** | How Meta's delivery stack actually decides: Andromeda (retrieval), GEM (foundation model), Lattice (ranking), Sequence Learning (journey), SUM (user modelling), DLRM (conversion prediction) | Meta engineering publications, distilled |
| **Part II — The Audit** | 50 weighted operational checks: Pixel/CAPI health, creative diversity + fatigue, account structure, audience — each check tied back to the system in Part I it protects | Adapted from [claude-ads](https://github.com/AgriciDaniel/claude-ads) `ads-meta` |
| **Part III — The Build** | The Andromeda-optimal playbook: launch structure, creative production system, scaling rules, journey-based retargeting, diagnostics | Synthesis of I + II |

## Install

Copy `SKILL.md` into a `meta-ads-omnipotent/` folder under your Claude skills directory:

```
cd %USERPROFILE%\.claude\skills
mkdir meta-ads-omnipotent
copy <this repo>\SKILL.md meta-ads-omnipotent\SKILL.md
```

Invoke as `/meta-ads-omnipotent`, or let Claude load it whenever a task involves auditing, building, or diagnosing Meta ad accounts.

## Why "the algorithm layer" matters

Since Andromeda's global rollout (Oct 2025), creative diversity is a **delivery prerequisite** — ads sharing >60% of visual/audio features get retrieval-suppressed before any auction happens. Most audit checklists test symptoms; this skill ties every operational check to the specific system that punishes the violation, so recommendations are grounded in how delivery actually works.
