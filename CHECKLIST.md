# AI Security Deployment Checklist

**FutureProof Agents · Version 1.0.0 · Reviewed September 28, 2026**

A practical review for cloud AI, self-hosted models, coding assistants, autonomous agents and retrieval systems. Apply the controls to the complete workflow, including software installation and background processes.

## How to assess

Select the relevant profiles: **cloud**, **self-hosted**, **agents**, and **rag**. Controls tagged **all** apply to every profile; otherwise apply a control when any selected profile matches. More than one profile usually applies. A managed service can satisfy a control through documented provider evidence rather than a customer-operated setting.

**P0** means a launch gate for the applicable scope. **P1** means required hardening with an owner and deadline; it can become a launch gate when exposure or business impact warrants it. These priorities are this checklist's planning convention, not vulnerability scores or regulatory classifications.

Use **Pass / Fail / Unknown / Not applicable / Exception**. Mark a checkbox only when the control passes with evidence. An exception is documented risk acceptance, not a pass. Not applicable needs a reason. Unknown means the work is unfinished.

For each control, record an actual owner, evidence reference, tested version/configuration, test date and next review date in the [assessment template](templates/assessment.md). Suggested owners below are roles to assign, not completed assignments. Store completed assessments and detailed findings privately.

**Release decision:** all applicable P0 controls must pass or have explicit, time-limited approval from the accountable risk owner with compensating controls. Any P0 failure or unknown without that approval blocks the reviewed scope. Track P1 findings with dates. Do not replace this decision with an average percentage.

Verification should use staging, disposable identities and synthetic data under your authority. These checks are acceptance criteria, not instructions to reproduce vulnerabilities on third-party systems.


## Ownership and scope

### G01 · Name the accountable owner

- [ ] **P0 · all** — Assign a business owner and a technical owner for each AI workflow, including experiments that access company data.

**Verify:** Select a running workflow and confirm who can stop it and who accepts its residual risk.

**Evidence:** Approved ownership record and escalation contact.  
**Suggested owner:** Business owner

### G02 · Inventory the complete workflow

- [ ] **P0 · all** — Record models, gateways, tools, plugins, MCP servers, storage, dependencies, identities, data sources and execution locations.

**Verify:** Trace one real request from user input to output and every external action; compare it with the inventory.

**Evidence:** Dated inventory and data-flow diagram.  
**Suggested owner:** Technical owner

### G03 · Classify data before connecting it

- [ ] **P0 · all** — Define which data classes may enter each model, connector, index, browser session and log destination.

**Verify:** Use synthetic examples of allowed and prohibited data and verify the documented handling decision.

**Evidence:** Data classification matrix and approved use cases.  
**Suggested owner:** Data owner

### G04 · Document trust boundaries

- [ ] **P0 · all** — Identify where untrusted content, executable code or a different user or tenant crosses into a more privileged component.

**Verify:** Walk through a malicious document, compromised package and stolen token; identify the enforced boundary for each.

**Evidence:** Threat model with controls and unresolved risks.  
**Suggested owner:** Security lead

### G05 · Make approved AI easy to use

- [ ] **P1 · all** — Maintain approved tools and a clear process for requesting new tools, reporting accidental uploads and retiring unused integrations.

**Verify:** Ask a team member to find the policy and report a synthetic accidental upload without using a public channel.

**Evidence:** Approved-tools list, onboarding record and reporting procedure.  
**Suggested owner:** IT owner

### G06 · Reassess meaningful changes

- [ ] **P1 · all** — Require review when adding a data source, tool, model, privilege, network route or execution backend; give exceptions an expiry.

**Verify:** Review the last material change and confirm its tests and risk acceptance; find any expired exceptions.

**Evidence:** Change record and dated exception register.  
**Suggested owner:** Technical owner

## Credentials and identity

### K01 · Inventory credentials without collecting their values

- [ ] **P0 · all** — Record each credential's owner, purpose, scope, storage location, consumers, expiry and revocation method.

**Verify:** Sample one credential per integration and follow its lifecycle without printing its value.

**Evidence:** Redacted credential register.  
**Suggested owner:** Identity owner

### K02 · Separate identities and environments

- [ ] **P0 · all** — Use distinct service identities for development, staging, production, workloads and tenants where their access must differ.

**Verify:** Try a staging identity against a production test resource; confirm denial and absence of shared administrator keys.

