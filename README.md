# Bit Lantern for Claude Code

Bit Lantern is a local, read-only MCP server that gives Claude Code indexed definitions, exact
source ranges, references, static call relationships, architecture summaries, and bounded edit
impact for source repositories.

This repository contains the inspectable Claude plugin wrapper. The separately installed Bit Lantern runtime remains proprietary software under the Bit Lantern license. Installing the plugin
does not download or install the runtime, run repository code, or send source code to Zaguán Labs.

## Requirements

- Claude Code with plugin support
- A supported Bit Lantern installation whose `bitlantern` executable is on `PATH`
- An unmanaged or organization-approved workstation that permits the Bit Lantern preview

Bit Lantern previews for macOS and Windows do not yet carry Apple or Microsoft publisher
signatures. Review the [installation and platform-safety documentation](https://atlasscout.dev/docs)
before installing the runtime. Do not weaken operating-system or organization security controls.

## Setup

Install and verify the Bit Lantern runtime first. The supported installer is published at
<https://atlasscout.dev/install.sh>; signed release metadata, checksums, provenance, and manual
verification guidance are linked from <https://atlasscout.dev/docs>.

```bash
bitlantern --version
bitlantern doctor --workspace /absolute/path/to/project
```

To install directly from the Zaguán Labs marketplace while the community-directory review is
pending:

```bash
claude plugin marketplace add ZaguanLabs/atlas-scout-claude-plugin --scope user
claude plugin install bitlantern@bitlantern --scope user
```

After directory publication, users can install from Anthropic's automatically available official
marketplace:

```text
/plugin install bitlantern@claude-plugins-official
```

Start a new Claude Code session after installation. Run `/mcp` to confirm that the plugin-provided
`bitlantern` server is connected. Remove or disable any duplicate manually registered Bit Lantern
MCP server so Claude Code starts only one copy.

See [SETUP.md](SETUP.md) for troubleshooting and removal instructions.

## What the plugin provides

- A local `stdio` MCP connection that runs `bitlantern mcp`
- A concise code-navigation skill describing Scout's capabilities and coverage boundaries
- Advisory `SessionStart`, `SubagentStart`, and bounded `UserPromptSubmit` context
- Bounded advisory `PreToolUse` context when `Grep` or Bash `rg`/`grep` searches target code identifiers
- Eager discovery metadata for the three navigation entry points

The hooks add human-readable capability context only. The `UserPromptSubmit` reminder appears on
the first prompt and every fifth prompt after, only in indexed workspaces and never twice for a turn
that already received the identifier-search notice. The `PreToolUse` hook locally examines the
current `Grep` pattern or Bash command, stays silent for non-identifier searches and unindexed
workspaces, and has a per-session notice limit. The hooks do not inspect conversation history, deny
or approve tools, modify tool calls, or execute repository code. Temporary reminder counters
contain only the sanitized session identifier and are removed by the operating system's normal
temporary storage lifecycle. Bit Lantern's MCP tools are annotated as read-only, non-destructive,
idempotent, and closed-world.

## Example prompts

1. `Find the definition of reconcile_workspace and show me its exact source range.`
2. `Which functions call SymbolStore::replace_snapshot, and where are those calls?`
3. `Trace the static path from the MCP symbol_search handler to the SQLite query.`
4. `Summarize the indexed module architecture and the strongest cross-module dependencies.`
5. `Estimate the bounded edit impact of changing this public function and identify likely tests.`

Results are bounded by the languages and relationships present in the local index. Claude should
check the returned health, coverage, trust, and truncation metadata before treating an empty result
as exhaustive.

## Data access

Bit Lantern reads source files in the workspace selected by Claude Code and writes a disposable
SQLite index beneath that workspace. It sends navigation results to Claude Code because that is the
plugin's requested function. Bit Lantern does not transmit source code, repository paths, symbols,
queries, tool calls, editor state, Git remotes, or index metrics to the Bit Lantern licensing
service.

The runtime does not execute repository code, hooks, package scripts, builds, or tests. A Free
installation that has never been activated makes no licensing request. Previously activated
installations may perform asynchronous license refreshes as described in the privacy notice.

## Privacy Policy

The Bit Lantern privacy policy describes local indexing, data sent to the connected coding agent,
optional account and licensing data, storage, retention, third-party processing, and contact
details: <https://atlasscout.dev/legal/privacy>.

Privacy questions and requests: <release@atlasscout.dev>.

## Support and security

- Documentation: <https://atlasscout.dev/docs>
- Support: <support@atlasscout.dev>
- Security reports: <support@atlasscout.dev>
- Security process: [SECURITY.md](SECURITY.md)

Do not include proprietary source code, credentials, license tokens, or private repository details
in a public support request.

## Licensing boundary

The Claude plugin wrapper and the Bit Lantern runtime are separate works. The public repository's
license applies only to the plugin wrapper files. The Bit Lantern executable, product source,
documentation shipped with the runtime, and other product materials remain governed by their
separate proprietary terms and EULA.
