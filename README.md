# gha_experiments

Experiments re GitHub actions

Using it:

```
name: Coding standards
on: [pull_request]
jobs:
  coding_standards:
    name: "phpcs remote action"
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - uses: indigoxela/gha_experiments/actions/phpcs_full@main
        with:
          php_version: "8.5"
          fail_on_warnings: false
```

Default php version: 8.3
Defaults to fail on warnings
