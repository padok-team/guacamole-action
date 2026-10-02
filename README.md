# Guacamole-action

This GitHub Action runs [guacamole](https://github.com/padok-team/guacamole) against infrastructure-as-code to identify code smells and bad practices.

It can also report the IaC score of the layers and modules changed by a pull request directly as a PR comment.

## Usage

### IaC score on pull requests

The `ci` check detects the Terragrunt layers and Terraform modules modified by the pull request, runs the matching static checks and posts the score as a pull request comment. The comment is updated in place on each new push, and the report is also written to the job summary.

See [`examples/pull-request-iac-score.yaml`](examples/pull-request-iac-score.yaml). The workflow needs the `pull-requests: write` permission and a checkout with `fetch-depth: 0`.

Set `fail_on_error: true` to make the step fail when at least one check fails.

### Static checks on the whole codebase

See [`examples/static-checks.yaml`](examples/static-checks.yaml).

## Inputs

| Name | Default | Description |
|---|---|---|
| `check_type` | `static` | Guacamole command to run: `static`, `static module`, `static layer`, `state`, `all`, `profile` or `ci` |
| `path` | `.` | Path with infrastructure code to scan (directory containing `layers/`, `base/`, `functional/` or `modules/` for the `ci` check) |
| `verbose` | `false` | Verbose mode |
| `ignorefile` | `.guacamoleignore` | File with patterns to ignore |
| `version` | pinned release | Version of guacamole to install |
| `base_branch` | PR base branch | `ci` only: branch to diff against |
| `scan_all` | `false` | `ci` only: scan every layer/module instead of the ones changed by the pull request |
| `fail_on_error` | `false` | `ci` only: fail the step when at least one check fails |
| `comment` | `true` | `ci` only: post the IaC score as a pull request comment |
| `github_token` | `${{ github.token }}` | `ci` only: token used to post the comment, needs `pull-requests: write` |

## Outputs

Only set by the `ci` check.

| Name | Description |
|---|---|
| `score` | Global IaC score, in percent |
| `passed` | Number of passed checks |
| `total` | Total number of checks |

