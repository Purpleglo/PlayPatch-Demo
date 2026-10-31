# PlayPatch browser tester demo

This public repository contains compiled tester releases and their validation workflow. The Unity project, editable artwork, original asset packages and development history remain private.

A small HTTPS release proxy serves the compiled files from the latest verified GitHub Release. The publisher creates a draft, uploads every required attachment, verifies names, sizes and SHA-256 digests, then publishes it atomically. The previous live release remains selected during failed builds, tests or incomplete uploads. GitHub Actions validates compiled archives and hosting metadata; hosting does not use GitHub Pages.

## Tester updates

Use the same public website link for every release. New visits load the current release. A session already playing keeps its immutable assets and offers the next version at Home. Content-addressed asset routes retain their first uploaded release and attachment; old release manifests and versioned wrapper files remain available. Browser-local settings and high scores keep the same document path and origin.

Scores and settings belong to that browser. There are no player accounts, ads, purchases or shared online leaderboard. Browser rendering, audio and actual touch hardware still need tester observation.

## Published files

Each release contains the canonical compiled `playpatch-demo.zip`, plus `index.html`, `app.js`, `styles.css`, `version.json`, `release.json` and `hosting-index.json`. Only newly needed immutable engine/streaming files are uploaded again. Their attachment name is `asset-<content SHA-256>`.

The hosting index uses `{schema:1, release, sourceCommit, builtAt, files:{relativePath:{release, asset, sha256, bytes}}}`. Root files use the latest release; `app.js?v=<tag>` and `styles.css?v=<tag>` use that exact tag. `releases/<tag>/release.json` uses the tag's `release.json` attachment. Immutable asset paths use their retained index entry. The proxy streams these compiled attachments; it receives no Unity credentials or private-source access.

## Automatic publication

The local watcher fetches pushed private main into an owned clean detached worktree. It installs locked QA dependencies and runs the committed build and publication helpers there, while development continues independently in the original checkout. Unity builds in a separate cached project. A newer push can supersede an older candidate.

Build receipts bind the exact clean source commit, all Assets/Packages/ProjectSettings input hashes and all compiled output hashes. Publication verifies that receipt, freezes the committed wrapper, tests the exact upload ZIP, runs the native-save contract and real-browser smoke, then rechecks source and output before uploading. Input lists and receipts stay local. The first release can bootstrap from an exact pushed snapshot; changing an existing build workspace requires its full retained asset pool. The licensed Windows build machine must remain awake for new builds; the published site remains online independently.

Original and third-party assets remain owned by their respective authors. This compiled demo grants no right to extract, redistribute or reuse those assets.
