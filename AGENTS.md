# Repository Guidelines

## Project Structure & Module Organization
This repository is a rule and configuration set for OpenClash/Mihomo, not an application codebase. The root directory contains:

- `config.yaml`: main runtime configuration, including `proxy-providers`, DNS, `proxy-groups`, and `rules`.
- `*.list`: custom rule lists such as `AI.list`, `Direct.list`, `ProxyLite.list`, `cursor_proxy.list`, `zhi_proxy.list`, and `custom_proxy.list`.
- `oprules.ini` and `oprules1.ini`: rule generator presets referencing this repository’s raw files and third-party rule sources.

Keep related changes together. For example, if a new domain is routed through a dedicated group, update both the relevant `*.list` file and any matching entry in `config.yaml` or `oprules.ini`.

## Build, Test, and Development Commands
There is no `package.json`, build pipeline, or bundled test runner. Use lightweight local checks instead:

- `git diff --stat`: review the scope of your changes before commit.
- `git diff`: inspect exact rule or YAML edits.
- `grep -n "DOMAIN-KEYWORD,example" *.list`: confirm duplicates or conflicting entries.
- `mihomo -t -f config.yaml`: validate YAML and Clash/Mihomo semantics if `mihomo` is installed locally.

## Coding Style & Naming Conventions
Use 2-space indentation in YAML and preserve existing key order where practical. In `*.list` and `.ini` files, keep one rule per line and group entries by purpose with short Chinese comments when needed. Prefer uppercase rule types such as `DOMAIN-SUFFIX`, `DOMAIN-KEYWORD`, and `IP-CIDR`. File names use lowercase with underscores, for example `custom_proxy.list`.

## Testing Guidelines
No automated coverage threshold exists today. Validation is change-focused:

- check for duplicate or contradictory rules across `Direct.list`, `ProxyLite.list`, and custom proxy lists;
- verify new domains are routed to the intended policy group;
- run `mihomo -t -f config.yaml` when available.

When changing routing behavior, include at least one concrete example domain or IP in the PR description.

## Commit & Pull Request Guidelines
Recent history uses imperative, descriptive commit messages such as `Add DOMAIN-KEYWORD entry for cubence to zhi_proxy.list` and `Remove DOMAIN-KEYWORD entry for alimama from zhi_proxy.list`. Follow the same pattern: start with `Add`, `Remove`, `Update`, or `Comment out`, then name the affected file and reason.

Pull requests should include:

- a short summary of the routing intent;
- the files changed;
- sample domains, keywords, or CIDRs affected;
- screenshots only if the change impacts OpenClash UI-facing configuration behavior.

## Security & Configuration Tips
Do not commit live subscription URLs, secrets, or personal endpoints in `config.yaml`. Keep provider `url` fields blank or sanitized unless the repository explicitly intends to publish them.