**Evidence:** Permission matrix and redacted denial event.  
**Suggested owner:** Identity owner

### K03 · Limit credential scope and lifetime

- [ ] **P0 · all** — Prefer workload identity and short-lived credentials; constrain resources and operations, and justify any long-lived key.

**Verify:** Attempt an out-of-scope operation with a test identity and verify expiry or revocation terminates access.

**Evidence:** Policy, token lifetime and test results.  
**Suggested owner:** Identity owner

### K04 · Keep secrets out of published and retained content

- [ ] **P0 · all** — Exclude credentials from prompts, repositories, image layers, build output, traces, shell history and assessment evidence.

**Verify:** Scan a synthetic test fixture through the actual build and logging paths; verify findings and redaction without using live keys.

**Evidence:** Scan results and sanitized logging samples.  
**Suggested owner:** Platform owner

### K05 · Keep reusable secrets outside agent execution

- [ ] **P0 · agents** — Use a trusted tool service or credential broker when possible. An environment variable or mounted secret is readable by code with sufficient access inside that environment.

**Verify:** In a disposable test environment, inspect only known synthetic secret locations and verify that reusable provider credentials are absent from the agent's view.

**Evidence:** Architecture, allowed credential exceptions and synthetic isolation test.  
**Suggested owner:** Platform owner

### K06 · Constrain the credential broker itself

- [ ] **P0 · agents** — Bind each broker operation to an authenticated caller, approved destination, account, method and resource. Do not forward credentials across arbitrary redirects.

**Verify:** Try a wrong destination, cross-account request, redirected request and revoked caller using test credentials; each unauthorized case must fail.

**Evidence:** Broker policy and negative-test results.  
**Suggested owner:** Platform owner

### K07 · Prove revocation works

- [ ] **P0 · all** — Provide a documented emergency path for revoking keys, sessions, refresh tokens, workload trust and derived access.

**Verify:** Revoke a disposable credential, then retry from an existing session and a new session; measure the effective cutoff.

**Evidence:** Timed revocation drill and list of dependent credentials.  
**Suggested owner:** Identity owner

### K08 · Block unnecessary metadata credentials

- [ ] **P0 · self-hosted, agents** — Prevent untrusted workloads from reaching cloud metadata and container credential services unless specifically required; minimize any attached workload role.

**Verify:** Use an isolated test setup to verify network denial and inspect the effective identity policy; never collect production metadata tokens as evidence.

**Evidence:** Egress policy, workload role and test result.  
**Suggested owner:** Cloud owner

## Dependencies and release pipelines

### S01 · Lock the full dependency graph

- [ ] **P0 · all** — Use reviewed lockfiles for direct and transitive packages, verified artifact hashes where supported, and container digests. A pinned malicious release remains malicious.

**Verify:** Build in a clean environment using the enforced lockfile mode and compare the resolved manifest with the reviewed one.

**Evidence:** Lockfile, artifact digest and build manifest.  
**Suggested owner:** Engineering owner

### S02 · Treat build and security tools as production dependencies

- [ ] **P0 · all** — Review and pin CI actions and scanners; use full commit identifiers for actions and verified immutable artifacts where available.

**Verify:** Inspect every workflow, including reusable workflows, for moving tags or unreviewed downloads; verify the referenced upstream repository.

**Evidence:** Workflow inventory and reviewed immutable references.  
**Suggested owner:** Build owner

### S03 · Separate untrusted builds from release credentials

- [ ] **P0 · all** — Run pull requests, dependency builds and third-party scanners without publishing or production credentials. Grant release access only in a protected stage.

**Verify:** Run a synthetic untrusted contribution and confirm it cannot obtain a release token, edit protected artifacts or trigger an authorized release.

**Evidence:** Job permission map and release-stage test.  
**Suggested owner:** Build owner

### S04 · Protect publishing identity

- [ ] **P0 · all** — Use short-lived release identity where supported, strong maintainer authentication and restricted repository, workflow, ref and environment trust.

**Verify:** Attempt a release from an unapproved ref using a test package or dry-run target; verify denial.

**Evidence:** Release policy and negative authorization test.  
**Suggested owner:** Release owner

### S05 · Verify artifact origin and integrity

- [ ] **P1 · all** — Use approved registries and publishers; validate signatures or provenance where provided and inspect changes between reviewed source and distributed artifacts.

