# ITD110 Consolidation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Turn ITD110-Act2 into the ITD110 monorepo and retire the stale repos.
**Architecture:** In-place fix on a branch + PR; git filter-repo for act1 history; gh for renames/archives.
**Tech Stack:** git 2.53, git-filter-repo, gh.
**Spec:** `docs/superpowers/specs/2026-11-25-itd110-consolidation-design.md`

## Global Constraints
- Commit messages pass the global commit-msg hook (≤72 subject and body width).
- Every push, rename and archive is approved by the user (guardrail prompts).

## Review Focus
1. `act1/` must hold real files (mode 100644/tree), not a gitlink (160000).
2. `git log -- act1` shows itd110's 4 commits.
3. No remaining 160000 entries anywhere in the tree.
4. Rename order: itd110 must be renamed before ITD110-Act2 → ITD110.
5. Notes must be pushed before archiving (archived repos reject pushes).

### Task 1: Branch commits (local)
- [ ] `git rm --cached act1`, then filter-repo itd110 → `act1/`, then `merge --allow-unrelated-histories`. Commit: `fix(act1): replace broken gitlink with itd110 history`.
- [ ] `git rm --cached "Case Study 1 - Pounce"`, `git rm dump.rdb act2/dump.rdb`, add `dump.rdb` to `.gitignore`. Commit: `chore: remove broken Pounce gitlink and Redis dumps`.
- [ ] Add README index + these docs. Commit: `docs: add ITD110 index README and consolidation docs`.
- [ ] Verify: `git ls-tree -r HEAD | awk '$1=="160000"' | wc -l` → 0; `git log --oneline --no-merges -- act1 | wc -l` → 4; `git ls-files | grep -c dump.rdb` → 0; `git diff master --stat -- act2/backend act3 act4 "Case Study 2 - AgriChain"` → empty.

### Task 2: PR
- [ ] Push branch, `gh pr create --base master` with the CLAUDE.md sections. Verify: PR URL, mergeable.

### Task 3: After the user merges
- [ ] Moved notes on itd110 (`act1`) and ITD110-Act3 (`act3`), pushed to `main`.
- [ ] `gh repo rename ITD110-Act1 -R MirkoLouis/itd110`; archive ITD110-Act1 and ITD110-Act3.
- [ ] `gh repo rename ITD110 -R MirkoLouis/ITD110-Act2`; set the description.
- [ ] Verify: `gh api repos/MirkoLouis/ITD110 --jq .full_name`; `archived=true` for both; the old URL `ITD110-Act2` redirects.
