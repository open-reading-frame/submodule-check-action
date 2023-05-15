# submodule-check-action

This action will assert that the calling repository's submodules are all on commits in the default branch's commit history for each respective submodule.
Essentially requires submodules to be on a "prod-ready" commit to be merged.
This action is intended to be used to gate pull requests where the repository's default branch is the base branch in the pull request.
The provided secret must have read access to all repositories used as submodules

## Example

```yaml
# This template is intended to be incorporated as a workflow in another repository for pull request gating
name: Run Submodule Check
on:
  pull_request:
    # branches: [main] # Uncomment to gate only pull requests to main (or another default branch)
    types: [opened, edited, synchronize, reopened]

jobs:
  run-submodule-check:
    runs-on: ubuntu-latest
    steps:
      - name: Run the submodule check workflow
        uses: open-reading-frame/submodule-check-action@main
        with:
          token: ${{ secrets.REPO_READ_ACCESS }}
```
