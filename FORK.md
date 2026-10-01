# Fork release branch

`release/0.3.4-grepfix` is a fork-only branch of so0k/shell: PR #124 (grep
binary-file fix) plus a Node-only release path (aarch64 linux + macOS addons).
Not for upstream; the workflow refuses to run outside `so0k/shell`.

## Cut a release

Pushing this branch builds and packs both addons (dry run, artifacts on the run).
Pushing a tag releases: attests the three tarballs and creates a prerelease.

    git tag -s v0.3.4-grepfix.1 && git push fork v0.3.4-grepfix.1

## Consume (`npm ci` records sha512 integrity per tarball)

    "dependencies": { "@strands-agents/shell": "https://github.com/so0k/shell/releases/download/v0.3.4-grepfix.1/strands-agents-shell-0.3.4-grepfix.1.tgz" },
    "overrides": {
      "@strands-agents/shell-linux-arm64-gnu": "https://github.com/so0k/shell/releases/download/v0.3.4-grepfix.1/strands-agents-shell-linux-arm64-gnu-0.3.4-grepfix.1.tgz",
      "@strands-agents/shell-darwin-arm64": "https://github.com/so0k/shell/releases/download/v0.3.4-grepfix.1/strands-agents-shell-darwin-arm64-0.3.4-grepfix.1.tgz"
    }

Verify: `gh attestation verify strands-agents-shell-0.3.4-grepfix.1.tgz --repo so0k/shell`
