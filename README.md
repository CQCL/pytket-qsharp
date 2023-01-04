# Pytket Extensions

This repository contains the pytket-qsharp extension, using Quantinuum's
[pytket](https://cqcl.github.io/tket/pytket/api/index.html) quantum SDK.

# pytket-qsharp

[Pytket](https://cqcl.github.io/tket/pytket/api/index.html) is a python module for interfacing
with tket, a quantum computing toolkit and optimisation compiler developed by Quantinuum.

[Azure Quantum](https://azure.microsoft.com/en-gb/services/quantum/) is a portal for accessing
quantum computers via Microsoft Azure.

Microsoft's [QDK](https://docs.microsoft.com/en-us/quantum/install-guide) is a
language and associated toolkit for quantum programming.

`pytket-qsharp` is an extension to `pytket` that allows `pytket` circuits to be
executed on remote devices and simulators via Azure Quantum,
as well as local simulators and resource estimators from the Microsoft QDK.

## Backends provided in this module

This module provides four
[backends](https://cqcl.github.io/tket/pytket/api/backends.html), all deriving
from the `pytket` `Backend` class:

* `AzureBackend`, for executing pytket circuits on targets the user has access to on Azure Quantum;

* `QsharpSimulatorBackend`, for simulating a general pure-quantum circuit using
the QDK;

* `QsharpToffoliSimulatorBackend`, for simulating a Toffoli circuit using the
QDK;

* `QsharpEstimatorBackend`, for estimating various quantum resources of a
circuit using the QDK. This provides a `get_resources` method, which returns a
dictionary.

## Getting started

`pytket-qsharp` is available for Python 3.9, 3.10 and 3.11, on Linux, MacOS
and Windows. To install, run:

```pip install pytket-qsharp```

This will install `pytket` if it isn't already installed, and add new classes
and methods into the `pytket.extensions` namespace.

In order to use `pytket-qsharp` you will first need to install the `dotnet` SDK
(6.0) and the `iqsharp` tool. On some Linux systems it is also necessary to
modify your `PATH`:

1. See [this page](https://dotnet.microsoft.com/download/dotnet-core/6.0) for
instructions on installing the SDK on your operating system.

2. On Linux, ensure that the `dotnet` tools directory is on your path. Typically
this will be `~/.dotnet/tools`.

3. Run `dotnet tool install -g Microsoft.Quantum.IQSharp`.

4. Run `dotnet iqsharp install --user`.


Alternatively, you can set up an environment with all the required packages using conda:

```
conda create -n qsharp-env -c quantum-engineering qsharp notebook

conda activate qsharp-env
```

## Bugs, support and feature requests

Please file bugs and feature requests on the Github
[issue tracker](https://github.com/CQCL/pytket-qsharp/issues).

There is also a Slack channel for discussion and support. Click [here](https://tketusers.slack.com/join/shared_invite/zt-18qmsamj9-UqQFVdkRzxnXCcKtcarLRA#/shared-invite/email) to join.

## Development

To install an extension in editable mode, simply change to its subdirectory
within the `modules` directory, and run:

```shell
pip install -e .
```

## Contributing

Pull requests are welcome. To make a PR, first fork the repo, make your proposed
changes on the `develop` branch, and open a PR from your fork. If it passes
tests and is accepted after review, it will be merged in.

### Code style

#### Formatting

All code should be formatted using
[black](https://black.readthedocs.io/en/stable/), with default options. This is
checked on the CI. The CI is currently using version 20.8b1.

#### Type annotation

On the CI, [mypy](https://mypy.readthedocs.io/en/stable/) is used as a static
type checker and all submissions must pass its checks. You should therefore run
`mypy` locally on any changed files before submitting a PR. Because of the way
extension modules embed themselves into the `pytket` namespace this is a little
complicated, but it should be sufficient to run the script `modules/mypy-check`
(passing as a single argument the root directory of the module to test). The
script requires `mypy` 0.800 or above.

#### Linting

We use [pylint](https://pypi.org/project/pylint/) on the CI to check compliance
with a set of style requirements (listed in `.pylintrc`). You should run
`pylint` over any changed files before submitting a PR, to catch any issues.

### Tests

To run the tests for a module:

1. `cd` into that module's `tests` directory;
2. ensure you have installed `pytest`, `hypothesis`, and any modules listed in
the `test-requirements.txt` file (all via `pip`);
3. run `pytest`.

When adding a new feature, please add a test for it. When fixing a bug, please
add a test that demonstrates the fix.
