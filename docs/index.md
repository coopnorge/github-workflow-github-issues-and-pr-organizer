# GitHub-workflows-GitHub-issues-and-pr-organizer

## Goals

The goal of this workflow is allow teams to automatically move issues and pull
request and issues from individual repos to a single project board.

## Usage

### Inputs

```yaml
inputs:
   incoming_column:
      required: true
      type: string
      description: The name of the column you want a created issue to go to
   done_column:
      required: true
      type: string
      description: The name of the column you want a closed issue to go to
   project_id:
      required: true
      type: number
      description: The number of the project with the board you want to move issues to
secrets:
   gh_app_secret_key:
   required: true
```

### Workflow

Add this job to your workflow:

```yaml
on:
  issues:
    types:
      - opened
      - reopened
      - closed
jobs:
   handle-issues:
      uses: coopnorge/github-workflow-github-issues-and-pr-organizer/.github/workflows/reusable-handle-issues-workflow.yaml@v1
      permissions:
        issues: write
        contents: read
        projects: write
      with:
         incoming_column: <Name of the column in your project board you want opened issues to end up in here>
         done_column: <Name of the column in your project board you want closed issues to end up in here>
         project_id: <Number of your project here>
      secrets:
         gh_app_secret_key: ${{ secrets.PROJECTS_UPDATE_APP_PEM }}
```
