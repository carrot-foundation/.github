# .github

Organization default community health files and reusable workflows for `carrot-foundation`.

GitHub applies the community health files in this repository to every repository in the organization that does not
define its own. GitHub reads these defaults only from a public `.github` repository, so this
repository is public by design. Keep anything sensitive out of it.

## Files

| File | Purpose |
| --- | --- |
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | Default pull request body: a summary, a test plan, the ClickUp task link and a closing keyword. |
| [`.github/workflows/repo-agent-config.yml`](.github/workflows/repo-agent-config.yml) | Reusable audit of a repository’s agent configuration. |

## Calling the agent configuration audit

Add this job to a workflow in the calling repository. Replace `<sha>` with the full commit SHA that contains the reusable workflow. Configure `LORIEN_READ_TOKEN` as an Actions secret with read access to the verifier repository.

```yaml
jobs:
  repo-agent-config:
    permissions:
      contents: read
    uses: carrot-foundation/.github/.github/workflows/repo-agent-config.yml@<sha>
    secrets:
      lorien-read-token: ${{ secrets.LORIEN_READ_TOKEN }}
```

## Overriding a default

A repository that keeps its own file of the same type, for example its own pull request template,
uses that file instead of the default here. To change the shared default, edit it in this repository.
