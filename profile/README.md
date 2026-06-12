<p align="center">
  <img src="./images/af-banner.png" alt="Aesthetic Function Banner" width="100%" />
</p>

<h1 align="left">Aesthetic Function</h1>

Design systems break silently. Tokens drift between Figma and code. Components fall out of sync across frameworks. Documentation lags behind both. AI coding agents generate UI with no awareness of your system's constraints.

Aesthetic Function is a reconciliation engine for design systems: it continuously checks Figma, code, and documentation against one reconciled model, shows you exactly where they disagree, and writes corrections back through a single audited path. Beneath it sit three open-source projects you can use on their own.

## Projects

**[dspack](https://github.com/aestheticfunction/dspack)** is an open JSON specification for representing what a design system knows: tokens, components, patterns, and anti-patterns, in one portable artifact that AI agents can query. Think of it as OpenAPI for design systems.

**[dspack-export](https://github.com/aestheticfunction/dspack-export)** generates a spec-valid dspack snapshot from a React + Tailwind/shadcn codebase, file-based and offline: it answers what your design system looks like right now. It can also import tokens from a DTCG JSON file, the format Figma, Tokens Studio, and Style Dictionary export. Snapshots only: no network, no write-back, no drift detection. Experimental.

**[ds-mcp](https://github.com/aestheticfunction/ds-mcp)** is a read-only MCP server that loads a dspack file and exposes your design system as tools AI coding agents can query at coding time. Drop it into any MCP-compatible environment (Claude, Cursor, GitHub Copilot) and your agent gets token lookups, component API references, and pattern guidance without custom prompting.

**[aesthetic-function](https://github.com/aestheticfunction/aesthetic-function)** is the open-core reconciliation engine beneath a commercial product. It detects drift between what your Figma file says, what your code implements, and what your documentation claims, then tells you exactly where they disagree.

## How they fit together

dspack-export generates the dspack file from your code. You commit it. ds-mcp serves it to your agents. Aesthetic Function reads the committed file as a reference contract and continuously checks every surface against it. AF does not write dspack files: when code drifts from the contract, that same drift is your signal to regenerate the snapshot with dspack-export.

You can use each independently. dspack files are just JSON, so they stand alone. The open tools work without us, forever, under Apache 2.0. AF is what happens when you want the loop run continuously and safely.

## Status

Active development. Contributions and feedback welcome. Open an issue in the relevant repo.

## License

Apache 2.0
