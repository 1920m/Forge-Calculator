# Branch archive

Old feature branches were deleted on 25 Oct 2026 to tidy the repo. **Nothing was lost**: every branch's work is on `main`, and each branch can be brought back exactly. This page records what each one was and how to restore it.

## How to bring a branch back

Pick whichever is easiest. Replace `N` with the pull request number and `NAME` with the branch name from the table.

1. **On GitHub (easiest).** Open the pull request (`/pull/N`) and press **Restore branch** near the bottom. GitHub offers this for branches deleted after their pull request closed.
2. **From the pull request's saved copy.** GitHub keeps every pull request's commits forever, even after the branch is deleted:
   ```
   git fetch origin pull/N/head:NAME
   git push origin NAME
   ```
3. **From the backup file** `forge-calculator-branches-2026-10-25.bundle` (kept offline, 2.2 MB). It holds every branch exactly as it was:
   ```
   git fetch forge-calculator-branches-2026-10-25.bundle "refs/backup/*:refs/remotes/backup/*"
   git push origin backup/NAME:refs/heads/NAME
   ```
4. **Same files, fresh branch.** To get a branch's files without its old commits, make a branch at the matching commit on `main` (last column):
   ```
   git push origin MAIN_COMMIT:refs/heads/NAME
   ```

Options 1–3 restore the original commits. The six oldest branches (marked ★) were written before the history clean-up, so their commits still carry the old co-author lines; option 4 avoids that.

## The branches

| Branch | PR | What it was | Last commit on the branch | Same files on `main` |
| --- | --- | --- | --- | --- |
| `feat/calculator` ★ | #2 | The working calculator: Forge Chances, forge slots, result card, ore picker, variants, Enhance Equipment, traits; Ores, Weapons, Armour and How it works pages; world themes and particles; game data published to Supabase. | `2c00bb1e9d18886a7a13af9dde69949ba072bb81` | `c3b3798e44a4f8d48dcba88249950c14249c4a40` |
| `feat/trait-scaling` ★ | #3 | Trait chances and damage scale with trait strength; weapon damage rounds to the hundredth; each world has its own weapon pool (World 4 Dragon Slayer, The Carver, Jack's Crest). | `3bae3e3c7b2416d935c9740fd3727b31cf38dd53` | `42da7cfef72388491b2928a70c42da06969f0a9e` |
| `feat/shop-halloween` ★ | #4 | Funguy shop blueprints roll in their world (Shop badge); Halloween weapons only in World 4; Duskwing's Cleaver, Demonic Spear, Halberd, Coffin's Lid; snow and ash particles. | `da460cfd074b58bafa61c0abc3970e7e50f14d4c` | `1e3593c75c56665be336f01c204711e92d60b227` |
| `feat/ore-filters` ★ | #5 | Filter button on the ore picker: sort by multiplier, best for armour/weapons, two-handle multiplier range, trait marks on ore tiles. | `fb8b0a1fb9cb87ed7453feae835ee0c2e0a3a064` | `9c4f06520374bc02768de609ec7c247ea5054e70` |
| `feat/four-ore-types` ★ | #6 | The forge holds at most 4 ore types; press and hold a slot to remove an ore. | `74812fd0c7f85c9e70ac184ec9c35247abb7bbc7` | `55e9e7f5225455571988631b3d7e44d1feb30910` |
| `feat/builds` ★ | #7 | Builds page with recommended mixes per world and stage, weapon DPS with traits, ore trait fixes. | `7aaca1635dc08e621ae92c6e6c38058c017eeda3` | `f1b4602e7b81a3e69fa71be8f923fb92aa50fa04` |
| `feat/readme` | #8 | New README with banner and screenshots; armour builds computed by trying every mix; status labels hidden. | `b7f53b2e59d257e8d2efcc7265798ad0de730467` | same commit |
| `sec/hardening` | #9 | Security pass: strict share-link parsing, CSP and security headers, `pg_net` removed, only the newest catalogue readable; Vercel Analytics and Speed Insights; CodeQL, Dependabot, SECURITY.md. | `4cc8ee47fc808d4efb5fd2daa65acc832dde8e5b` | same commit |
| `feat/auth` | #15 | Sign in with Google and Discord, account menu, Settings (rename, delete account), Privacy page, `profiles` table. | `ec974528b9606c55d7ddef22096692ec0a282c86` | same commit |
| `feat/saved-forges` | #16 | ☆ on the calculator to save a forge; Forger page with saved-forge cards; `saved_forges` table. | `77cac80f79aea226aac1d151f66945a2b7160995` | same commit |
| `feat/loadout` | #17 | Loadout panel on the Forger page with drag and drop, slot pickers and pickaxes; `loadouts` table. | `bc4309f6771884c47a211f8a74f6d632776f4a51` | same commit |

"Same commit" means the branch's last commit is itself part of `main`.

## Kept on purpose

`feat/foundation` (PR #1, closed without merging, last commit `ee7131688e21768cbd79059d5833bd93b24a6236`) was **not** deleted. It is the first scaffold of the project and holds 41 files that aren't on `main`: the original design handoff and design boards (`forge-calculator-handoff/`), the seed data sources and audits (`supabase/seed/`), and the early data scripts and docs. The calculator was rebuilt differently in #2, so it was never merged, but its material is worth keeping.
