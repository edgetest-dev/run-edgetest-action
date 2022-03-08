# run-edgetest-action

![example workflow](https://github.com/fdosani/run-edgetest-action/actions/workflows/test-action.yml/badge.svg)

The run edgetest action lets you run [edgetest](https://github.com/capitalone/edgetest) against
your Python libray. It will loop through your project's dependencies, and check if your project is compatible with the 
latest version of each dependency.

The action assumes the following:

- Your repo is already configured to use `edgetest`.
  - eg: you have a section in your `setup.cfg` for `edgetest`
- runs on `ubuntu-latest`, Python `3.9.x`, and the latest `edgetest`, `edgetest-conda`, and `edgetest-pip-tools`
- any external setup for your tests to pass outside the command passed to edgetest is done
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
      - uses: actions/checkout@v2
        with:
          ref: develop
      - name: Copy files for locopy
        id: copy-files
        run: |
          cp tests/data/.locopyrc ~/.locopyrc
          cp tests/data/.locopy-sfrc ~/.locopy-sfrc
      - id: run-edgetest
        uses: fdosani/run-edgetest-action@v1.1
        with:
          edgetest-flags: '-c setup.cfg -r requirements.txt --export'
          base-branch: 'develop'
          skip-pr: 'false'
```

- Typically, you will want to run the action on some cron schedule as its own workflow
- It should use `ubuntu`
- Checkout your repo and point it to your default branch (the one to run `edgetest` against).
  - This branch should have your `edgetest` configuration.
- (Optional) Do any preparation for your testing or other housekeeping. In this example we needed to copy some file to the home 
  directory for our testing to work. 
- Finally, you can call the `edgetest` action


Options
-------

| option           | desc                                                                                                     | default | examples                                       |
|------------------|----------------------------------------------------------------------------------------------------------|---------|------------------------------------------------|
| `edgetest-flags` | options to pass to the `edgetest` call. Everything after `edgetest ....`                                 | `""`    | `'-c setup.cfg -r requirements.txt --export' ` |
| `base-branch`    | the branch which you want to PR against if there are changes. This is typically your development branch  | `'dev'` | `'develop'  `                                  |
| `skip-pr`        | skips the action summiting a PR if there are any changes.                                                |         | `'true'` or `'false'`                          |



Action Dependencies
-------------------

Uses:
 - [conda-incubator/setup-miniconda@v2](https://github.com/conda-incubator/setup-miniconda)
 - [peter-evans/create-pull-request@v3](https://github.com/peter-evans/create-pull-request)


Contributing
------------

See our [developer documentation](CONTRIBUTING.md).



License
-------
MIT
