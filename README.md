# Sync issues from GitHub to Jira
[![REUSE status](https://api.reuse.software/badge/github.com/cloudoperators/sync-issues-github-jira)](https://api.reuse.software/info/github.com/cloudoperators/sync-issues-github-jira)
Example github workflow

```yaml
name: Sync GitHub issues to Jira example
on: [issues]

concurrency:
  group: sync-issues-to-jira-${{ github.event.issue.number }}

jobs:
  sync-issues:
    name: Sync issues to Jira
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: cloudoperators/sync-issues-github-jira@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          JIRA_URL: ${{ secrets.JIRA_URL }}
          # Provide either JIRA_USERNAME and JIRA_API_TOKEN or JIRA_AUTHORIZATION.
          JIRA_USERNAME: ${{ secrets.JIRA_USERNAME }}
          JIRA_API_TOKEN: ${{ secrets.JIRA_API_TOKEN }}
          JIRA_COMPONENT: ${{ secrets.JIRA_COMPONENT }}
          JIRA_PROJECT_KEY: ${{ secrets.JIRA_PROJECT_KEY }}
          JIRA_EPIC_KEY: ${{ secrets.JIRA_EPIC_KEY }}
```
Alternatively, one can provide the `JIRA_AUTHORIZATION` which is mutually exclusive with `JIRA_USERNAME` and `JIRA_API_TOKEN`.
Now all issues labeled `jira` will be synced to Jira.

## Debug

Debug using [act](https://github.com/nektos/act) with the following command:

```bash
act -s JIRA_URL=https://jira.tld -s JIRA_USERNAME=user -s JIRA_API_TOKEN='pass' -s JIRA_COMPONENT=component -s JIRA_PROJECT_KEY=project -s JIRA_ISSUE_TYPE=Task -s JIRA_EPIC_KEY=epic -s JIRA_LABELS=bug -e test-issue.json issues
```
