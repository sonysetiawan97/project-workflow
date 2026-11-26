---
name: project-grilling
description: PM interview that settles a project's problem, goals, actors, features and scope, writing glossary.md and product ADRs as decisions settle. Run after project-setup, before project-prd in the same conversation.
disable-model-invocation: true
---

# Project grilling

Relentless interview with the PM until every product topic below has a settled answer. Writes the project's language into `glossary.md` and product decisions into `docs/adr/` as they settle. The answers themselves stay in this conversation: `project-prd` runs next, in the same conversation, and writes `docs/prd.md` from them.

## Language

- Talk to the PM in Indonesian. Every file written into the project is in Indonesian.
- File and folder names are lowercase kebab-case.

## Topics

The done-bar. Each topic mirrors a section of the PRD template owned by `project-prd`.

| Topic | Settled when |
|---|---|
| Masalah | the problem and who has it, in the PM's words |
| Tujuan | outcomes, each measurable |
| Bukan Tujuan | what this version deliberately leaves out |
| Aktor | every user role and what it does in the system |
| Fitur | every feature with a name, priority (`must`, `should`, `could`) and a one-sentence summary |
| Metrik Keberhasilan | numbers that show the product works |
| Batasan dan Asumsi | business, time and regulatory limits; unproven assumptions |

## Process

### 1. Check

`glossary.md` and `docs/adr/README.md` exist in the project. If either is absent, stop and tell the PM to run `project-setup` first.

Read `AGENTS.md`, `glossary.md`, `docs/adr/README.md`, every ADR in `docs/adr/`, and `docs/prd.md` if it exists. An existing `docs/prd.md` means this is a re-run: grill only what changes, keep existing feature IDs, and treat its content as the current answer for each topic.

Done when every file above is read and the mode (first run or re-run) is known.

### 2. Grill

- One question at a time, recommended answer first, with the reason.
- Walk the topics in order, but follow a thread when an answer opens one: a new actor, a new feature, a contradiction with an earlier answer or an existing ADR.
- Push vague answers to concrete ones: a goal without a number, a feature without a priority, an actor without a role.
- A technical question (database, framework, hosting, API shape, integration mechanics) goes to the tech lead, not the PM. Record it as an open question and move on.
- Write as decisions settle, not at the end:
  - **Glossary**: when a domain term is fixed, add or update its entry in `glossary.md`, following the template in that file's header comment. The definition says what the term is, not what it does. Ask the PM when two words name one concept.
  - **ADR**: when a decision meets all three conditions in `docs/adr/README.md` and the PM confirms it, write it there with `Cakupan: product`, `Pemutus: PM`, `Sumber: sesi grilling YYYY-MM-DD`. Superseding an existing ADR follows the rules in that file.

Done when every topic is settled or holds an open question the PM could not answer, and the PM confirms nothing is missing.

### 3. Recap

Post the recap in the conversation, in Indonesian: one heading per topic with its settled answer, features numbered `F-01`, `F-02`, ... (continuing the existing IDs on a re-run), then a `Pertanyaan Terbuka` list with each question and who must answer it (PM or tech lead). This recap is what `project-prd` writes from; it must stand on its own if earlier turns are compacted.

List the glossary entries and ADRs written this session. Name the next step: run `project-prd` in this conversation.

Done when the PM confirms the recap.
