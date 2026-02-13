# gha_experiments

Experiments re GitHub actions

## Using "phpcs_full":

```yml
name: Coding standards
on: [pull_request]
jobs:
  coding_standards:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - name: Run PHP_CodeSniffer
        uses: indigoxela/gha_experiments/actions/phpcs_full@main
```

Available (optional) parameters:

- php_version: defaults to 8.3
- fail_on_warnings: defaults to true

## Using "simpletest":

```yml
name: Simpletest
on: [pull_request]
jobs:
  functional_test:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - name: Run Tests
        uses: indigoxela/gha_experiments/actions/simpletest@main
```

Available (optional) parameters:

- php_version: defaults to 8.3
- db_version: defaults to mariadb-10.11
- module_dependencies: default empty

## Using "phpstan":

```yml
name: PHPStan
on: [pull_request]
jobs:
  code_analysis:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - name: Run PHPStan
        uses: indigoxela/gha_experiments/actions/phpstan@main
```

Available (optional) parameters:

- php_version: defaults to 8.3
- config_path: by default `phpstan` expects a phpstan.neon file in your repo's
  base directory
- module_dependencies: default empty

You *will* need a phpstan.neon file to make use of this action, its path is
configurable.