**Verify:** Select one deployed artifact and link its digest to the reviewed release and build provenance; document gaps.

**Evidence:** Artifact origin record and verification output.  
**Suggested owner:** Build owner

### S06 · Review model and plugin installation behavior

- [ ] **P1 · all** — Treat model loaders, custom model code, install hooks, IDE extensions, skills and local MCP packages as executable software.

**Verify:** Inspect manifests and installation behavior in a disposable environment with synthetic data; identify network access and executable hooks.

**Evidence:** Component review and approved install procedure.  
**Suggested owner:** Engineering owner

### S07 · Update deliberately and promptly

- [ ] **P1 · all** — Assign patch ownership, monitor advisories, set risk-based deadlines and test upgrades with rollback. Dependency locking must not become permanent stagnation.

**Verify:** Take a relevant advisory through triage, affected-version discovery, staging checks and rollout or documented mitigation.

**Evidence:** Patch register, deployment inventory and rollback record.  
**Suggested owner:** Platform owner

### S08 · Rebuild compromised environments

- [ ] **P0 · all** — For suspected malicious dependencies, quarantine affected runners, caches, images and environments; preserve evidence, revoke exposed access and rebuild from trusted inputs.

**Verify:** Tabletop a poisoned dependency: identify all builds and downstream artifacts, then demonstrate clean rebuild and credential revocation paths.

**Evidence:** Artifact lineage and recovery exercise.  
**Suggested owner:** Incident lead

## Network and endpoint access

### N01 · Restrict inbound reachability

- [ ] **P0 · self-hosted, agents** — Keep model, tool, database and management endpoints on approved interfaces and networks. Review port publishing, tunnels, load balancers and IPv6 as well as IPv4.

**Verify:** From authorized external and internal test vantage points, verify that only intended paths are reachable, including direct backend addresses.

**Evidence:** Endpoint inventory and reachability results.  
**Suggested owner:** Network owner

### N02 · Authenticate every protected entry point

- [ ] **P0 · all** — Enforce authentication and authorization on inference, administration, uploads, model management, tools and debugging endpoints. Test direct paths around the gateway.

**Verify:** Send no-credential, invalid-credential and low-privilege requests to test endpoints; protected operations must fail without performing work.

**Evidence:** Route-to-policy map and negative-test results.  
**Suggested owner:** Application owner

### N03 · Separate administration from ordinary use

- [ ] **P0 · all** — Give configuration, model import, backend installation, tool registration and credential management their own restricted administrative permissions.

**Verify:** Use a regular user identity to attempt a harmless configuration change in staging; verify denial independently of the UI.

**Evidence:** Role matrix and denied admin test.  
**Suggested owner:** Application owner

### N04 · Control outbound connections

- [ ] **P0 · self-hosted, agents** — Allow only destinations and operations required for the workflow; include DNS, direct IP access, proxies, redirects and alternate protocols in the design.

**Verify:** Use synthetic traffic to approved and disallowed test destinations from the actual workload identity and network namespace.

**Evidence:** Egress rules and allow/deny observations.  
**Suggested owner:** Network owner

### N05 · Defend URL-fetching paths

- [ ] **P0 · all** — Validate resolved destinations and redirects for fetch tools, imports, previews, webhooks and authorization discovery; prevent unintended access to private services.

**Verify:** Use controlled fixtures for private, loopback, link-local, redirect and DNS-change cases; verify blocking without querying real sensitive endpoints.

**Evidence:** SSRF test record and destination policy.  
**Suggested owner:** Application owner

### N06 · Protect transport and browser access

- [ ] **P1 · all** — Use validated encrypted transport across relevant boundaries; set narrow browser origins and host checks, and CSRF protection for cookie-authenticated changes.

**Verify:** Test an invalid certificate, unexpected origin or host, and a forged state-changing request; confirm rejection. CORS is not authentication.

**Evidence:** TLS configuration and browser negative tests.  
**Suggested owner:** Application owner

### N07 · Limit resource consumption

- [ ] **P1 · all** — Enforce per-identity and per-tenant request, token, concurrency, upload, execution-time and spend limits; alert before exhaustion.

**Verify:** Apply a small agreed load in staging; verify throttling, cancellation and cost controls without affecting production.

