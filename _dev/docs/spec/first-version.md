# Heron's first version

What Heron's first version is: a tool that follows the upstreams a project is tied to, tells the project what changed, and keeps a record of how each change was judged. It grows from the upstream-bot idea, a private note the repository does not track.

## Scope

- In: the detector, the ledger, setup, the pull-request comment and the skill; npm and PyPI; upstreams on GitHub and an adopter's repo on GitHub; `a2uiverse` and `a2uiverse-apps` as the first adopters.
- Out: a hosted agent, a setup UI, forks and followed spec or protocol versions as kinds of entanglement, Cargo, Go and other ecosystems, forges other than GitHub, and Salmon, the contribution pack.

## Locked decisions

### 1. The detector and the ledger, as a plugin with skills

Heron's first version is the detector and the ledger, shipped as a Claude Code plugin with skills. There is no hosted agent: a judgement is proposed by the adopter's own agent, in its session.

### 2. One detector, three moments

The detector runs on a schedule in CI, daily by default, the interval the adopter's choice; setup says that GitHub turns off a public repo's scheduled workflows after 60 days with no activity. It runs on a pull request in the adopter's repo that touches what depends on upstream. It runs on demand, through the CLI or the skill, each project's own workflow deciding when. The three moments run the same detector.

### 3. What Heron watches

Heron watches the places a project is tied to another's code. It finds three kinds in the repo by itself: a patched dependency, a vendored copy, and a wait. The adopter writes a fourth kind, a pin held back on purpose, once, with its reason. A patched dependency is a patch file, checked by whether the patch reverse-applies to a release, or a source pointed at a fork or a commit, checked by which of the fork's commits a release already has.

### 4. Where waits are found

Heron looks for waits in code comments, in the project's own open issues and in its documents. A link to upstream is a wait only when the words around it say so, such as once, until, when it ships or is released, blocked, waiting, drop or remove; the same rule holds in every source. At setup the skill drops the false candidates.

### 5. What a wait can say

A wait is written in a small closed set of mechanical conditions where it can be: a release at or above a version, a pull request merged or an issue closed, a release that contains a pull request, a change to upstream's copy of a file. A wait no condition states stays prose: the dashboard marks it as possibly met, needing a reading, whenever its upstream moves, and the skill reads it at the next check. At setup and at each deferral the skill states the wait in the closed set where it can.

### 6. Setup

The skill runs the scan, explains each finding in plain words, and fills in what the scan cannot: a pin's reason from the git history, the upstream of an ambiguous copy, a wait-comment stated as a condition. It ends by opening a setup pull request; merging it confirms the setup. Without an agent, the CLI opens the same pull request with the reasons left blank.

### 7. The ledger

The ledger is one dashboard issue, rewritten by every run: what upstream did since the pin, every open event, and every wait and how it stands. An event that needs a decision gets an issue of its own. Closed as completed, it was adopted; closed as not planned, it does not affect the project, the reason in the closing comment; open with a deferred label, it waits on a stated condition. A wait met is a comment on the dashboard. A repo with issues turned off has the dashboard written to a file.

### 8. Facts are the detector's, judgements are a person's

The detector clears what facts settle: an event that un-happened, and a line that was never a decision, which goes on the dashboard with no issue. Every judgement, to adopt, to call it not affecting or to defer, is proposed by the skill and closed only on a person's word. The model never closes an event alone. A judgement is made against the pin, so a change judged not affecting is read again at the next release.

### 9. The pull-request comment

On a pull request that meets an entanglement, Heron posts one comment and edits it in place; on any other pull request it says nothing. The comment states what the detector knows of each entanglement the pull request meets, such as whether a patch still applies, is in a release or no longer applies, and how upstream's copy of an edited vendored file changed since the pin. It says which waits and patches Heron will start or stop watching; those take effect in the ledger once the pull request merges. It never fails a pull request. Pull requests from forks get it too: their run computes the comment, and a separate run with write access posts it.

### 10. npm and PyPI, on GitHub

The first version covers npm and PyPI, upstreams on GitHub and an adopter's repo on GitHub. Each ecosystem is an adapter of its own.

### 11. One program in three wrappings

Heron is one program, delivered as an npm package with a CLI, as a GitHub Action, and as a Claude Code plugin. The adopter's repo holds only thin workflow files that call Heron's own workflows at a tag. The plugin carries the skill, which is also published in the open Agent Skills format and calls the CLI. Where Node is not installed, the skill starts a manually triggered workflow run and reads its result.

### 12. The name

The name is Heron. The repository is `retz8/heron` and the plugin `heron`. The npm package takes a free name, reserved early. The `@heron` mention is not available on GitHub; a later GitHub App picks its handle then.

### 13. Its own repository

Heron has its own repository, public from its first commit, under the Apache License 2.0, in the folder `heron/` beside the other projects. The repository is its own plugin marketplace.

### 14. Its own daily-work harness

The work on Heron runs on the daily-work harness in Heron's own `_dev/`. A2UIVerse's TODO carries one line for adopting Heron.

### 15. The first adopters

`a2uiverse` and `a2uiverse-apps` adopt Heron first. Once Heron covers what A2UIVerse's "Upstream releases" workflow reads, that workflow and its readings script retire, and Duet, which reads both projects' upstream notices each morning, reads Heron's dashboards in their place. Spectra adopts Heron later, keeping its own readings for what Heron does not know.

### 16. Phase 21's hand readings

Until Heron is adopted, A2UIVerse's Phase 21, its move to A2UI v1.0, checks upstream by hand at the start of every sub-task. Each of those readings is a test case for Heron: what its dashboard should have shown at that moment.

### 17. What proves the first version

1. On `a2uiverse` and `a2uiverse-apps`, the skill's setup pull request finds what is there with nothing written by hand: the two pnpm patches, the vendored specification matched to the commit its `UPSTREAM.json` records, the waits in the TODO's Backlog, and the exact PyPI pins as pins held on purpose with their reasons from the git history. Both pull requests merge.
2. The dashboard matches Phase 21's hand readings for the same moment.
3. One real event is judged end to end: the patch on `@a2ui/web_core` against 0.16.1, which ships `addCatalog` in other code, Heron saying mechanically whether the patch reverse-applies or no longer applies, and the judgement closed with its reason.
4. A real pull request that bumps a patched package gets the comment: the Phase 21 sub-task that moves A2UIVerse's client off its patch on `@a2ui/web_core`, or a scratch pull request.
5. The scan runs read-only on public repositories that are not ours, chosen for their patch files, vendored files or waits in their issues, opening nothing on them.
6. Heron's own gates are green.

### 18. Nothing of Salmon

The first version does nothing toward Salmon. The pull-request comment states facts only.

## Invariants

- Detection is facts, with no judgement in it.
- Every event ends judged: adopted, not affecting with its reason, or deferred on a stated condition.
- Plain version bumps stay Renovate's and Dependabot's.

## Open items

- The npm package's name.
- Which public repositories proof 5 scans: Heron's own acceptance spec.
- How the first version splits into phases.
