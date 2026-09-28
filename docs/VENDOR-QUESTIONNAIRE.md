# AI Supplier Security Questionnaire

Use this for model providers, hosted execution services, tool integrations and internal platform teams. Ask about the exact service, account tier, region and deployment mode you will use. Request dated documentation or test evidence; distinguish independently assessed facts from provider statements.

| Ask | Evidence to request | Controls |
| --- | --- | --- |
| What data do you receive, store and send to other parties? | Data-flow map covering prompts, files, outputs, telemetry, retries and support | G02–G03, D01–D02 |
| Which settings govern training use, retention and processing locations? | Applicable terms, account settings, exceptions and change notification process | D02, V03 |
| What survives a deletion request or account closure? | Active-store, index, cache, log and backup lifecycle; deletion verification | D05, V04 |
| How are users, service accounts and tenants authorized? | Identity model, scopes, delegated-access behavior and cross-tenant test evidence | K02–K03, A05, D03 |
| Can customer code or an agent read reusable provider or customer credentials? | Secret delivery model, broker permissions, redaction and revocation behavior | K04–K07 |
| What can a fully compromised execution environment reach? | Effective mounts, control sockets, network routes, host interfaces and independent enforcement | I01–I04, N04 |
| How are filesystem boundaries handled across symlinks and resource reuse? | Design review and benign boundary-test results | I05, I07 |
| How is old storage isolated or erased before reassignment? | Allocation/reuse design, snapshot policy, erasure or key lifecycle evidence and assurance scope | V02, I07 |
| Does containment cover helpers, indexing and browser workers? | Process model and tests beyond the command shell | I01 |
| What protects builds, scanners and release credentials? | Build/release separation, dependency controls and artifact provenance | S01–S05 |
| Who patches the host, guest, runtime and plugins? | Responsibility matrix, supported-version policy and remediation process | S07, I06, V03 |
| Can customers stop actions and revoke access independently? | Containment interface, token/session invalidation semantics and drill results | K07, O03–O04 |
| What can we export to investigate an incident? | Event fields, timestamps, retention, integrity/access controls and export process | O01–O02 |
| Which audit or certification actually covers this service? | Current report, independent issuer, scope, dates, exclusions, exceptions and customer responsibilities | V01 |
| How do we leave safely? | Export, credential revocation, connector removal, deletion and fallback procedure | V04 |

## Decision record

- Service and deployment mode:
- Evidence date and reviewer:
- Confirmed capabilities:
- Provider assertions not independently verified:
- Customer responsibilities:
- Gaps and compensating controls:
- Approved scope and conditions:
- Risk owner and next review date:

“Encrypted,” “private,” “local,” “sandboxed” and “certified” each need an implementation-specific explanation. None answers all of the questions above.