**Evidence:** Limit configuration and bounded load-test results.  
**Suggested owner:** Service owner

## Agents, tools and authorization

### A01 · Authorize actions outside the model

- [ ] **P0 · agents** — Enforce tool, operation and resource permissions in trusted code using the real caller's authority. Model text and tool descriptions must not grant access.

**Verify:** Request a harmless out-of-scope action and verify the tool service rejects it even when the model proposes it.

**Evidence:** Policy decision and denied tool call.  
**Suggested owner:** Application owner

### A02 · Require precise approval for high-impact actions

- [ ] **P0 · agents** — For payments, deletion, permission changes, publishing or external messages, show the exact target and material payload or diff before approval; bind approval to that action and expiry.

**Verify:** Change the target or payload after a test approval, replay it, or let it expire; the executor must reject the altered or stale request.

**Evidence:** Approval record and integrity tests.  
**Suggested owner:** Application owner

### A03 · Treat retrieved instructions as untrusted data

- [ ] **P0 · agents** — Emails, pages, images, documents, repository files, skills and tool responses cannot override authorization. Use content screening as an additional layer.

**Verify:** Place a benign instruction to cross a test boundary in an external document; verify no unauthorized action or data access occurs.

**Evidence:** Injection regression case and tool audit trail.  
**Suggested owner:** Security lead

### A04 · Review integrations and permission changes

- [ ] **P0 · agents** — Approve each tool server, publisher, endpoint, local command, declared capability and update path; re-review changes in behavior or requested scope.

**Verify:** Compare deployed integrations with the approved inventory and simulate a changed tool description or newly requested permission.

**Evidence:** Integration manifest and change review.  
**Suggested owner:** Integration owner

### A05 · Keep tool sessions bound to identities

- [ ] **P0 · agents** — For remote integrations, validate token audience, issuer, expiry and scopes; bind session handles to the user and client. Apply explicit consent where acting for users.

**Verify:** Try another user's session handle, a token for a different audience and a revoked grant in staging; all must fail.

**Evidence:** Auth configuration and cross-user tests.  
**Suggested owner:** Identity owner

### A06 · Validate tool arguments and results

- [ ] **P1 · agents** — Use schemas plus business rules for paths, amounts, recipients and resource identifiers; use safe APIs instead of concatenating model text into shell or SQL.

**Verify:** Submit malformed inputs and validly shaped but unauthorized values; verify rejection before any side effect.

**Evidence:** Validation tests and safe execution interface.  
**Suggested owner:** Engineering owner

### A07 · Constrain autonomy and handoffs

- [ ] **P1 · agents** — Set step, retry, time and cost budgets; preserve the initiating user's permissions across agent handoffs and require a working cancel path.

**Verify:** Trigger a bounded loop and a handoff to a more privileged test agent; verify termination and no privilege expansion.

**Evidence:** Run limits, cancellation event and delegation tests.  
**Suggested owner:** Application owner

## Execution and storage isolation

### I01 · Contain the entire execution path

- [ ] **P0 · agents** — Evaluate the agent harness, internal helpers, shell, Git, file tools, plugin subprocesses and browser workers as part of the execution boundary.

**Verify:** Run benign boundary tests through multiple tool and background-helper paths, not only the shell; inspect where child processes execute.

**Evidence:** Process-boundary diagram and test matrix.  
**Suggested owner:** Platform owner

### I02 · Share only necessary host resources

- [ ] **P0 · agents, self-hosted** — Avoid mounting the host root, home directory, credentials, browser profile, SSH agent or container daemon socket into untrusted workloads. Scope required mounts and prefer read-only access.

**Verify:** Inspect effective mounts, inherited environment and reachable sockets; verify a synthetic host-only file remains inaccessible.

**Evidence:** Sanitized mount/socket inventory and canary test.  
**Suggested owner:** Platform owner

### I03 · Keep enforcement outside untrusted execution

- [ ] **P0 · agents** — Keep authorization state, broker secrets and control-plane interfaces outside memory and storage readable or writable by the agent; authenticate every privileged request.

**Verify:** Verify that synthetic enforcement secrets and policy files are absent from the guest and that forged control requests are rejected.

**Evidence:** Control-plane design and access tests.  
**Suggested owner:** Platform owner

### I04 · Reduce operating-system privileges

