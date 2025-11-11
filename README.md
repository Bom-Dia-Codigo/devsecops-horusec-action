# Horusec Action

[Horusec](https://horusec.io/) is a [SAST](https://en.wikipedia.org/wiki/Static_application_security_testing) great DevSecOps tool to use for any pipeline. This is a proof of concept to embed in a Github Action.

## How to use

This action is now a simple composite action that installs the Horusec CLI on the runner (no Docker build required) and immediately executes `horusec start`.

- `path` (default `./`): forwarded to `horusec start -p`.
- `arguments` (optional): any extra flags you would normally pass to `horusec start` (e.g. `--log-level=debug`, `--custom-rules-path=horusec-config.json`, `--ignore=...`).

Example workflow:

```yml
on: [push]

jobs:
  checking_code:
    runs-on: ubuntu-latest
    name: Horusec Scan
    steps:
      - uses: actions/checkout@v4
      - name: Run Horusec
        uses: Bom-Dia-Codigo/devsecops-horusec-action@v0.2.5
        with:
          path: ./  # optional, defaults to ./ already
          arguments: --log-level=debug --custom-rules-path=horusec-config.json
```

If you prefer to manage everything through a Horusec config file, generate it locally first:

```bash
horusec generate
```

Then commit the config and pass it through `arguments`, for example:

```yml
with:
  arguments: --config-file-path=horusec-config.json
```

## Known Issue

Build Action based Docker purely isn't flexible to split arguments like it's possible when build using Javascript/Typescript.

This is a proof of concept to running Horusec as a Github Action.

This is a fork of fike/horusec-action, this fork and changes were made for didatic and integrity purposes.
Thanks Fike, counts on me :)
