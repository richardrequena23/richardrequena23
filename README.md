# Richard Requena

**GoHighLevel + n8n automation — from the sales side.**

I came to automation from operating a CRM, not from web design. For the past year I've run
day-to-day CRM operations for a high-ticket coaching company: 20,000+ leads processed,
1,400+ booked appointments, and I was the person doing the follow-up. When I build
automation, I'm building the machine I used to *be*.

## What I build

- **Webhook & integration layers** — signed ingress (GHL's Ed25519 `X-GHL-Signature` and
  the Standard Webhooks scheme), idempotent writes, retry ladders with jitter, dead-letter
  queues with replay. Webhooks are at-least-once; I make the *effect* apply exactly once
- **Lead qualification & routing** — every new lead classified, tagged by source, assigned
  an owner, and pushed into the right follow-up sequence automatically
- **Booking systems** — calendars, confirmation + reminder ladders, no-show and
  cancellation recovery loops
- **Reply handling** — when a lead answers, every other automation stops messaging them
  and a human gets alerted once, not twenty times
- **AI steps inside workflows** — model-based scoring and drafting behind strict output
  contracts, deterministic guardrails, and a human-in-the-loop send gate (AI routes and
  drafts; a signed human decision sits in front of the only send node). Where an agent
  touches data, the whitelist is compiled code, not a sentence in a prompt
- **Audits & fixes of inherited accounts** — a [static analyzer](https://github.com/richardrequena23/ghl-workflow-auditor)
  that reads a GHL account export and produces a scored, client-ready report of the defects
  that actually cost money (most are invisible on the canvas), plus a
  [snapshot differ](https://github.com/richardrequena23/ghl-snapshot-diff) that answers
  "what changed since it was working?" — a question GHL itself keeps no history to answer

## Proof, not adjectives

Every repo below is working software with its own verification — test suites, contract
cases exercised over the wire, and execution logs — because "it works" should be a
screenshot, not a promise.

| Repo | The proof |
|---|---|
| [`ghl-workflow-auditor`](https://github.com/richardrequena23/ghl-workflow-auditor) | Static analysis over a GHL account export — 0–100 health score, client-ready HTML report, and a rule catalog generated from the tool's own findings so it cannot describe a check the tool no longer performs. Live rule and test counts are on the repo's badges |
| [`ghl-crm-query-agent`](https://github.com/richardrequena23/ghl-crm-query-agent) | Plain-English questions against a CRM, in n8n — the model names a query from a frozen twelve-entry read-only catalog and never writes one. Read-only proven against a **live write endpoint**: 8 hijack attempts, counter unmoved. 56-case contract suite |
| [`ghl-webhook-hub`](https://github.com/richardrequena23/ghl-webhook-hub) | Signed/idempotent/dead-lettered n8n webhook hub — **18/18 contract tests**, incl. GHL's Sep-1-2026 Ed25519 signature cutover |
| [`ghl-webhook-toolkit`](https://github.com/richardrequena23/ghl-webhook-toolkit) | Zero-dependency Python receiver/router for GHL webhooks — 21 stdlib unittest cases |
| [`ghl-workflow-patterns`](https://github.com/richardrequena23/ghl-workflow-patterns) | 8 documented blueprints of systems published in my own GHL account — 7 architecture diagrams, design decisions, the traps each build hit |
| [`ghl-snapshot-diff`](https://github.com/richardrequena23/ghl-snapshot-diff) | Diffs two workflow exports — unpublished workflows, wiped send windows, re-scoped trigger filters, reworded first touches. **19 tests**, zero dependencies |
| [`lead-csv-hygiene`](https://github.com/richardrequena23/lead-csv-hygiene) | CLI that cleans lead exports before CRM import — every rule learned from 20,000+ real leads |

![Webhook Integration Hub — signed ingress, retry ladder, circuit breaker, DLQ with replay](https://raw.githubusercontent.com/richardrequena23/ghl-webhook-hub/main/images/canvas-hub.png)

## How I work

I use AI tooling (Claude) to author, audit, and document workflows instead of hand-clicking
every node — which is how a solo operator ships and QAs this much. Workflows are emitted by
generator scripts that mechanically refuse to build unverifiable claims (unwired error
outputs, unbounded retries, side effects upstream of dedupe). Every client build ends with
a walkthrough video and a one-page doc so the owner can edit any message themselves.

## Currently building

- Voice AI appointment-setter (Vapi → n8n → GHL calendar) — specced, waiting on a telephony number

## Find me

- Upwork: [Richard R. — GoHighLevel & n8n Automation](https://www.upwork.com/freelancers/~01f07027a75fc5667a)
