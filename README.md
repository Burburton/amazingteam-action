# AmazingTeam GitHub Action

This action sets up AmazingTeam Foundation for AI-powered development in your workflow.

## Usage

```yaml
- name: Setup AmazingTeam
  uses: Burburton/amazingteam-action@v1
  with:
    version: '3.0.18'
    config: 'amazingteam.config.yaml'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `version` | AmazingTeam Foundation version | No | `3.0.18` |
| `config` | Path to amazingteam.config.yaml | No | `amazingteam.config.yaml` |
| `overlay` | Technology overlay to apply | No | `''` |
| `cache` | Enable caching | No | `true` |
| `cache-dir` | Cache directory | No | `~/.amazing-team-cache` |

## Outputs

| Output | Description |
|--------|-------------|
| `foundation-path` | Path to downloaded foundation |
| `setup-complete` | Whether setup completed |
| `version` | Foundation version used |

## Example Workflow

```yaml
name: AmazingTeam

on:
  issue_comment:
    types: [created]

jobs:
  amazing-team:
    if: startsWith(github.event.comment.body, '/ai')
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
      issues: write
    
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup AmazingTeam
        uses: Burburton/amazingteam-action@v1
        with:
          version: '3.0.18'
      
      - name: Run OpenCode
        uses: anomalyco/opencode/github@latest
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## License

MIT