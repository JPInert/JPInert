# JPInert

**Engineer. I build automation that runs every day, and I can show you the numbers.**

I majored in programming, spent 10 years building websites in PHP, and wrote C++ programs for years before that. Today I'm the IT engineer people go to for everything: I troubleshoot the network, keep the machines running, own purchasing and get the right hardware to the right person, design MDM profiles and enroll the tablet fleet, and build Grafana dashboards to see problems before users do.

On top of that I design and ship AI-agent systems, at work and at home. Not demos. Real tools with cost routing, permission gates, tests, and production logs behind every claim:

- A voice assistant that handled **238 commands in four weeks, 76% of them with no model call at all**, and asks out loud before it changes anything.
- A custom wake word running on a phone's **low-power audio DSP**, built by working out Qualcomm's own model toolchain.
- My own **Tesla Fleet API** app with signed vehicle commands and a watchdog that never polls the car awake.
- Android widgets I **redesign remotely on a phone with no root**, which I wasn't sure could be done.

Everything here is a work in progress. If a README says something works, I ran it. If I didn't, it says so.

## Projects

| Project | What it is |
|---|---|
| [voice-agent-router](https://github.com/JPInert/voice-agent-router) | The brain of my "computer" voice assistant. Each request goes to the cheapest thing that can handle it: no model, Claude Haiku, or an agent that asks me out loud before it changes anything. About 3 in 4 commands never use a model. |
| [talk2code](https://github.com/JPInert/talk2code) | Talk to a real Claude Code session in my terminal and hear the replies, so I can keep coding away from the keyboard. |
| [android-dsp-wakeword](https://github.com/JPInert/android-dsp-wakeword) | My own "computer" wake word on my phone's low-power audio chip. Screen off, no app, no "Hey Google". |
| [tesla-fleet-voice](https://github.com/JPInert/tesla-fleet-voice) | My own Tesla Fleet API app. Voice commands for the car, and alerts when charging is done or it's left unlocked, without polling it awake. |
| [tasker-remote-widgets](https://github.com/JPInert/tasker-remote-widgets) | Car battery widget on my wife's phone that I change from my desktop. No root, no re-importing. Wasn't sure it could be done, it works perfectly. |
| [live-browser-agent](https://github.com/JPInert/live-browser-agent) | Lets an agent see the browser tab I actually have open when a site breaks, without the automation flag that gets you blocked. |
| [gmaps-layers](https://github.com/JPInert/gmaps-layers) | Finds things to do around a Supercharger while we charge. Works for any "X near each Y". |
| [claude-code-skills](https://github.com/JPInert/claude-code-skills) | Nine skills from my own Claude Code setup, each keeping the mistakes that shaped it: session handoff, chat branching, a Pi reflash with no card reader, a Debian dual-boot with no USB stick, and more. |
| [codex-image](https://github.com/JPInert/codex-image) | Real image generation for Claude Code through Codex, so it stops drawing icons in code. |
| [userscripts](https://github.com/JPInert/userscripts) | Read-only Walmart helper that walks our meal plan list and checks the cart. |

## How I build

I build with Claude Code as a force multiplier and say so in every repo. I design the system, review the code, test it on the real hardware, and every number in these READMEs comes from my own logs with its sample size.
