# gjallar-skills

Agent skills for working **with** and **on** [Gjallar](https://github.com/heimdallr-dev/gjallar),
packaged as a Claude Code plugin. Plain Markdown (`SKILL.md`), so any agent
that reads skills, or any person, can use them.

> **Security without chains.** See clearly, understand why, and stay free to choose.
> Gjallar sounds the horn when danger is real; what you do next is always yours.
> Full text: [PHILOSOPHY.md](PHILOSOPHY.md)

| Skill | Use it when |
|---|---|
| [`gjallar-philosophy`](skills/gjallar-philosophy/SKILL.md) | Designing, reviewing, documenting or deciding anything for Gjallar. The nine freedoms and four refusals, and how to apply them as a tie-breaker |
| [`gjallar-triage`](skills/gjallar-triage/SKILL.md) | Answering "what do we fix first?" with Gjallar's MCP tools, CLI or API: few findings, real reasons, options instead of orders |
| [`gjallar-contributing`](skills/gjallar-contributing/SKILL.md) | Changing code, chart, policies or docs in any heimdallr-dev repo: layers, pinned downloads, tests, which repo owns what |

## Install

Claude Code:

```text
/plugin marketplace add heimdallr-dev/gjallar-skills
/plugin install gjallar@heimdallr-dev
```

Or copy a skill folder into `~/.claude/skills/` (personal) or
`.claude/skills/` (one project). Other agents: point them at the `SKILL.md`
files; they are self-contained.

Pair `gjallar-triage` with the MCP server setup in
[gjallar-mcp](https://github.com/heimdallr-dev/gjallar-mcp).

## Keeping the philosophy in sync

`skills/gjallar-philosophy/SKILL.md` is the canonical philosophy skill;
`PHILOSOPHY.md` and the docs' `philosophy.md` quote the same text. Change all
three together.

Apache-2.0.
