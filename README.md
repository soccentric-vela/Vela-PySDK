# Vela-PySDK Python SDK leaf for the **Vela** project (Qualcomm QCS6490 + STM32) in the
SiliconCentric `project-managers` fleet. This leaf provides `vela-sdk`, a Pythonic gRPC client for the `HalService`
endpoint exposed by `Vela-Client`. The SDK distribution package is
**`vela-sdk`** (import name `vela_sdk`); a `acadia_sdk` deprecation shim
re-exports the public surface for callers still on the old name. The SDK source, tooling, docs, examples, and test suite live under
[`vela-sdk/`](vela-sdk). See [`vela-sdk/README.md`](vela-sdk/README.md)
for the full API, quickstart, and `make` targets (`setup`, `gen`, `check`,
`build`). ---
Part of the `Vela` project in the `project-managers` fleet. See
`docs/project-managers.md` for the full 9-project/ 8-leaf hierarchy and
shared conventions.

## Project Summary

Vela-PySDK packages the Python client used to call the Vela HAL service. The
distributable package lives under `vela-sdk/`, is published as `vela-sdk`, and
uses `vela_sdk` as its import name. Source includes a client, channel setup,
conversion helpers, exceptions, peripheral abstractions, typed metadata, and
generated gRPC/protobuf modules under `vela-sdk/src/vela_sdk/_proto/`. An
`acadia_sdk` compatibility package remains as a deprecation shim.

The leaf includes API, error-handling, peripheral, quickstart, versioning, and
release documentation, examples including `06_self_test_all.py`, a
`pyproject.toml`, and Make targets. This is a real checked-in SDK surface, but
the inventory does not establish that generated stubs match current server
protos, that all peripheral methods have live implementations, or that the
package has been exercised against a Vela device. The nested
`vela-sdk/README.md` remains the detailed package guide.

The SDK’s generated files are part of the checked-in package contract, but they
are normally derived from protobuf definitions shared with Vela-Client and
Vela-Server. Regeneration and compatibility checks are therefore important
before publishing a release. The examples document intended usage, while a
device-backed self-test is a separate concern from importing the package or
building a wheel. The compatibility shim should remain covered until all
callers migrate from the old import name. Package metadata, typed markers,
documentation, and Make targets support distribution, but none of them alone
prove network credentials, server compatibility, peripheral availability, or
production error handling. Those boundaries are reflected as unknown or
manual-review items below.

## Feature Status

| # | Name / Description | Implemented? | Test Coverage? | Manual Test |
|---:|---|---|---|---|
| 1 | `vela-sdk` distribution metadata | Implemented | Package checks available; results not verified | [ ] Manual verification required |
| 2 | `vela_sdk` client and channel | Implemented | Tooling exists; execution not verified | [ ] Manual verification required |
| 3 | Generated gRPC/protobuf modules and typing stubs | Implemented | Generation/check documented; compatibility unknown | [ ] Manual verification required |
| 4 | Peripheral abstraction and conversion helpers | Implemented | Coverage depth unknown | [ ] Manual verification required |
| 5 | Exceptions and error handling | Implemented | Error coverage not established | [ ] Manual verification required |
| 6 | `acadia_sdk` compatibility shim | Implemented | Shim compatibility unknown | [ ] Manual verification required |
| 7 | API, quickstart, peripheral, and release docs | Implemented | Documentation correctness not automated | [ ] Manual verification required |
| 8 | Self-test example workflow | Implemented | Hardware execution not verified | [ ] Manual verification required |
| 9 | Setup, generation, check, and build targets | Implemented | Command execution not verified | [ ] Manual verification required |
| 10 | Published-package/server interoperability | Unknown | No E2E result established | [ ] Manual verification required |

Use the nested package targets `make setup`, `make gen`, `make check`, and
`make build`; consult `docs/AUDIT.md` and `docs/SDK_FINDINGS.md` for gaps.