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

An additional tool to install is [`pre-commit`](https://pre-commit.com/), for automating formatting and style checks when you commit files. Install `pre-commit` globally once:

```shell
uv tool install --with pre-commit-uv pre-commit
```

and install the hooks in this repository once to let them one automatically run before each commit:

```shell
pre-commit install --install-hooks
```

## Editing notebooks

Notebooks that are served on [rub-ep1.github.io/lite](https://rub-ep1.github.io/lite) are located under the [`content/`](./content/) directory. Add and modify them as you like with Jupyter Lab:

```shell
jupyter lab content/
```

To test what the web-based JupyterLite server will look like, run:

```shell
jupyter lite serve --contents content --output-dir dist
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
