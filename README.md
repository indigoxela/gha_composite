# Custom composite GitHub Actions

For Backdrop CMS contrib projects.

Note that this isn't the official repository. That's [here](https://github.com/backdrop-ops/gha)

To use such a predefined action you'd create a directory
`.github/workflows/` in your repository and add a yml file (whatever the
name is).

Most below copy-paste examples are the minimal setup (without params) and all run
on pull requests only.
You can use all of them in the same repo, but need a workflow file for each of
them.

## Using "phpcs_full":

`.github/workflows/phpcs.yml`

```yml
name: Coding standards
on: [pull_request]
jobs:
  coding_standards:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - name: Run PHP_CodeSniffer
        uses: indigoxela/gha_composite/actions/phpcs_full@main

```

Available (optional) parameters:

- php_version: defaults to 8.3
- fail_on_warnings: defaults to true

## Using "simpletest":

`.github/workflows/simpletest.yml`

```yml
name: Simpletest
on: [pull_request]
jobs:
  functional_test:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - name: Run Tests
        uses: indigoxela/gha_composite/actions/simpletest@main

```

Available (optional) parameters:

- php_version: defaults to 8.3
- db_version: defaults to mariadb-10.11
- module_dependencies: default empty

### Additional code sample overriding all parameters:

```yml
name: Simpletest
on: [pull_request]
jobs:
  functional_test:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - name: Run Tests
        uses: indigoxela/gha_composite/actions/simpletest@main
        with:
          php_version: "8.5"
          db_version: "mysql-8.0"
          module_dependencies: "entity_plus,entity_ui"

```

### Run Simpletest on multiple PHP versions:

Every PHP version uses its own workflow runner, they start in parallel.

```yml
name: Simpletest
on: [pull_request]
jobs:
  functional_test:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        php-versions: ['7.4', '8.5']
    steps:
      - name: Run Tests
        uses: indigoxela/gha_composite/actions/simpletest@main
        with:
          php_version: ${{ matrix.php-versions }}

```

## Using "phpstan":

`.github/workflows/phpstan.yml`

```yml
name: PHPStan
on: [pull_request]
jobs:
  code_analysis:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - name: Run PHPStan
        uses: indigoxela/gha_composite/actions/phpstan@main

```

Available (optional) parameters:

- php_version: defaults to 8.3
- config_path: by default `phpstan` expects a phpstan.neon file in your repo's
  base directory
- module_dependencies: default empty

You *will* need a phpstan.neon file to make use of this action, its path is
configurable.

## Using "jshint":

`.github/workflows/jshint.yml`

```yml
name: JSHint
on: [pull_request]
jobs:
  js_linter:
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - name: Run JSHint
        uses: indigoxela/gha_composite/actions/jshint@main

```

Available (optional) parameter:

- paths_to_check: defaults to current working directory
