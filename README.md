<p align="center">
  <h1 align="center">jason-idk/gh-actions</h1>
  <p align="center">
    A collection of composite actions and reusable workflows.
    <br>
    <a href="https://github.com/jason-idk/gh-actions/issues/new?template=bug.md">Report bug</a>
    ·
    <a href="https://github.com/jason-idk/gh-actions/issues/new?template=feature.md&labels=feature">Request feature</a>
  </p>
</p>

![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/jason-idk/gh-actions/ci.yml)
![GitHub License](https://img.shields.io/github/license/jason-idk/gh-actions?color=yellow)
[![GitHub Contributors](https://img.shields.io/github/contributors/jason-idk/gh-actions.svg?style=flat)]()
![GitHub Tag](https://img.shields.io/github/v/tag/jason-idk/gh-actions)


## Table of contents

- [Quick start](#quick-start)
- [Status](#status)
- [What's included](#whats-included)
- [Bugs and feature requests](#bugs-and-feature-requests)
- [Contributing](#contributing)
- [Thanks](#thanks)
- [Copyright and license](#copyright-and-license)


## Quick start

To begin using the composite actions and reusable workflows found in this repository, simply reference them in your GitHub Workflow accordingly. Read the upstream documentation on using a [composite action](https://docs.github.com/en/actions/sharing-automations/creating-actions/creating-a-composite-action#testing-out-your-action-in-a-workflow) or [reusable workflow](https://docs.github.com/en/actions/sharing-automations/reusing-workflows#calling-a-reusable-workflow).

Example of using a reusable workflow:
```yaml
name: Reusable Workflow Example

on:
  push:

jobs:
  call-workflow-passing-data:
    uses: jason-idk/gh-actions/.github/workflows/reusable-workflow.yml@v1
    with:
      config-path: .github/extra.yml
    secrets:
      personal_access_token: ${{ secrets.token }}
```

Example of using a composite action:
```yaml
name: CI

on:
  push:

  pull_request:
    branches: [ "main" ]

concurrency:
  group: ${{ github.ref }}-${{ github.workflow }}
  cancel-in-progress: true

jobs:
  ci:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: YAML Lint and Shellcheck
        uses: jason-idk/gh-actions/.github/actions/gha-linter@v1

      - name: Semantic versioning
        uses: jason-idk/gh-actions/.github/actions/semantic-versioning@v1
        with:
          main_branch: main
```

## Status

Actively maintained. If you are interested in adding additional workflows or actions, please open a PR! :alien:

I will continue to add new features and address bugs or hotfixes as needed. Make sure to open a bug report or issue.

## What's included

The folder structure looks as follows:

```text
.github/
└── actions/
|   ├── action0/
|   │   ├── action.yml
|   │   └── script.sh
|   └── action1/
|       └── action.yml
└── workflows/
    ├── reusable-workflow0.yml
    └── reusable-workflow1.yml
```
To understand the differences between reusable workflows and composite actions, refer to the following [documentation](https://docs.github.com/en/actions/sharing-automations/reusing-workflows). 

## Bugs and feature requests

Have a bug or a feature request? Please first read the (***to be added***) [issue guidelines](https://github.com/jason-idk/gh-actions/blob/main/CONTRIBUTING.md) and search for existing and closed issues. If your problem or idea is not addressed yet, [please open a new issue](https://github.com/jason-idk/gh-actions/issues/new).

## Contributing

Please read through the (***to be added***) [contributing guidelines](https://github.com/jason-idk/gh-actions/blob/main/CONTRIBUTING.md). Included are directions for opening issues, coding standards, and notes on development.

## Thanks

Thanks for stopping by, if you find the actions in this repository useful, consider dropping a star :star: and sharing! 

## Copyright and license

Code and documentation copyright 2011-2025 the authors. Code released under the [MIT License](https://github.com/jason-idk/gh-actions/blob/main/LICENSE).

Enjoy :metal:
