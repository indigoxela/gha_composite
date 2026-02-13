# gha_experiments

Experiments re GitHub actions

To use such a predefined action you'd create a directory
`.github/workflows/` in your repository and add a yml file (whatever the
name is).

Example: `.github/workflows/code-checks.yml`

All below copy-paste examples are the minimal setup (without params) and all run
on pull requests only.
You can use all of them in the same repo, but need a workflow file for each of
them.

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

Additional code sample overriding all parameters:

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
        with:
          php_version: "8.5"
          db_version: "mysql-8.0"
          module_dependencies: "entity_plus,entity_ui"
```

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
