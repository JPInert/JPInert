# JPInert

I work in IT support and build automation on the side, mostly with AI agents. I care most about whether a thing is cheap to run, safe, and still working a month later. Most of these started as something I wanted at home.

Everything here is a work in progress. If a README says it works, I ran it. If I didn't, it says that.

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
| [codex-image](https://github.com/JPInert/codex-image) | Real image generation for Claude Code through Codex, so it stops drawing icons in code. |
| [userscripts](https://github.com/JPInert/userscripts) | Read-only Walmart helper that walks our meal plan list and checks the cart. |

## How I build

I build with Claude Code and say so in every repo. I decide what it should do, test it on the real thing, and the numbers in the READMEs come from my own logs.
