# 12 Essential Questions Before Deploying AI

**A first-pass discussion for business owners and technical teams.**

Ask for a demonstration or a dated evidence reference. “We think so” is an open item. This short list helps you start; it does not replace the [full checklist](CHECKLIST.md).

- [ ] **1. Can we name an owner and stop the workflow?** Someone owns its permissions, data and risk, and an operator can disable it independently of the AI. **Ask for:** owner record and stop test. **Controls:** G01, O03.
- [ ] **2. Do we know every place our data goes?** Include models, tools, uploads, logs, caches, indexes and support systems. **Ask for:** one traced request and a data-flow diagram. **Controls:** G02–G04, D01–D02.
- [ ] **3. Can the AI read reusable credentials?** Check its environment, files, browser sessions, mounted folders and inherited access. **Ask for:** credential map and synthetic isolation test. **Controls:** K01, K04–K06, I02.
- [ ] **4. Would a stolen key have limited reach?** Use separate identities, narrow permissions and short lifetimes. **Ask for:** an out-of-scope denial and a revocation test. **Controls:** K02–K03, K07–K08.
- [ ] **5. Is every installed component deliberate?** Include transitive packages, scanners, plugins, models and update paths. **Ask for:** enforced lockfiles, immutable artifacts and patch ownership. **Controls:** S01–S02, S05–S07.
- [ ] **6. Can an untrusted build reach release or production access?** Release permissions belong in a separately protected stage. **Ask for:** build/release permission map. **Controls:** S03–S04.
- [ ] **7. Can an outsider reach a model or management endpoint?** Check direct backend access, published ports and temporary tunnels. **Ask for:** an authorized external test and authentication failures. **Controls:** N01–N03.
- [ ] **8. Can the workload send data anywhere it wants?** Define approved destinations and prevent unintended access to internal or metadata services. **Ask for:** egress deny test using synthetic data. **Controls:** N04–N06, K08.
- [ ] **9. Can a document or tool response grant new powers?** Authorization must be enforced by trusted code; high-impact actions need approval tied to the actual target and payload. **Ask for:** a blocked action and an altered-approval rejection. **Controls:** A01–A07.
- [ ] **10. What remains protected if the agent gains full control of its environment?** Inspect host shares, privileged interfaces, helper processes and data left between sessions. **Ask for:** boundary tests and isolation evidence. **Controls:** I01–I07, V02.
- [ ] **11. Can one user retrieve another user's information?** Test documents, memories, caches, downloads and final outputs with two synthetic identities. **Ask for:** denied cross-user retrieval and deletion checks. **Controls:** D03–D07.
- [ ] **12. Can we detect a problem and recover cleanly?** Revoke access, preserve evidence, rebuild affected environments and retest. **Ask for:** a completed exercise and supplier escalation path. **Controls:** S08, O01–O06, V01–V04.

## Turn answers into action

For every unchecked item, record an owner, next action and due date in a private assessment. Use the full checklist to decide whether it blocks deployment. Do not average away a failed launch gate.

A good answer sounds like: “The deployment identity cannot modify permissions. We tested that yesterday, and here is the denied request.”
