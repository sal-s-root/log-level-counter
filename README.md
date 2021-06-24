# log-level-counter

Count explicit severity tokens in text logs.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "log": "INFO started\nERROR unavailable\nplain line"
}
```

Result:

```json
{
  "counts": {
    "DEBUG": 0,
    "INFO": 1,
    "WARN": 0,
    "ERROR": 1,
    "FATAL": 0
  },
  "unclassified": 1
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Matches the first uppercase token; structured logging avoids ambiguous text classification.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [service-port-inventory](https://github.com/sal-s-root/service-port-inventory), [environment-variable-auditor](https://github.com/sal-s-root/environment-variable-auditor).
