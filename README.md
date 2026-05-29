# git-devkit

Standalone, dependency-light GitHub tooling for personal repos: README **badge blocks**, a small async **GitHub client**, and **file** + **report** helpers. No external project coupling - install it anywhere.

## Install

```bash
pip install "git-devkit @ git+https://github.com/perditioinc/git-devkit.git"
```

(Public repo, so no token needed to install.)

## Badges

Generate/refresh a badge block in a README. The block is delimited by markers so re-runs replace it in place:

```python
from git_devkit.badges import BadgeBlock

block = BadgeBlock(
    repo="owner/repo",
    test_workflow="test.yml",     # GitHub Actions test workflow -> live status badge
    workflow="sync.yml",          # optional second (nightly/main) workflow badge
    suite="Reporium",             # optional suite tag (see SUITE_COLORS)
    metrics={"repos": "826"},     # optional informational badges
    python_version="3.11+",
)
block.update_readme("README.md")  # replaces the block between the markers; returns True if changed
```

Markers (placed in your README where badges should appear):

```html
<!-- git-devkit-badges-start -->
<!-- git-devkit-badges-end -->
```

If the markers are absent, the block is inserted after the first heading.

## Modules

- `git_devkit.badges` - badge block generation + in-place README update.
- `git_devkit.github` - async `GitHubClient` (get repo, read/update file contents) over `httpx`.
- `git_devkit.files` - `atomic_write`, `update_badge_value`.
- `git_devkit.report` - `write_last_run` and run-report helpers.

## Develop

```bash
pip install -e ".[dev]"
pytest
```
