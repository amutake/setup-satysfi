# setup-satysfi

[![ci](https://github.com/amutake/setup-satysfi/actions/workflows/ci.yml/badge.svg)](https://github.com/amutake/setup-satysfi/actions/workflows/ci.yml)

Set up your GitHub Actions workflow with a specific version of SATySFi.

> [!IMPORTANT]
> This is an Action for SATySFi version 0.1.0 and later. Currently, it is only compatible with the `dev-0-1-0-separate-saphe-from-satysfi` branch.

## Usage

### Example workflow for document

```yaml
name: CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: amutake/setup-satysfi@v0
      # optional but recommended:
      - uses: actions/cache@v4
        with:
          path: ~/.saphe
          key: ${{ runner.os }}-saphe-${{ hashFiles('./main.saphe.lock.yaml') }}
          restore-keys: |
            ${{ runner.os }}-saphe-
      - run: saphe update main.saty
      - run: saphe solve main.saty
      - run: saphe build main.saty
      # optional:
      - uses: actions/upload-artifact@v4
        with:
          name: pdf
          path: main.pdf
```

### Example workflow for library

```yaml
name: CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: amutake/setup-satysfi@v0
      # optional but recommended:
      - uses: actions/cache@v4
        with:
          path: ~/.saphe
          key: ${{ runner.os }}-saphe-${{ hashFiles('./saphe.lock.yaml') }}
          restore-keys: |
            ${{ runner.os }}-saphe-
      - run: saphe update .
      - run: saphe solve .
      - run: saphe build .
      - run: saphe test .
```
