# Contributing

## Source code and virtual environment

For contributing to the website (especially adding notebooks), you need to clone this repository

```shell
git clone https://github.com/RUB-EP1/lite
```

and install the **[`uv`](https://docs.astral.sh/uv/)** package manager for Python:

```shell
curl -LsSf https://astral.sh/uv/install.sh | sh
```

That allows you to create a pinned virtual environment with Jupyter Lab for local development, Jupyter Lite for testing the website deployment, and additional development tools for writing the notebooks. To update and activate the environment, run:

```shell
uv sync
source .venv/bin/activate
```

Note that you don't _have_ to activate virtual environment. You can also run the commands directly by prepending `uv run` before them.

Formatting and linting checks are automatically performed when committing changes. This is done with [pre-commit](https://pre-commit.com). To install the hooks in your local repository, run install `pre-commit` with `uv`:

```shell
uv tool install pre-commit --with pre-commit-uv --force-reinstall
```

and [`pre-commit install`](https://pre-commit.com/#3-install-the-git-hook-scripts) **once**:

```shell
pre-commit install --install-hooks
```

[Poe the Poet](https://poethepoet.natn.io) is used as a task runner. It can also be installed with `uv`:

```shell
uv tool install poethepoet
```

You can see which local CI checks it defines by running

```shell
poe
```

For instance, all style checks can be run with

```shell
poe style
```

## Editing notebooks

Notebooks that are served on [rub-ep1.github.io/lite](https://rub-ep1.github.io/lite) are located under the [`content/`](./content/) directory. Add and modify them as you like with Jupyter Lab:

```shell
poe lab
```

To test what the web-based JupyterLite server will look like, run:

```shell
poe doclive
```

> [!TIP]
> To mimic the [GitHub deployment workflow](./.github/workflows/deploy.yml) workflow with exactly the same dependencies, prepend `uv run` with the correct group (i.e. no developer dependencies):
>
> ```shell
> uv run --no-dev jupyter lite serve --contents content --output-dir dist
> ```

## Adding notebook dependencies

The JupyterLite page uses [`jupyterlite-pyodide-kernel`](https://github.com/jupyterlite/pyodide-kernel) to run Python natively in the browser. A Pyodide kernel [hosts a number of Python packages](https://pyodide.org/en/stable/usage/packages-in-pyodide.html), but you have to install any additional packages you need in a cell in the notebook, for instance:

<!-- cspell:ignore ipympl -->

```ipython
%pip install ipympl
```

Note that [only packages with pure-Python wheels](https://pyodide.org/en/stable/usage/loading-packages.html#installing-packages) are supported.
