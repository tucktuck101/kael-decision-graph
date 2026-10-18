# Kael's Decision Graph

How Kael, a D&D character, decides what to do when he meets a creature: whether to flirt, fight, befriend, tolerate or panic. Every path ends in one of five punchlines:

| Ending | |
|---|---|
| **E1** | Keep flirting, it might still work |
| **E2** | Prepare new character sheet |
| **E3** | New bestie! |
| **E4** | Kill them |
| **E5** | Tolerate them |

## ▶ [Open the interactive graph](https://tucktuck101.github.io/kael-decision-graph/)

## What the app does

- **Walk**: go through an encounter one question at a time.
  - It answers "Resume combat objective" and "Who were they?" for you, based on the walk so far.
  - It applies party score changes as you go.
  - Where a party member's score decides the answer, it highlights that answer.
  - **Back**, or clicking any earlier step, undoes everything after it, including score changes.
- **Map**: the full diagram, or one section at a time.
  - Pan, zoom and search.
  - Click a node to see where it comes from and where it leads, or to start walking from there.
  - Your current walk is highlighted.
- **Party**: a relationship score for each party member, saved in your browser.
  - The header shows a health check that runs on every load. It confirms every node can be reached and every path reaches an ending.

## Party relationship score

Each party member has a score from -5 to +5, starting at 0. Kael's possible children who are adult party members start at +5.

| Event | Change |
|---|---|
| Cockblock | -2 |
| Annoyance | -1 |
| Favour (including dragging Kael out of a death fight) | +1 |
| Wingman | +2 |
| Saved his life | +5 |
| A week with no new strikes | +1 |
| Physically attacks him | -5 |

At **+5**, a party member who isn't hostile is Kael's bestie. At **-5 or lower**, Kael casts Vicious Mockery and then fights them to the death. Surrender is ignored, and he hunts them if they flee. Only another party member dragging him away can stop it, which puts their score back to -4.

## Files

| File | Purpose |
|---|---|
| [`kael-decision-flowchart.md`](kael-decision-flowchart.md) | The source of truth: a Mermaid flowchart, which GitHub renders on this page. |
| [`index.html`](index.html) | The interactive app. It loads the `.md` above, so editing the diagram updates the app. |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are. |

### Walker rules

The lines at the top of the Mermaid block that start with `%% @` are comments, so Mermaid ignores them. The app reads them to know:

- where combat intent is set (`@set`) and where routing depends on it (`@dispatch`)
- the score events (`@event`) and where scores change (`@score`, `@target`)
- which answers the score can suggest (`@check`)

If you rename or remove a node, update the matching `@` lines. The health check flags any rule that points at a missing node or answer.

## Running locally

Browsers block a page opened straight from disk from loading the `.md`, so serve the folder instead:

```sh
python3 -m http.server
# then open http://localhost:8000
```
