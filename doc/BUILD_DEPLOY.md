# Vela-PySDK Build and Deployment

## Purpose and scope

Vela-PySDK packages the `vela-sdk` Python gRPC client for the HalService
endpoint exposed by Vela-Client. The nested `vela-sdk/pyproject.toml` defines
the distribution and dev dependencies; the root Makefile uses `uv` to create a
virtual environment, regenerate generated bindings, test, lint, type-check,
and build distributions.

## 1. Prerequisites

- Python 3.10+ and `uv` on `PATH` (override with `UV=...`).
- Network access for uv dependencies unless the required packages are cached.
- Matching Vela-HAL protobuf contracts and a reachable Vela-Client HalService
  for live examples or interoperability checks; no device is needed for the
  local unit suite.

## 2. Setup

Run `make setup` to create `.venv` and install `vela-sdk[dev]` editable. `make
venv` creates only the environment. The package source and generated output are
under `vela-sdk/`, with generated protobuf files in `src/vela_sdk/_proto`.

## 3. Build and compile

- `make gen` regenerates protobuf and dataclass bindings.
- `make gen-check` fails when committed generated stubs differ; use `make
  gen-clean` for a full clean regeneration.
- `make build` installs the Python `build` helper into the uv environment and
  writes wheel and sdist artifacts to `vela-sdk/dist`.

## 4. Tests and lint

`make test` runs pytest with coverage. `make lint` runs Ruff over the SDK source
and `make typecheck` runs strict mypy with the package configuration. `make
check` combines lint, type-check, and test; `make` defaults to that aggregate.

## 5. Packaging and artifacts

The wheel and source distribution are created under `vela-sdk/dist`. Package
metadata names the distribution `vela-sdk` and the import package `vela_sdk`;
protobuf `.pyi` package data is included. Inspect the generated artifacts before
publishing and keep generated stubs compatible with the server/client proto
contracts.

## 6. Deployment, install, and run

Install a built wheel into a consumer environment with `python -m pip install
vela-sdk/dist/<artifact>`, or keep the editable uv setup for development. `make
shell` opens a uv-activated shell. Use the SDK's examples and HalService client
against a configured Vela-Client endpoint; the endpoint, credentials/TLS, and
target address are application configuration rather than Make variables.

## 7. Cleanup

`make clean` removes SDK build/dist, caches, coverage, egg-info, and Python
cache directories while retaining `.venv`. `make distclean` also removes the
uv environment and install stamps.

## 8. Hardware, cloud, and manual verification caveats

Local tests and wheel creation do not prove generated-stub compatibility,
network/TLS authentication, server version compatibility, or peripheral
availability. A self-test example needs a live Vela-Client, matching HAL
contracts, permissions, and actual hardware; record those results separately
from `make check`.