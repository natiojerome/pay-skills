---
name: machine-preflight
title: "Machine Preflight API"
description: "Analyze unsigned Base transactions with execution simulation, gas estimates, target bytecode checks, and structured risk findings before signing."
use_case: "Use before approving or signing a Base transaction to detect unlimited approvals, privileged calls, likely reverts, and suspicious target contracts."
category: security
service_url: https://preflight.natio.re
openapi:
  path: openapi.json
---

Machine Preflight API inspects one final unsigned Base transaction without
requesting wallet custody. It checks the target bytecode, performs `eth_call`
and gas estimation, recognizes high-signal approval and administrative call
patterns, and returns a structured report with evidence and limitations.

The service never signs or broadcasts the submitted transaction. Its report is
a technical signal, not investment advice or a replacement for a full audit.

## Spend-aware usage

- Submit the final transaction payload immediately before asking for a signature.
- Make one call per distinct `to`, `data`, `valueWei`, and optional `from` tuple.
- Do not call repeatedly for an unchanged payload unless the relevant on-chain
  state may have changed.
