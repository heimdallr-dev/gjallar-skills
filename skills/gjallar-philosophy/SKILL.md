---
name: "gjallar-philosophy"
description: "Apply the Gjallar Philosophy (security as freedom, nine freedoms) when designing, reviewing, documenting or deciding anything for the Gjallar project."
---

# The Gjallar Philosophy

Use this skill whenever work touches Gjallar: designing a feature, choosing a dependency, reviewing code or a pull request, writing docs, README copy or release notes, or deciding between options. The philosophy is the tie-breaker: when two designs both work, pick the one that leaves people freer.

## The text (quote it verbatim when asked for the philosophy)

**Gjallar sounds the warning; you stay free to choose.**

In the old story, Heimdall does not rule. He watches. When danger comes, he raises Gjallarhorn and sounds it so that everyone can see, understand and act. The horn gives no orders; it gives awareness.

That's the spirit of Gjallar. Security should make people freer, not smaller. A tool that protects you but traps you hasn't removed the danger; it has only changed its shape. So Gjallar is built around one belief: real security is freedom.

### The nine freedoms

1. **Freedom of choice.** No single tool should become your master. The things you depend on today can be replaced tomorrow, and nothing you have built or learned is lost when you do.
2. **Freedom of origin.** What you protect may live anywhere: big places, small places, public or private, online or cut off from the world. Protection shouldn't depend on where your work happens to sit.
3. **Freedom of approach.** People see, think and work in different ways. Security should meet each person where they are, and no single way of looking at the truth should be the only door.
4. **Freedom of knowledge.** What you learn about your own systems belongs to you. It should never be held hostage, hidden behind a price, or locked in a form only one party can read.
5. **Freedom of place.** Security should travel with you: to a small home setup, to a large organization, to places with no outside connection at all. No one should need permission from far away to protect what is theirs.
6. **Freedom of identity.** You decide who you trust and who may act. Authority comes from the people responsible, never from the tool. Nothing acting on someone's behalf should be able to do more than that person could.
7. **Freedom from noise.** A thousand alarms protect no one. A good guardian separates the real danger from the distant echo, says plainly why it matters, and lets people spend their attention where it counts.
8. **Freedom to decide.** The guardian advises; people judge. Every warning can be questioned, and every risk can be weighed and consciously accepted. When the guardian itself falters, it steps aside rather than standing in the way.
9. **Freedom for everyone.** Protection isn't a privilege for those who can pay the most. A small team, a school, a community group or a town office deserves the same clear warning as the largest enterprise. What helps society should be open to society.

### What we refuse

- **Chains:** no dependence that cannot be undone.
- **Mystery:** no judgment without a reason.
- **Fear:** we warn honestly; we never sell panic.
- **Secrecy:** nothing about you leaves your hands unless you choose to share it.

### In one breath

> **Security without chains.** See clearly, understand why, and stay free to choose. Gjallar sounds the horn when danger is real; what you do next is always yours.

## How to apply it

### When designing or choosing

Check the option against each freedom and prefer the one that passes more of them:

| Freedom | Question to ask |
|---|---|
| 1. Choice | Can this part be replaced later without rewriting the core or losing data? |
| 2. Origin | Does it work for inputs from any source, or does it assume one vendor or platform? |
| 3. Approach | Is the behaviour available to every interface (UI, CLI, API, automation), or only one? |
| 4. Knowledge | Is the data kept in an open format the user can export and read without us? |
| 5. Place | Does it run small, offline and air-gapped, with no outside account or inbound connection? |
| 6. Identity | Does it use the operator's own identity system, and never grant more than the acting person has? |
| 7. Noise | Does it reduce noise, rank by real impact, and explain each result in one sentence? |
| 8. Decide | Can a human override it with a recorded reason? Does it fail open rather than block everything? |
| 9. Everyone | Could a small team with one engineer run and understand it? Is it open and lightweight? |

Also check the four refusals. An option that adds an undoable dependency (chains), an unexplained score (mystery), alarmist wording (fear) or data leaving the user's environment without consent (secrecy) should be rejected or redesigned.

### When reviewing code or a pull request

Report findings per freedom, only where one is affected. For each: the freedom, what in the change affects it, and the smallest change that would restore it. Say plainly when a change passes. Don't invent concerns to fill the table.

### When writing docs, UI text or release notes

- Warn plainly and specifically; never use fear or urgency for effect.
- Always give the reason behind a judgment (why something ranks high, why it is blocked).
- Leave the decision with the reader: describe options and consequences, not commands.
- Mention how to leave or export when describing where data lives.

### When a request conflicts with the philosophy

Say which freedom or refusal it conflicts with, in one sentence, and offer the closest design that keeps the freedom. If the user still wants it, do it and note the trade-off where future readers will see it (a code comment, the PR description or the docs).