- [ ] **P1 · self-hosted, agents** — Run with the least required user and capabilities; restrict unnecessary syscalls, namespaces, devices and kernel modules. Test compatibility before tightening.

**Verify:** Compare effective privileges with the workload's requirements and exercise denied operations in a disposable environment.

**Evidence:** Runtime profile and compatibility test.  
**Suggested owner:** Platform owner

### I05 · Test file boundaries beyond path strings

- [ ] **P0 · agents** — Constrain file and patch operations using resolved, authorized resources; account for symlinks, nested directories, renames and changes between validation and use.

**Verify:** Use benign fixtures for traversal, symlink redirection and renamed parents; confirm reads and writes stay within the intended workspace.

**Evidence:** Filesystem boundary tests and affected-version record.  
**Suggested owner:** Engineering owner

### I06 · Patch every isolation layer

- [ ] **P1 · self-hosted, agents** — Track the host OS, guest OS, runtime, hypervisor, filesystem-sharing layer, agent and extensions; an updated application can still use an old guest image.

**Verify:** Compare running versions and image digests against approved baselines and applicable vendor advisories.

**Evidence:** Runtime version inventory and patch evidence.  
**Suggested owner:** Platform owner

### I07 · Separate sessions and clean up reuse

- [ ] **P0 · agents, self-hosted** — Isolate users and tenants across disks, memory, temporary files, browser state and snapshots. Define cleanup for recycled environments and failed jobs.

**Verify:** Run two disposable identities in sequence with synthetic markers and verify the second cannot retrieve the first's data; review infrastructure erasure guarantees.

**Evidence:** Session isolation tests and storage lifecycle policy.  
**Suggested owner:** Platform owner

## Data, retrieval and output handling

### D01 · Minimize the data sent to each component

- [ ] **P0 · all** — Send only fields needed for the task; redact or tokenize sensitive values before external processing where the workflow allows it.

**Verify:** Trace a synthetic request through model, tool, telemetry and retry paths and compare every field with the approved data flow.

**Evidence:** Redacted trace and minimization rules.  
**Suggested owner:** Data owner

### D02 · Check actual provider data settings

- [ ] **P0 · all** — Document retention, training use, support access, subprocessors, processing locations and deletion behavior for the exact service, account tier and features used.

**Verify:** Inspect account settings and applicable service terms; test deletion where supported and record exceptions such as abuse-monitoring retention.

**Evidence:** Dated settings and vendor review.  
**Suggested owner:** Data owner

### D03 · Enforce retrieval permissions before generation

- [ ] **P0 · rag** — Apply current user and tenant permissions to documents, chunks, metadata and retrieval queries; never rely on the model to hide unauthorized context.

**Verify:** Give two synthetic users different document rights; test direct retrieval and generated answers for cross-user access.

**Evidence:** ACL mapping and retrieval negative tests.  
**Suggested owner:** Application owner

### D04 · Isolate memory, caches and sessions

- [ ] **P0 · rag, agents** — Scope conversation history, retrieval caches, embeddings and saved memory to their intended identity and purpose; validate what may become persistent memory.

**Verify:** Repeat similar requests across test tenants and inject an untrusted memory instruction; verify no data or authority crosses boundaries.

**Evidence:** Cache-key design and memory/session tests.  
**Suggested owner:** Application owner

### D05 · Control retention and deletion end to end

- [ ] **P1 · all** — Define lifetimes for uploads, prompts, outputs, traces, embeddings, temporary files, snapshots and backups; document how deletions and permission removals propagate.

**Verify:** Delete a synthetic document and revoke access; verify active copies disappear and backup handling follows the documented schedule.

**Evidence:** Retention matrix and deletion/revocation test.  
**Suggested owner:** Data owner

### D06 · Validate outputs before downstream use

- [ ] **P0 · all** — Treat model output as untrusted at rendering, export and execution boundaries; sanitize active content, enforce destination permissions and review sensitive disclosures.

**Verify:** Use synthetic active markup, formula-like export cells and sensitive markers; confirm safe rendering/export and blocked unauthorized delivery.

**Evidence:** Output handling tests and release checks.  
**Suggested owner:** Engineering owner

### D07 · Protect ingestion and model assets

- [ ] **P1 · rag, all** — Restrict who can change datasets, retrieval indexes, model files and configuration; record origin, version and integrity and quarantine untrusted uploads.

