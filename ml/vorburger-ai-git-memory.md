# Vorburger.ch AI Git Memory `aifiles`

Like everyone else, I am increasingly using AI tools.

Today I finally got around to start setting up what will be the (public) "memory" of my personal future AI agents that will work for me.

Being a developer, I don't want this to be hidden away in some proprietary black box, but instead want to be able to inspect, edit, and version control it.

I also don't want it be specific to any one AI tool or provider, but instead be portable and reusable across all of them;
whether that's the (awesome!) [Gemini CLI](https://geminicli.com/), Anthropic's Claude Code, OpenAI's, or my very own [Enola.dev](https://enola.dev/).

While project specific instructions belong into [`AGENTS.md`](https://agents.md) files of the respective projects,
such as e.g. my [🐝 Bee project's AI Agents configuration](https://github.com/enola-dev/be/blob/main/AGENTS.md),
I want certain other AI memory that is specific to myself to be shared across all my projects.

As but one small example, when I talk to my AI about _"MariaDB4j"_ it must know that this is my own open source project,
who's canonical GitHub repo is at https://github.com/MariaDB4j/MariaDB4j (and not https://github.com/vorburger/MariaDB4j, which is just my own fork).

So I created https://github.com/enola-dev/vorburger-ai-assistant for this purpose;
and it's [`git-repos.md`](https://github.com/enola-dev/vorburger-ai-assistant/blob/3776720ba24fb1f060ced2999cdf7f67581b8c35/knowledge/git-repos.md)
to capture the information of the example above.

And [with this change](https://github.com/vorburger/vorburger-dotfiles-bin-etc/commit/58b7eb6b1805f947839a35a63e39e4fa536aaf0f),
my Gemini CLI installation now automatically pulls this information into my AI agents' memory.
(I'll later do something similar for other AI tools I use, too.)

This new repo is basically the AI memory equivalent of my [Linux `dotfiles`](https://github.com/vorburger/dotfiles)!

What shall we call such Git repos? How about everyone's `aifiles`? 😃
