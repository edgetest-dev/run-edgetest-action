# run-edgetest-action

![example workflow](https://github.com/edgetest-dev/run-edgetest-action/actions/workflows/test-action.yml/badge.svg)

The run edgetest action lets you run [edgetest](https://github.com/capitalone/edgetest) against
your Python library. It will loop through your project's dependencies, and check if your project is compatible with the
latest version of each dependency.

The action assumes the following:

- Your repo is already configured to use `edgetest`.
  - eg: you have a section in your `pyproject.toml` for `edgetest`
- Runs on `ubuntu-latest`, Python `3.10` by default (3.10 through 3.14 supported), and the latest `edgetest`, `edgetest-conda`, and `edgetest-pip-tools`
- Any external setup for your tests to pass, outside the command passed to edgetest, is done
  before the call.

Example of usage:

```yaml
on:
  schedule:
    - cron:  '5 9 * * 1'
jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: running edgetest
    steps:
      - uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1  # v7.0.1
        with:
          ref: dev
      - id: run-edgetest
        uses: edgetest-dev/run-edgetest-action@v1.7
        with:
          edgetest-flags: '-c pyproject.toml -r requirements.txt --export'
          base-branch: 'dev'
          skip-pr: 'false'
          python-version: '3.12'
```

- Typically, you will want to run the action on some cron schedule as its own workflow
- It should use `ubuntu`
- Checkout your repo and point it to your default branch (the one to run `edgetest` against).
  - This branch should have your `edgetest` configuration.
- (Optional) Do any preparation your testing needs (copying config files, setting env vars, etc.) before the call.
- Finally, you can call the `edgetest` action

Options
-------

| option           | desc                                                                                                    | default   | examples                                       |
|------------------|---------------------------------------------------------------------------------------------------------|-----------|------------------------------------------------|
| `edgetest-flags` | options to pass to the `edgetest` call. Everything after `edgetest ....`                                | `""`      | `'-c pyproject.toml -r requirements.txt --export' ` |
| `base-branch`    | the branch which you want to PR against if there are changes. This is typically your development branch | `'dev'`   | `'develop'  `                                  |
| `skip-pr`        | skips the action submitting a PR if there are any changes. Accepts the strings `'true'` or `'false'`.   | `'false'` | `'true'` or `'false'`                          |
| `python-version` | Python version to use (from "setup-miniconda"). Must be 3.10 or newer (`edgetest` requires it).         | `'3.10'`  | `'3.10'`, `'3.11'`, `'3.12'`, `'3.13'`, `'3.14'` |
| `add-paths`      | A comma separated list of file paths to commit.  (from "peter-evans/create-pull-request").              | `'*'`     | `'requirements.txt, pyproject.toml'`           |

Action Dependencies
-------------------

Uses:
 - [conda-incubator/setup-miniconda@v4.1.0](https://github.com/conda-incubator/setup-miniconda)
 - [peter-evans/create-pull-request@v8.1.1](https://github.com/peter-evans/create-pull-request)

Both are pinned to commit SHAs in `action.yml`. These action majors run on Node 24,
which requires Actions Runner v2.327.1 or later on self-hosted runners.
GitHub-hosted `ubuntu-latest` is unaffected.

Contributing
------------

See our [developer documentation](CONTRIBUTING.md).

License
-------
MIT
