<p align="center">
  <img src="./images/af-banner.png" alt="Aesthetic Function Banner" width="100%" />
</p>

<h1 align="left">Aesthetic Function</h1>

Design systems break silently. Tokens drift between Figma and code. Components fall out of sync across frameworks. Documentation lags behind both. AI coding agents generate UI with no awareness of your system's constraints.

Aesthetic Function is a set of open-source tools for keeping design systems honest across surfaces, and making them queryable by AI agents.

## Projects

**[dspack](https://github.com/aestheticfunction/dspack)** is a portable JSON spec for representing design system corpora: tokens, components, patterns, and anti-patterns. Framework-agnostic, AI-readable, human-auditable. Think of it as OpenAPI for design systems.

**[dspack-export](https://github.com/aestheticfunction/dspack-export)** generates a spec-valid dspack snapshot from a React + Tailwind/shadcn codebase: components, cva variant enums and their defaults, semantic color and radius tokens from CSS custom properties, and dark-theme overrides. It can also import tokens from a DTCG JSON file, the format Figma, Tokens Studio, and Style Dictionary export. It is the generator that feeds dspack into ds-mcp. Snapshots only: no network, no write-back, no drift detection. Experimental.

**[ds-mcp](https://github.com/aestheticfunction/ds-mcp)** is a TypeScript MCP server that loads a dspack file and exposes your design system as tools for AI coding agents. Drop it into any MCP-compatible environment (Claude, Cursor, GitHub Copilot) and your agent gets token lookups, component API references, and pattern guidance without custom prompting.

**[aesthetic-function](https://github.com/aestheticfunction/aesthetic-function)** is a framework-aware control plane for deterministic sync across code, design, and component surfaces. It detects drift between what your Figma file says, what your code implements, and what your documentation claims, then tells you exactly where they disagree. Point it at a committed dspack file and it polices your surfaces against that contract over time.

## How they fit together

dspack is the spec. dspack-export generates it from code. ds-mcp serves it to agents. aesthetic-function watches it over time.

You can use each independently. dspack files are just JSON, so they stand alone. dspack-export turns a React + Tailwind codebase into a conformant dspack file. ds-mcp points at any conformant dspack file and exposes it to agents. aesthetic-function reads a committed dspack file as a contract and tells you when your Figma, code, or docs drift away from it.

Together they form one loop: generate a contract from code, serve it to your agents, and let aesthetic-function police it as your surfaces change.

## Status

Active development. Contributions and feedback welcome. Open an issue in the relevant repo.

## License

Apache 2.0