**Verify:** Try an unauthorized index change and process a benign malformed upload in staging; verify denial or isolation and traceability.

**Evidence:** Ingestion policy, dataset lineage and version record.  
**Suggested owner:** Data owner

## Detection, response and recovery

### O01 · Log attributable security events

- [ ] **P0 · all** — Record user and workload identities, tool operations, targets, policy decisions, approvals, versions and timestamps with correlation IDs; redact content and secrets.

**Verify:** Trace one permitted and one denied test request across components without relying on the model's own narrative.

**Evidence:** Sanitized event chain and log access policy.  
**Suggested owner:** Operations owner

### O02 · Alert on meaningful changes and misuse

- [ ] **P1 · all** — Monitor new exposed endpoints, unusual credential use, privilege changes, disabled controls, unexpected egress, repeated denials and spend spikes.

**Verify:** Trigger selected low-impact synthetic events and verify alerts reach an accountable responder.

**Evidence:** Alert rules, routing and drill results.  
**Suggested owner:** Operations owner

### O03 · Provide independent containment controls

- [ ] **P0 · agents, all** — Maintain a trusted way to stop tool execution, revoke identities, restrict network access and quarantine environments even if the agent is unresponsive.

**Verify:** Stop a benign long-running staging task from outside the agent; verify both current and newly queued actions cease.

**Evidence:** Timed containment test and operator procedure.  
**Suggested owner:** Incident lead

### O04 · Prepare the credential-exposure response

- [ ] **P0 · all** — Plan containment, evidence preservation, clean-device revocation, session invalidation, persistence review, clean rebuild and downstream impact analysis.

**Verify:** Exercise the incident playbook with a fake exposed key and a compromised-dependency scenario; record decisions and gaps.

**Evidence:** Incident exercise and revised runbook.  
**Suggested owner:** Incident lead

### O05 · Prove recovery and rollback

- [ ] **P1 · all** — Back up necessary configuration and data with restricted access; test restoration into a clean environment and prevent revoked secrets from returning.

**Verify:** Restore a synthetic workload from backup, verify permissions and integrity, and ensure old credentials remain unusable.

**Evidence:** Restore report and recovery objectives.  
**Suggested owner:** Operations owner

### O06 · Repeat security acceptance tests

- [ ] **P1 · all** — Rerun applicable tests after material changes and on a documented schedule; keep versioned evidence and track unresolved findings.

**Verify:** Select the most recent release and verify tests match its actual versions, integrations and permissions.

**Evidence:** Acceptance-test report and remediation backlog.  
**Suggested owner:** Security lead

## Suppliers and shared infrastructure

### V01 · Verify assurance scope and issuer

- [ ] **P1 · all** — Review actual audit reports, certification scope, dates, exclusions and independent issuers; verify that the deployed service and relevant controls are covered.

**Verify:** Match a supplier claim to the underlying current report and identify customer responsibilities and unresolved findings.

**Evidence:** Vendor assessment and report review.  
**Suggested owner:** Procurement owner

### V02 · Establish tenant-storage isolation

- [ ] **P0 · cloud, self-hosted** — For shared infrastructure, obtain evidence of allocation, deletion, reuse and snapshot isolation; assess per-tenant key separation where supported. Disk encryption alone does not prove tenant isolation.

**Verify:** Review the provider's or platform team's isolation design and assurance evidence; run only authorized synthetic tenant tests within your own scope.

**Evidence:** Storage isolation review and accepted residual risk.  
**Suggested owner:** Cloud owner

### V03 · Define security change and incident communication

- [ ] **P1 · all** — Identify who receives vendor advisories, how affected versions are located and when incident notifications reach your team.

**Verify:** Route a sample advisory to the owner and find affected deployments from the inventory.

**Evidence:** Notification contacts and response workflow.  
**Suggested owner:** Service owner

### V04 · Plan exit and offboarding

- [ ] **P1 · all** — Document connector removal, identity revocation, data export/deletion, retention exceptions and operational fallback when a provider or plugin is removed.

**Verify:** Offboard a disposable integration and confirm both access termination and data-lifecycle follow-through.

**Evidence:** Exit checklist and test record.  
**Suggested owner:** Service owner

## Completion

Use the release decision above, record remaining risk and schedule the next review. A completed checklist describes the assessed configuration at a point in time; it is not a guarantee of security.
