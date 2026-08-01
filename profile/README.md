# JustMe Digital Marketing Services

**Let's Elevate Your Unique Brand**

We are a digital marketing agency with an in-house software arm. This organization holds the
software: two multi-tenant business platforms — an **ERP** and a **CRM** — built and operated for
the businesses that run their day-to-day work on them.

Both platforms share one architectural commitment:

> **One shared codebase. One deployment per tenant. Tenancy is data, never code.**
>
> There is no `tenant_id` column threaded through the application. There is no `if (tenant === ...)`
> branch anywhere in the core. A tenant is a config file plus an environment variable, and each
> tenant's data lives in its own PostgreSQL schema.

**The platform repositories in this organization are private.** They are commercial software
operated on behalf of the businesses that depend on them. What follows is the design, not a link
to the code.

---

## The multi-tenancy model

```
                     ┌──────────────────────────────┐
                     │   core/   (shared, one copy) │
                     │   API · UI · domain logic    │
                     │   never branches on tenant   │
                     └──────────────┬───────────────┘
                                    │  built + deployed once per tenant
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
      ┌───────▼────────┐    ┌───────▼────────┐    ┌───────▼────────┐
      │ deployment:    │    │ deployment:    │    │ deployment:    │
      │   acme         │    │   bravo        │    │   cirrus       │
      │ TENANT=acme    │    │ TENANT=bravo   │    │ TENANT=cirrus  │
      └───────┬────────┘    └───────┬────────┘    └───────┬────────┘
              │                     │                     │
      ┌───────▼────────┐    ┌───────▼────────┐    ┌───────▼────────┐
      │ schema:        │    │ schema:        │    │ schema:        │
      │   acme_erp     │    │   bravo_erp    │    │   cirrus_erp   │
      └────────────────┘    └────────────────┘    └────────────────┘
       PostgreSQL — no tables shared across tenants
```

*Tenant names shown are placeholders.*

### The trade-offs we chose, and why

| Decision | What we gave up | What we bought |
|---|---|---|
| **Schema-per-tenant** instead of a shared table with a tenant column | Cross-tenant reporting is a deliberate, explicit job rather than a `WHERE` clause | Cross-tenant leakage is structurally impossible. A forgotten filter cannot expose another tenant's data, because the rows are not in the table. |
| **Per-tenant deployment** instead of one multi-tenant process | More deployments to operate; a release is a rollout, not a single push | Blast radius is one tenant. Resource contention, incidents, and rollbacks stay contained. |
| **Config-driven tenancy** instead of tenant conditionals | Every tenant-varying behaviour must be modelled as data up front | Onboarding a tenant is configuration, not a code change and not a regression risk to existing tenants. |
| **Build-time tenant binding** on the frontend instead of runtime detection | No single bundle serves everyone | A built frontend cannot be pointed at the wrong tenant after the fact. |

### Guards, because discipline is not a control

Conventions get violated. Startup checks do not. Every process refuses to boot when the tenant it
declares does not match the database schema it was pointed at.

Misconfiguration fails **loudly, at startup**, before the first request — instead of quietly
writing one tenant's records into another's schema and being discovered a month later. Schema
migrations are applied per tenant schema and are not considered complete until every tenant has
them.

---

## The platforms

### ERP — multi-department operations

Five modules on one system of record: **Sales, Finance, Production, HR, IT.**

| Area | Capabilities |
|---|---|
| Telephony | Live call monitoring, call detail record ingestion and analytics, per-agent performance rollups |
| Quality | AI-assisted call transcription and automated quality scoring against configurable rubrics |
| Production | Drag-and-drop Kanban pipeline, triage workflows, turnaround-time tracking |
| Commerce | Vendor service catalogue with multi-currency handling, contract and payment tracking, incentive and payout calculation |
| People | Employee directory, attendance and timekeeping with approval workflows |
| Administration | Role-based user administration and an audit trail across core entities |

### CRM — lead lifecycle

Bulk **CSV lead import with duplicate detection**, a **verification and enrichment stage** before a
lead becomes workable, **assignment to sales representatives**, and separate **production** and
**sales** pipeline tracks with their own stages.

Data scoping is per representative, not just per tenant: a rep's queries are constrained
server-side to the leads assigned to them. Reporting and pipeline analytics sit above that
boundary.

---

## Stack

| Layer | Choice |
|---|---|
| Runtime | Node.js 20, Express 5 |
| Frontend | React 19, Vite 7, React Router 7, Tailwind CSS v4, shadcn/ui, Recharts |
| Data | PostgreSQL 17, schema-per-tenant, hand-reviewed migrations |
| Testing | Vitest for unit and integration suites; Playwright for end-to-end, run on demand |
| CI | GitHub Actions |

## Engineering practice

- **CI runs on push and on pull requests** — secret scanning, dependency audit, tests, and a
  production build. Documentation-only changes are skipped by path filter.
- **Tests colocated with source.** A module and its test live next to each other, so deleting the
  code deletes its tests and moving it moves them.
- **A maintained codebase changelog is the source of truth for what shipped.** Every user-visible
  change lands with its entry in the same change, not reconstructed later from commit archaeology.
- **Migrations are explicit and per tenant.** No implicit sync, no ORM guessing at the schema.
- **Dependency advisories are reviewed continuously**, with any accepted risk recorded by advisory
  ID rather than silently ignored.

### Security posture

Session-based authentication with **bcrypt at 12 rounds**, login **rate limiting** and **account
lockout**, **forced password change on first login**, **Helmet**-managed security headers including
a content security policy, **CORS allowlisting**, and **role-based access control** enforced
server-side. Access decisions are made on the API, not in the UI — the frontend hides what a role
cannot do, and the backend refuses it regardless.

---

## The agency

The software arm exists inside a working marketing agency, which is why the platforms are shaped by
operators rather than by a roadmap deck. Agency services:

**Social media marketing** · **SEO** · **Content marketing** · **Email marketing** ·
**PPC advertising** · **Web development**

---

## Contact

**[justmedms.com](https://justmedms.com)** — for platform, partnership, or engineering enquiries:
**it.support@justmedms.com**
