# AI Credential and Component Incident Playbook

Use this when a key may have leaked, a malicious package ran, an unauthorized AI action occurred or an execution boundary may have failed. Assign an incident lead and follow the organization's existing incident process. Adapt the sequence when containment and evidence preservation conflict; record the decision.

## 1. Establish scope and contain

- Record the detection time, affected workflow, runtime versions, artifact digests and identities.
- Stop new jobs and high-impact tool actions from a trusted control plane. Block unauthorized egress and isolate affected hosts or runners as appropriate.
- Suspend exposed endpoints or remove the unsafe integration. Preserve necessary business fallback paths.
- Use a known-clean administrative device. Do not place replacement secrets into a potentially compromised environment.

## 2. Preserve useful evidence

- Preserve relevant audit events, job logs, package manifests, images, configuration changes and identity events in restricted storage.
- Capture volatile evidence or snapshots through the incident-response team when needed. Snapshots themselves may contain sensitive material.
- Record collection time, collector, integrity information and access controls.
- Do not run a suspect interpreter merely to inspect an installed package: startup hooks may execute before your command. Prefer offline inspection or a clean forensic environment.
- Avoid premature cache deletion or rebuilding until evidence needs are addressed, unless immediate containment requires it.

## 3. Revoke exposed authority

- Inventory keys, browser sessions, refresh tokens, workload roles, SSH access, package-publishing access and cloud/container credentials reachable from the affected context.
- Revoke or disable affected access promptly from a clean system. Account for already issued sessions and credentials derived from the original identity.
- Investigate new identities, grants, integrations, scheduled jobs, persistence and configuration changes created during the exposure window.
- Verify access is actually denied after revocation. Do not assume rotating one API key terminates every related session.

## 4. Trace downstream impact

- Find every environment, build, cached package, image and deployment that used the affected artifact or identity.
- Distinguish downloaded, installed, executed, exposed and confirmed compromised states. Record unknowns.
- Review cloud, identity, data-store and tool logs for use of valid credentials from unexpected contexts.
- Review lateral access into other workloads, repositories, tenant data and internal services.
- Separate confirmed disclosure from plausible exposure in internal and external statements. Follow your established notification and legal review process where applicable.

## 5. Recover from trusted inputs

- Rebuild affected execution environments from approved images and verified dependencies. Package removal alone may leave startup hooks, persistence or contaminated artifacts.
- Replace or quarantine affected caches, images and backups according to the incident findings.
- Reintroduce minimal credentials only into the clean environment; repair the original trust or authorization gap.
- Restore required data and configuration from verified sources. Ensure obsolete privileges and secrets are not restored.
- Run the relevant acceptance tests, including authentication, scope, egress, tenant isolation and independent containment.

## 6. Close with evidence

- Record root cause, confirmed impact, remaining uncertainty, containment and recovery times, and the authority that approved resumption.
- Assign corrective actions and deadlines; update the inventory, threat model and checklist assessment.
- Monitor for delayed use of previously exposed credentials and recurrence of the compromised path.

## A short exercise

**Scenario:** a reviewed AI plugin acquires a malicious transitive dependency during installation on a build runner. The runner can read a synthetic test key and has a route to an external service.

**Questions:** Which artifacts identify all affected builds? Which identities were reachable? Can release access be stopped independently? How is evidence preserved? Can a clean rebuild avoid the poisoned cache? What proves the old key and derived access no longer work?

Record the answers in a private incident exercise. Do not place real incident details in this repository's public issues.
