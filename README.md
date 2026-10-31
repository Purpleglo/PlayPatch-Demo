# PlayPatch browser tester demo

This public repository holds the deployment workflow for the compiled PlayPatch tester demo. The Unity project, editable artwork, original asset packages and development history remain in the private organisation repository.

The website is published from a tested `playpatch-demo.zip` attached to each GitHub Release. GitHub Actions downloads that compiled site and deploys it to GitHub Pages. It does not build Unity and needs no Unity licence or external hosting credentials. The built-in repository token is restricted to reading release assets, publishing Pages and requesting the Pages identity token.

## Tester updates

Use the same website link for every release. Newly opened visits load the current release. A session already playing keeps its immutable engine/assets; the page offers the next version at Home. Content-hashed assets and every prior release manifest are retained so an update cannot replace files underneath a running game. The wrapper keeps the document path stable for browser-local settings and scores.

Scores and settings are local to that browser. There are no player accounts, ads, purchases or shared online leaderboard. Browser rendering and input are an additional test target; passing the Windows preview does not establish browser or physical-tablet performance.

## Deployment

Enable **Settings > Pages > Source: GitHub Actions** once. The `Deploy compiled tester demo` workflow runs when a GitHub Release is published. Its release must contain exactly one `playpatch-demo.zip` built by the private project's browser tooling after a real-browser smoke test. Manual dispatch retries only the latest published release. Older release events are skipped, and the latest tag is checked again immediately before deployment. An old archive cannot be selected for rollback because it could omit assets still used by a newer running session.

The build helper records the clean source commit and deterministic hashes of every Assets/Packages/ProjectSettings input before mirroring, in the isolated copy, and after building. It also records every compiled output hash. The publisher checks that receipt, current inputs and actual output before packaging and again before upload; an old or modified build cannot be relabelled as a newer commit. Input lists and receipts stay local.

The publisher keeps an exclusive local lock, freezes the wrapper from the attributed Git commit, verifies it inside the exact upload ZIP and runs native-save and real-browser checks against that candidate. Immediately before upload it rechecks the candidate commit, pushed private main and clean source. It then waits for the matching deployment and checks the public version manifest. A failed build/test/deployment leaves the last successful public deployment in place.

The local watcher fetches pushed private main into a dedicated clean detached worktree and runs the committed tools and locked browser-QA dependencies there. Unity builds in a separate cache project. Development can continue in the original working checkout, including uncommitted edits; those files are never used for automatic publication or checked out by the watcher. A newer push can supersede an older candidate. A new demo can bootstrap its first public release from that exact pushed snapshot; an existing demo requires its complete retained asset pool when changing workspaces. The licensed Windows build machine must remain running for new builds.

Local preview builds may include uncommitted work, but their receipts do not qualify for public publication. Automatic detached snapshots are clean and require no historical-edit fingerprint CSV.

Original and third-party assets remain owned by their respective authors. This compiled demo grants no right to extract, redistribute or reuse those assets.
