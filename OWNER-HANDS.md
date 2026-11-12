# OWNER-HANDS — cyan-eclipse-legacy-recon PyPI launch

Everything in this file is done **by the owner, in the owner's
browser**. The package is built and locally proven (wheel + sdist,
clean-venv install, MCP handshake against the installed entry point);
it is **not yet published** — no Trusted Publisher exists for this
project yet.

> **Stop rule:** no step below creates or hands over an API token.
> Publishing runs on Trusted Publishing (OIDC) only.

## Trusted Publisher for `cyan-eclipse-legacy-recon` (pending publisher)

On <https://pypi.org/manage/account/publishing/> → "Add a new pending
publisher" → **GitHub** tab. Enter these strings **exactly**:

| Field | Value |
|---|---|
| PyPI Project Name | `cyan-eclipse-legacy-recon` |
| GitHub Repository Owner | `CYAN-ECLIPSE-TECHNOLOGIES-LLC` |
| GitHub Repository Name | `cyan-eclipse-legacy-recon-mcp` |
| GitHub Workflow Name | `publish-pypi.yml` |
| Environment Name | `pypi` |

## Ship day (after the publisher above exists)

1. Agent verifies `VERSION` + `server.json` agree at the release
   version and the full test suite is green.
2. Owner reviews; agent tags `v<version>` and pushes the tag.
   **Do not tag before the Trusted Publisher exists** — the
   `publish-pypi.yml` workflow fires on `v*` tags and will fail.
3. GitHub Actions then builds, runs `twine check`, and publishes to
   PyPI via Trusted Publishing with PEP 740 attestations.

## Known blocker at packaging time (2026-11-12)

The repo test suite has one pre-existing failure at HEAD, unrelated
to packaging: `tests/test_claim_scope.py::test_manifest_keeps_the_historical_failed_verdict`
still asserts the card -10 FAILED verdict, while `bazaar-manifest.json`
was synced to CERTIFIED(local) / card -11 by the 2026-10-26 Rook
listing pass (commit e6142cd). The `publish-pypi.yml` build job runs
the test suite (house pattern), so this must be reconciled — by
whichever hand owns the manifest/test pair — before a tag can
publish green.
