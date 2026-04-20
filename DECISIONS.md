# Chem-Dry of Richmond — Decisions Log

Append-only. Newest at the bottom. Never delete entries — if a decision is reversed, add a new entry referencing the old one.

---

## 2026-04-20: Use a separate `chem-dry-ops` repo distinct from `chem-dry-stack`

**Context:** We need persistent project memory so Claude sessions don't start from zero. The code repo (`chem-dry-stack`) has been accumulating tangential context that belongs in docs, not code.

**Decision:** Stand up a dedicated `chem-dry-ops` command center repo holding the 5 living docs. Code stays in `chem-dry-stack`, memory lives in `chem-dry-ops`.

**Reasoning:** Separating machine from manual keeps both clean. Code repo commits stay focused on code. Ops repo becomes the context layer Claude reads on every session. Also aligns with the agency pattern — every future client gets the same two-repo shape.

**Alternatives considered:**
- Keep everything in `chem-dry-stack` with a `/docs` folder — rejected because it conflates concerns and creates noisy git history
- Use Claude project knowledge only (no GitHub) — rejected because versioning, diffs, and mobile editing all suffer

**Revisit if:** The two-repo pattern becomes a coordination burden in practice.

---

## (earlier decisions to backfill as needed)

As architectural decisions from the original build get remembered or re-examined, backfill them here with best-guess dates. Don't fabricate specifics — if reasoning is unclear, note that.