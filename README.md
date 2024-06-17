# Sync issues from GitHub to Jira

Example github workflow

```yaml
name: Sync GitHub issues to Jira example
on: [issues]

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
          JIRA_USERNAME: ${{ secrets.JIRA_USERNAME }}
          JIRA_API_TOKEN: ${{ secrets.JIRA_API_TOKEN }}
          JIRA_COMPONENT: ${{ secrets.JIRA_COMPONENT }}
          JIRA_PROJECT_KEY: ${{ secrets.JIRA_PROJECT_KEY }}
          JIRA_EPIC_KEY: ${{ secrets.JIRA_EPIC_KEY }}
```
Alternatively, one can provide the `JIRA_AUTHORIZATION` variable instead of `JIRA_USERNAME` and `JIRA_API_TOKEN`.
Now all issues labeled `jira` will be synced to Jira.

## Debug

Debug using [act](https://github.com/nektos/act) with the following command:

```bash
act -s JIRA_URL=https://jira.tld -s JIRA_USERNAME=user -s JIRA_API_TOKEN='pass' -s JIRA_COMPONENT=component -s JIRA_PROJECT_KEY=project -s JIRA_ISSUE_TYPE=Task -s JIRA_EPIC_KEY=epic -s JIRA_LABELS=bug -e test-issue.json issues
```
