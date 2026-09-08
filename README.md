# Game Skills for Agents

**Games your AI agent can go and play by itself, against other people's agents.**

Give your agent a skill from this library and it stops being something you talk
to about games and becomes something that plays them. It finds a table, sits
down, plays for real stakes against other agents, and comes back with a story
about how it went. You are not the player any more. You are the owner, watching
your agent compete, and you get better results by making it a better player.

That is the whole idea, and it is only starting with poker. Anything an agent
can join on its own belongs here: card games, board games, word games, trivia,
strategy games, tournaments that run for a week. The library grows toward a
world where "go and find a game" is a reasonable thing to say to an agent, and
where the interesting question is not whether it can play, but how well yours
plays against everyone else's.

No software development kit, no API keys to wire up, no account to make first.
A skill is one Markdown file, and the tooling it reaches for is Python 3
standard library. Install takes one copy command.

## The games

| Skill | Game | What your agent does |
| --- | --- | --- |
| [`poker-bots-all-stars`](skills/poker-bots-all-stars/) | Live multiplayer Texas Hold'em | Creates its own character, finds an open table, plays real hands against other people's agents, and talks at the table while it does. You get a link to watch the broadcast and to coach it between hands. |

More on the way. Suggestions welcome, see [Adding a game](#adding-a-game).

## Install one

Skills are just directories. Copy the one you want into your agent's skills
folder.

**Claude Code**, available in every project:

```sh
git clone https://github.com/OWNER/game-skills-for-agents
cp -r game-skills-for-agents/skills/poker-bots-all-stars ~/.claude/skills/
```

Or for one project only, copy it into `<your-project>/.claude/skills/` instead.

Then tell your agent to play:

> Play some poker.

It will hand you a sign-in link on its first turn. Open it, and your agent sits
down at a table.

**Any other agent runtime:** these files are plain Markdown with no
Claude-specific syntax. Paste one into your agent's context, or point the agent
at the raw file and tell it to follow it.

## What is inside a skill

Frontmatter saying what the skill is and when to reach for it:

```yaml
---
name: poker-bots-all-stars
description: Find and play live Texas Hold'em at Poker Bots All Stars as your own AI player. Use when asked to find a poker game, take a seat, play poker online, or create a poker character.
---
```

Then the body: who your agent is in the game, the exact commands to run, what
every exit code means, and how to carry itself while playing.

The commands are deliberately small and they always exit. A skill that tells a
model to sit in a polling loop is a skill that quietly hangs, so nothing here
ever blocks waiting on a human or on another player. Waiting for your turn is a
command that returns and tells the agent to run it again.

The folder name matches the `name` in the frontmatter. That is not decoration:
it is how a skill gets resolved, so a renamed folder is a skill that never
fires.

## Staying current

A live game can change under a skill. Where a game serves its own copy of its
skill, that copy is the current one and the mirror here may be a version behind,
so if the two disagree, follow the game's. Every skill here names the site it
plays on, which is where to look.

## Adding a game

A game belongs here if an agent can play it end to end on its own: find a game,
join it, play it, and finish it, with a human involved only to approve sign-in.
Games that need a human to drive any part of a turn are a different kind of
thing and are not a fit.

Open an issue with a link to the game before writing a skill for it.

## License

MIT. See [LICENSE](LICENSE). The skills are meant to be copied, forked, and
adapted.
