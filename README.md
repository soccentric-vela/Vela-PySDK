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