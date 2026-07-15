<p align="center">
  <img src="./images/af-banner.png" alt="Aesthetic Function Banner" width="100%" />
</p>

<h1 align="left">Aesthetic Function</h1>

AI can generate UI. AF keeps it aligned.

Design systems break silently. Tokens drift between Figma and code. Components fall out of sync across frameworks. Documentation lags behind both. And now agents generate UI against a rendering standard with no correctness standard: a catalog says what can render, but nothing says what your design system considers correct.

**A2UI defines what can render. dspack defines what is correct.**

One design-system contract, enforced at two moments. At generation time, the open governance tools check what an agent builds before it renders. Over time, the reconciliation engine keeps code, design, and documentation aligned with the same contract. Three layers stay distinct throughout: the schema answers "can this object exist?", the linter answers "is this object correct?", the renderer answers "can this render?"

## Projects

Six ecosystem repositories plus the open-core engine. All under Apache 2.0.

**[dspack-studio](https://github.com/aestheticfunction/dspack-studio)** is the flagship, the full loop where you can inspect it: an agent generates UI under a dspack contract, streamed over AG-UI as A2UI, rendered with Astryx, with every gate, repair, and state patch recorded and scrubbable. The hosted studio at [studio.aesthetic-function.com](https://studio.aesthetic-function.com) is the replay experience: six recorded real runs, session import, inspectors, and a Break It mode that replays labeled recorded catches for three failure conditions and checks one more client-side; the remaining three say plainly that they need the agent. Live generation is bring-your-own-machine: clone the repo and run the local agent. The hosted demo replays the pipeline's receipts; it does not run the pipeline.

**[dspack](https://github.com/aestheticfunction/dspack)** is an open contract for design systems: schemas, typed governance rules, intents, categories, and examples that define not just what exists but what correct means, in one portable artifact that AI agents can query. Think of it as OpenAPI for design systems.

**[dspack-export](https://github.com/aestheticfunction/dspack-export)** generates a spec-valid dspack snapshot from a component codebase, file-based and offline, with framework-aware extraction that today supports React + Tailwind/shadcn and Vue 3 + Vuetify 3: it answers what your design system looks like right now. Snapshot only: rules, intents, and examples are hand-authored downstream, not extracted. Experimental.

**[dspack-gen](https://github.com/aestheticfunction/dspack-gen)** is the generation and governance pipeline for dspack contracts: it compiles the contract into generation context, generates surfaces with schema-constrained models, lints them deterministically, applies bounded repair, and produces a versioned audit report for every run. Home of the published findings.

**[dspack-emit](https://github.com/aestheticfunction/dspack-emit)** is a deterministic emitter that compiles governed dspack surfaces to rendering protocols, A2UI (0.9.1 and 1.0) and json-render today, each behind its own validation gates. Formerly dspack-to-a2ui.

**[ds-mcp](https://github.com/aestheticfunction/ds-mcp)** is a read-only MCP server that loads a dspack file and exposes your design system as tools AI coding agents can query at coding time, including generation context and surface validation. No network, no shell, no writes. A generate_ui tool is deliberately absent: the MCP host is already the model.

**[aesthetic-function](https://github.com/aestheticfunction/aesthetic-function)** is the open-core reconciliation engine beneath a commercial product. It detects drift between what your Figma file says, what your code implements, and what your documentation claims, then tells you exactly where they disagree.

## How they fit together

dspack-export generates the dspack file from your code. You commit it. ds-mcp serves it to your agents. Aesthetic Function reads the committed file as a reference contract and continuously checks every surface against it. AF does not write dspack files: when code drifts from the contract, that same drift is your signal to regenerate the snapshot with dspack-export.

At generation time the same contract governs what agents build: dspack-gen compiles it into generation context, lints what a model produces against its typed rules, applies bounded repair, and audits every run; dspack-emit projects the governed surface to a rendering protocol; ds-mcp serves the context and validation to any agent that wants to run the loop itself. dspack-studio runs that whole chain end to end, live against a local model or replayed from recordings, and makes every gate and repair inspectable.

You can use each independently. dspack files are just JSON, so they stand alone. The open tools work without us, forever, under Apache 2.0. AF is what happens when you want the loop run continuously and safely.

## Milestones

- **M1, complete.** The governed-generation vertical slice: one intent, typed rules, bounded repair, deterministic A2UI emission, an audit report for every run.
- **M2, complete.** A second emitter target (json-render), the evaluation harness, the ds-mcp generation tools, and the rename to dspack-emit. The original two-local-family M2 run ended with zero end-to-end passes and one dominant failure signature: the projection gap.
- **M3, complete.** dspack v0.4 (the required-props rule type, with component categories in the same revision) and its measured amendment made that failure signature extinct; end-to-end passes rose from 28/216 to 67/216 across three local model families. A second contract, a nine-component slice of Meta's Astryx run through json-render only, proved the rule system generalizes: zero emitter-gate failures in 216 runs.
- **Studio launch, July 12, 2026.** dspack-studio shipped: the full generation-time chain running end to end behind a scrubbable recorder, six recorded real runs, Break It with seven curated failure conditions, hosted replay at [studio.aesthetic-function.com](https://studio.aesthetic-function.com).
- **Next.** Trigger-gated on A2UI v1.0 leaving Candidate status. Deferred and not implemented today: A2UI v1.0 adoption, an MCP Apps emitter, a heuristic governance tier, intent inference, the full Astryx contract, a generic structural selector language, and rule scaffolding in dspack-export.

Every number above traces to a retained audit report: [the M3 report](https://github.com/aestheticfunction/dspack-gen/blob/main/docs/m3-report.md), [the findings](https://github.com/aestheticfunction/dspack-gen/blob/main/docs/findings.md), and [the studio audit](https://github.com/aestheticfunction/dspack-studio/blob/main/docs/AUDIT.md). Pass rates are quoted k/n.

## Status

Active development with early design partners. Contributions and feedback welcome. Open an issue in the relevant repo.

## License

Apache 2.0
