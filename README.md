# openclash

## Private subscription handling

This repository is public. Do not commit real subscription URLs under `proxy-providers`.

- Keep `config.yaml` as the public template and leave every `proxy-providers.*.url` empty or sanitized.
- Put real subscriptions only in ignored local files such as `config.local.yaml` or `config.private.yaml`.
- Existing local working copies with private subscriptions are ignored by `.gitignore`.

## Recommended workflow

1. Copy `config.yaml` to a local private file.
2. Fill in the real `proxy-providers` subscription URLs only in that local file.
3. Before `git add .`, run `git status --short` and confirm no private config is staged.

## If a subscription was already committed

If a real subscription URL has ever been pushed to a public commit, assume it is leaked:

1. Rotate or regenerate the subscription/token first.
2. Rewrite Git history to remove the old URL.
3. Force-push the cleaned history.

Ignoring files now only prevents future leaks. It does not erase existing public history.
