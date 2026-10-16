# JPInert

**Engineer. I build automation that runs every day, and I can show you the numbers.**

I majored in programming, spent 10 years building websites in PHP, and wrote C++ programs for years before that. Today I'm the IT engineer people go to for everything: I troubleshoot the network, keep the machines running, own purchasing and get the right hardware to the right person, design MDM profiles and enroll the tablet fleet, and build Grafana dashboards to see problems before users do.

On top of that I design and ship AI-agent systems, at work and at home. Not demos. Real tools with cost routing, permission gates, tests, and production logs behind every claim:

- A voice assistant that handled **238 commands in four weeks, 76% of them with no model call at all**, and asks out loud before it changes anything in the room. Its phone worker now reaches my home, TV, car, mail, calendar and food log through house tools with permission tiers.
- A custom wake word running on a phone's **low-power audio DSP**, built by working out Qualcomm's own model toolchain.
- My own **Tesla Fleet API** app with signed vehicle commands and a watchdog that never polls the car awake.
- Android widgets I **redesign remotely on a phone with no root**, which I wasn't sure could be done.

Everything here is a work in progress. If a README says something works, I ran it. If I didn't, it says so.

## Projects

### The voice stack

Everything here plugs into one voice assistant: say "computer" in the room or to my phone, and it works out what should answer.

| Project | What it is |
|---|---|
| [voice-agent-router](https://github.com/JPInert/voice-agent-router) | The brain of my "computer" voice assistant. Each request goes to the cheapest thing that can handle it: no model, Claude Haiku, or an agent that asks me out loud before it changes anything in the room. Phone requests that match nothing go to a Sonnet worker with permission tiers and a tool registry. Includes a capability map of the devices and accounts it reaches (home, TV, car, mail, calendar, phone, food log) and `soul/`, a local memory layer (hybrid recall, nightly reflection, facts that wait for my yes). About 3 in 4 commands never use a model. |
| [talk2code](https://github.com/JPInert/talk2code) | Talk to a real Claude Code session in my terminal and hear the replies, so I can keep coding away from the keyboard. |
| [android-dsp-wakeword](https://github.com/JPInert/android-dsp-wakeword) | My own "computer" wake word on my phone's low-power audio chip. Screen off, no app, no "Hey Google". |
| [tesla-fleet-voice](https://github.com/JPInert/tesla-fleet-voice) | My own Tesla Fleet API app. Voice commands for the car, and alerts when charging is done or it's left unlocked, without polling it awake. |

### Agents and tools for agents

| Project | What it is |
|---|---|
| [helpdesk-agent-kit](https://github.com/JPInert/helpdesk-agent-kit) | An AI agent for an IT help desk queue: reads Zendesk tickets and their screenshots, looks people up in an admin portal with no API, fixes the common cases in a real browser, and drafts replies a second model checks. A clean-room rewrite of one I built at work, with a mock portal so you can run it. |
| [live-browser-agent](https://github.com/JPInert/live-browser-agent) | Lets an agent see the browser tab I actually have open when a site breaks, without the automation flag that gets you blocked. |
| [claude-code-skills](https://github.com/JPInert/claude-code-skills) | Nine skills from my own Claude Code setup, each keeping the mistakes that shaped it: session handoff, chat branching, a Pi reflash with no card reader, a Debian dual-boot with no USB stick, and more. |
| [codex-image](https://github.com/JPInert/codex-image) | Real image generation for Claude Code through Codex, so it stops drawing icons in code. |

### Everything else

| Project | What it is |
|---|---|
| [gmaps-layers](https://github.com/JPInert/gmaps-layers) | Finds things to do around a Supercharger while we charge. Works for any "X near each Y". |
| [tasker-remote-widgets](https://github.com/JPInert/tasker-remote-widgets) | Car battery widget on my wife's phone that I change from my desktop. No root, no re-importing. Wasn't sure it could be done, it works perfectly. |
| [linux-drills](https://github.com/JPInert/linux-drills) | A hands-on Linux break-fix lab: 41 Docker scenarios that break real boxes (systemd, networking, Docker, GPU) and prove the fix. Every scenario is self-tested before it ships. |
| [userscripts](https://github.com/JPInert/userscripts) | Canned replies for Zendesk with an AI rewrite that never clobbers what I typed, a clipboard history that follows me across every tab, and a read-only Walmart meal-plan helper. |
| [meetcap](https://github.com/JPInert/meetcap) | Live captions of the other side of a call, a jargon panel for technical terms, and notes plus timing metrics afterwards. It records the sound card instead of joining the meeting. Measured on a replayed clip: 6.7 to 8.3% word error, captions about 1.6 to 2.8 s behind. In testing, not yet tried on a real call. |
| [linux-desktop-shell](https://github.com/JPInert/linux-desktop-shell) | The panels I use instead of a desktop panel on a stripped-down XFCE desktop: hover clock and system stats, a network menu, a Home Assistant panel, and a port to KDE Plasma 6 on Wayland. Python, GTK 3, no framework. |

Not published: the phone worker's real device backends and the household-specific parts of the memory layer. What is in the repos is extracted, scrubbed and tested against fakes, and each README says what was not run on real hardware.

## How I build

I work with AI coding agents the way a lead works with a team: I pick the right tool and model for each job, and I own the result.

| Tool | How I use it |
|---|---|
| **oh-my-pi** (my daily driver) | A model-agnostic harness where I set the routing policy myself: each kind of work goes to the model that suits it, and a cheap model never touches the hard problems. Details below. |
| **Claude Code** (Fable and Opus for the heaviest code) | My tool for long builds, extended with my own skills, hooks and a session-handoff system so work survives across chats. The same skills load in oh-my-pi, so nothing I built is locked to one tool. |
| **Codex CLI** (Astra and Sol) | A second agent with its own strengths, including real image generation for app art ([codex-image](https://github.com/JPInert/codex-image)) |
| **opencode** | A second open harness I use to test the same work on open models |
| **Kimi K3, DeepSeek V4 Pro, GLM** | Frontier open-weight models for fast, cheap bulk work and for cross-checking another model's answer |

### Model routing in oh-my-pi

I treat model choice as an engineering decision, the same way the voice router treats it: spend the expensive reasoning only where it pays off.

| Job | Model tier | Why |
|---|---|---|
| Planning and hard debugging | Claude Opus | Mistakes here cost the most, so this gets the strongest reasoning |
| Everyday coding | Claude Sonnet | Fast and strong enough for most edits |
| Commit messages, summaries, quick classification | DeepSeek V4 Flash | Cheap and fast, with Claude Haiku as the backup |
| Reading screenshots and images | A vision-capable Codex model | Routed by capability, not by habit |
| Web lookups | Gemini Flash | Long fallback chain across search providers so a lookup never just fails |

Each role has its own **fallback chain** (for example Opus work falls back to a Codex model, then DeepSeek V4 Pro), and usage-aware fallback switches models before a quota runs dry, keeping 10% in reserve. Long jobs fan out to parallel sub-agents, and my Gmail and Calendar tools plug in over MCP. It is the same idea as the voice assistant above: the cheapest thing that can do the job does it, and a stronger one steps in when it cannot.

The agents write a lot of the code. The engineering is mine: I design the system, break up the work, review every change, test it on the real hardware, and every number in these READMEs comes from my own logs with its sample size.
