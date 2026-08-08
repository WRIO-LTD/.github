# WRIO

WRIO is an operating system for verifiable work — an open-core platform for process orchestration and automation. Design and run end-to-end business processes that combine deterministic workflows with agentic automation, spanning people, systems, and AI agents. Built on Cloudflare, with an open-source process engine you can run anywhere.

## WRIO Platform

The WRIO platform is composed of the following components:

- [**bizcom-engine**](https://github.com/WRIO-LTD/bizcom-engine) — the open-core BPMN execution engine. A platform-agnostic process interpreter with BPMN 2.0 round-trip, jexl variables, incidents, and retry. Inspired by Camunda, with zero Cloudflare dependencies so it runs anywhere — on Cloudflare, your own cloud, or on-premises.
- [**bizcom**](https://wr.io) — the BizCom suite: process dashboards, BPMN visualization, logs viewer, and project management for SMBs.
- **forge** — a Knowledge Compiler ("Operating System for Business Knowledge"): knowledge bases, Zettelkasten, MoCB documents, and AI ingestion with semantic search.
- **sonar** — prospecting and outbound: find, qualify, and enrich leads.
- **sentry** — inbound gateway: route messages from Telegram, email, and social into processes.
- **marketplace** — installable process packs and playbooks.
- **operator** — a process-driven operator assistant.

## Open-core model

WRIO follows an open-core strategy:

- **Core (open source)** — `bizcom-engine`: pure BPMN interpreter, model, parser/serializer, variables + jexl, validation, incidents, and built-in `core.*`/`http.request`/`web.fetch_content` nodes. Runs on plain `fetch()` — no infrastructure required.
- **Enterprise (proprietary)** — Cloudflare adapters (D1, R2, CF Workflows), enterprise node catalog (`db.*`, `ai.chat`, `telegram.*`, `storage.*`, `rss.fetch`), and the platform services.

Take the engine, bring your own adapters and node handlers, and run it on your own stack:

```ts
import { ProcessInterpreter, createInMemoryPorts, createBuiltinHandlers } from "@wrio/bizcom-engine";

const ports = createInMemoryPorts();
for (const [action, fn] of Object.entries(createBuiltinHandlers())) {
  ports.nodeHandler.register(action, fn);
}

const engine = new ProcessInterpreter({ ports: ports.ports });
await engine.run(definition, { orderId: 123 });
```

## Get started

- [WRIO](https://wr.io) — product site.
- [bizcom-engine](https://github.com/WRIO-LTD/bizcom-engine) — open-core engine: quickstart, BPMN round-trip, custom nodes, retry & errors.
- [BizCom BDD Spec](https://github.com/WRIO-LTD/monorepo/blob/master/docs/specs/bizcom/BizcomEngine_BDD.md) — behavior specification (Gherkin scenarios).

## Community

We value community contributions. The engine repo is a read-only mirror of `packages/bizcom-engine` in the [WRIO-LTD/monorepo](https://github.com/WRIO-LTD/monorepo); approved PRs are synced back automatically.

- [Open issues](https://github.com/WRIO-LTD/bizcom-engine/issues)
- [Discussions](https://github.com/WRIO-LTD/bizcom-engine/discussions)
