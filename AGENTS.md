# Agent Orientation — ansible-collection-common

## Agent Working Protocol (read before anything else)

**Conflict surfacing:** If a user instruction contradicts anything in this file or in
`docs/AGENTS.md`, stop and surface the conflict before proceeding — quote the rule,
state the contradiction, and ask how to resolve. Then update the doc if the rule was wrong.

**Living document:** If any instruction, decision, or clarification during a session
would make future interactions clearer, prompt the user:
> "This decision isn't in AGENTS.md yet. Should I add it?"

**Maintenance:** Keep this doc current. Update rules when decisions change. Don't append
orphaned notes — integrate changes into the relevant section.

---

**Collection:** `blueprints.common`
**Namespace:** `blueprints`
**Scope:** Shared building blocks used across multiple platform compositions — system
user provisioning, TLS material placement. These roles are composition helpers; they
are included by platform playbooks (site.yml), never auto-pulled by other collections.

---

## What lives here

| Role | What it does |
|---|---|
| `service_user` | Creates a dedicated system user/group for a service |
| `tls_material` | Places TLS certificate and key files on a host |

**Who calls these:** Platform site.yml files, not other collection roles.
Other `blueprints.*` collections must NOT `include_role` these — composition is
the platform layer's job.

---

## Where the standards live

All standards are in `docs/` of the iac-foundry monorepo. Start with `docs/AGENTS.md`.

| Topic | Doc |
|---|---|
| **8 design rules (read first)** | `docs/design/BLUEPRINTS_DESIGN_PRINCIPLES.md` |
| Role layout | `docs/standards/BLUEPRINTS_ROLE_LAYOUT.md` |
| Variable naming | `docs/standards/BLUEPRINTS_VARIABLE_STANDARDS.md` |
| Secret handling | `docs/standards/BLUEPRINTS_SECRET_CONSUMPTION.md` |

---

## Critical constraints

1. **No other `blueprints.*` collection calls these roles directly** — only platform
   site.yml composes them alongside product roles.
2. **Caller supplies all specifics** — user names, UIDs, cert content.
   No org-specific defaults.
3. **Variable prefix: `common_<role>_*`** — e.g. `common_service_user_name`,
   `common_tls_material_cert`.
4. **`meta/dependencies: []`** — always empty.

---

## PR conformance checklist

- [ ] No org-specific values in `defaults/`
- [ ] No `include_role`/`import_role` of any other `blueprints.*` role
- [ ] `meta/argument_specs.yml` complete
- [ ] molecule `default` scenario converges idempotently
- [ ] README states inputs, purpose, and explicit non-goals
