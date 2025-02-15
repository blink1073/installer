# Workflow

This page describes the tooling used during development of this
project. It also serves as a reference for the various commands that
you would use when working on this project.

## Overview

This project uses the [GitHub Flow] for collaboration. The codebase
is Python.

- [flit] is used for automating development tasks.
- [nox] is used for automating development tasks.
- [pre-commit] is used for running the linters.
- [sphinx] is used for generating this documentation.
- [pytest] is used for running the automated tests.

## Repository Layout

The repository layout is pretty standard for a modern pure-Python
project.

- `CODE_OF_CONDUCT.md`
- `LICENSE`
- `README.md`
- `.nox/` -- Generated by [nox].
- `dist/` -- Generated as part of the release process.
- `docs/` -- Sources for the documentation.
- `src/`
  - `installer/` -- Actual source code for the package
- `tests/` -- Automated tests for the package.
- `noxfile.py` -- for [nox].
- `pyproject.toml` -- for packaging and tooling configuration.

## Initial Setup

To work on this project, you need to have git 2.17+ and Python 3.7+.

- Clone this project using git:

  ```sh
  git clone https://github.com/pradyunsg/installer.git
  cd installer
  ```

- Install the project's main development dependencies:

  ```sh
  pip install nox
  ```

You're all set for working on this project.

## Commands

### Code Linting

```sh
nox -s lint
```

Run the linters, as configured with [pre-commit].

### Testing

```sh
nox -s test
```

Run the tests against all supported Python versions, if an interpreter for
that version is available locally.

```sh
nox -s test-3.9
```

Run the tests against Python 3.9. It is also possible to specify other
supported Python versions (like `3.7` or `pypy3`).

### Documentation

```sh
nox -s docs
```

Generate the documentation for installer into the `build/docs` folder.
This (mostly) does the same thing as `nox -s docs-live`, except it
invokes `sphinx-build` instead of [sphinx-autobuild].

```sh
nox -s docs-live
```

Serve this project's documentation locally, using [sphinx-autobuild].
This will open the generated documentation page in your browser.

The server also watches for changes made to the documentation (`docs/`),
which will trigger a rebuild. Once the build is completed, server will
automagically reload any open pages using livereload.

## Release process

- Update the changelog.
- Update the version number in `__init__.py`.
- Commit these changes.
- Create a signed git tag.
- Run `flit publish`.
- Update the version number in `__init__.py`.
- Commit these changes.
- Push tag and commits.

[github flow]: https://guides.github.com/introduction/flow/
[flit]: https://flit.readthedocs.io/en/stable/
[nox]: https://nox.readthedocs.io/en/stable/
[pytest]: https://docs.pytest.org/en/stable/
[sphinx]: https://www.sphinx-doc.org/en/master/
[sphinx-autobuild]: https://github.com/executablebooks/sphinx-autobuild
[pre-commit]: https://pre-commit.com/
