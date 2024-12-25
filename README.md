# ghstack GitHub Actions

This GitHub Action is a tool that enables you to land pull requests using
ghstack directly from GitHub Pull Requests. It adds a command that can be used
in pull request comments to check the status and automatically land the PR using
ghstack.

## Required Permissions

For this action to work properly, it needs the following repository permissions:
- `contents: write` - To push changes when landing the PR
- `pull-requests: write` - To update and merge pull requests

## Usage

Simply comment on any pull request to trigger the action. The action will:
1. Check if the PR is ready to be landed
2. Use ghstack to land the changes if all checks pass

## Example Configuration

Add the following to your `.github/workflows/ghstack.yml`:

```yaml
name: ghstack
on:
  issue_comment:
    types: [created]
permissions:
  contents: write
  pull-requests: write
jobs:
  ghstack:
    runs-on: ubuntu-latest
    steps:
      - uses: shikanime/ghstack-actions@main
        with:
            appId: ${{ secrets.APP_ID }}
            privateKey: ${{ secrets.PRIVATE_KEY }}
```

This configuration will enable the ghstack action to run whenever a comment is
added to a pull request.
