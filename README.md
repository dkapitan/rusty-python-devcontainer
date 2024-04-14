# My new stack: a Rusty Python devcontainer

## Using devcontainers optimized for data science & -engineering

The [VS Code Dev Containers extension](https://code.visualstudio.com/docs/devcontainers/containers) lets you use a container as a full-featured development environment. It allows you to open any folder inside (or mounted into) a container and take advantage of the full feature set of VS Code. It is an alternative to using Python virtual environments, with the benefit that you can customize the whole runtime. This is particularly useful when dealing with alternative chipsets, such as ARM64/Apple M-series, and managing dependencies for using GPUs.

We use the pre-configured [Data Science Devcontainers](https://github.com/b-data/data-science-devcontainers), which have already taken care of optimizing the whole setup of the devcontainer. To start using them, do the following:

- Install and run Docker
- Clone the repo and open it in VS Code. A pop-up should appear asking whether you want to open the folder in the devcontainer

Note that data is persisted in the container as follows:
  - When using an unmodified devcontainer.json: work in `/home/vscode` which is the `home` directory of user `vscode`
  - Python packages are installed to the home directory by default. This is due to env variable `PIP_USER=1`
  - Note that the directory `/workspaces` is also persisted

### Making changes to the devcontainer

You can change the setup of the devcontainer in the following layers:

- Change (one of) the `Dockerfile`(s): do this is you need to optimize the basic container runtime
- Change `devcontainer.json`: use this to
  - Specify which VS Code extensions you want
  - Specify which apt-packages you need (useful for experimenting without changing the Dockerfile), for example adding `default-jdk` to be able to run pyspark
- Change `/workspaces/rusty-python/.devcontainer/scripts/usr/local/bin/onCreateCommand.sh`: add any other stuff, such as customizing the shell or installing a `requirements.txt`

## Rusty Python for data science & AI

We love the Rustification of Python because it improves the development with tools such as
-   [Ruff](https://docs.astral.sh/ruff/) for linting and code formatting
-   [uv](https://github.com/astral-sh/uv) as a drop-in replacement for `pip`
-   [rye](https://github.com/astral-sh/rye) as a comprehensive project and package management solution for Python
-   [pixi](https://prefix.dev/) as fast software package manager built on top of the existing conda ecosystem

For data science & AI, we enjoy significant performance gains with
- [polars](https://pola.rs/) to handle DataFrames in the new era, and writing plugins in Rust is [not that hard](https://marcogorelli.github.io/polars-plugins-tutorial/)
- [pydantic](https://docs.pydantic.dev/latest/) for data validation
- [tokenizers](https://github.com/huggingface/tokenizers) by Huggingface, that provides an implementation of today's most used tokenizers, with a focus on performance and versatility
- [VegaFusion](https://vegafusion.io/index.html) provides serverside scaling for the Vega visualization library, including the Altair Python interface to Vega-Lite
- [Robyn](https://robyn.tech/), a web framework that can be used to build async APIs
