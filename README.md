# Workflows Semantic Release

A reusable GitHub Actions workflow for automating releases using [semantic-release](https://semantic-release.gitbook.io/semantic-release/).

## Features

- Fully automated release process
- Semantic versioning based on commit messages
- Generates changelogs automatically
- Configurable Node.js version
- Customizable semantic-release plugins
- Supports main, alpha, and beta release branches

## Usage

### Basic Setup

1. Create a workflow file in your repository (e.g., `.github/workflows/release.yaml`):

```yaml
name: Semantic Release

on:
  push:
    branches:
      - main
      - alpha
      - beta
  workflow_dispatch:

jobs:
  semantic-release:
    name: Create Release
    uses: circleeh/workflows-semantic-release/.github/workflows/semantic-release.yaml
    secrets:
      github-token: ${{ secrets.GITHUB_TOKEN }}
```

### Advanced Configuration

You can customize the workflow using optional inputs:

```yaml
with:
  node-version: "lts/*"
  extra-plugins: "@semantic-release/git @semantic-release/changelog"
  fetch-depth: 0
```

## Inputs

| Name            | Description                         | Required | Default                                             |
| --------------- | ----------------------------------- | -------- | --------------------------------------------------- |
| `node-version`  | Node.js version to use              | No       | `lts/*`                                             |
| `extra-plugins` | Additional semantic-release plugins | No       | `@semantic-release/git @semantic-release/changelog` |
| `fetch-depth`   | Number of commits to fetch          | No       | `0`                                                 |

## Secrets

| Name           | Description                     | Required |
| -------------- | ------------------------------- | -------- |
| `github-token` | GitHub token for authentication | Yes      |

## Prerequisites

1. Your repository should use [Conventional Commits](https://www.conventionalcommits.org/) for commit messages
2. You need a valid `package.json` file in your repository
3. Configure semantic-release using `.releaserc`, `releaserc.yaml` or `package.json`

## Example .releaserc.yaml Configuration

```yaml
---
branches:
  - main
  - name: alpha
    prerelease: true
  - name: beta
    prerelease: true
plugins:
  - "@semantic-release/commit-analyzer" # Plugin documentation: https://github.com/semantic-release/commit-analyzer
  - "@semantic-release/release-notes-generator" # Plugin documentation: https://github.com/semantic-release/release-notes-generator
  - "@semantic-release/changelog" # Plugin documentation: https://github.com/semantic-release/changelog
  - "@semantic-release/github" # Plugin documentation: https://github.com/semantic-release/github
  - "@semantic-release/git" # Plugin documentation: https://github.com/semantic-release/git
```
