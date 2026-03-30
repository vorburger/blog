# Parallelizing Agentic Coding: Supercharging AI Workflows with Terminal Notifications

The real power of AI-assisted development isn't just having an agent write code for you; it's the ability to *parallelize* your workflow. When you assign a complex, multi-step refactoring task or a deep codebase investigation to a tool like the Gemini CLI, you shouldn't just sit there watching the terminal output scroll by. You should be switching to another pane to write documentation, review PRs, or tackle another problem entirely while the agent grinds away in the background.

But this "fire and forget" workflow introduces a new problem: how do you know when the agent is actually finished and needs your review? Constantly context-switching back to check on it defeats the purpose of parallelizing your work.

The solution is delightfully retro: the terminal bell (`\a`).

By configuring the Gemini CLI to trigger a system sound when an agent finishes its execution, you can completely ignore its terminal pane until you hear the chime.

### Setting up AI Notifications

I recently updated my [dotfiles](https://github.com/vorburger/dotfiles/commit/ed6a1dadbb9ed8172762df648518059c81c6dd71) to make this work seamlessly.

First, I added lifecycle hooks to my Gemini CLI configuration so it plays a pleasant notification sound when it finishes a task or throws a notification:

```json
// .gemini/settings.json
{
  "hooks": {
    "Notification": "printf '\\a' && paplay /usr/share/sounds/freedesktop/stereo/message.oga",
    "AfterAgent": "printf '\\a' && paplay /usr/share/sounds/freedesktop/stereo/complete.oga"
  }
}
```

Next, because I heavily use `tmux` to manage my parallelized workspaces, I needed to ensure that bells ringing in background windows would actually reach my terminal emulator. Changing `bell-action` passes the signal through to my host OS:

```tmux
# .tmux.conf
set -g bell-action any
```

Now, I kick off an agent, switch to another window, and keep working. When I hear the "complete" chime, I know my AI pair programmer has finished its task.

---

### Appendix: Taming the Noise (Silencing Pagers)

If you've ever had terminal bells enabled globally, you probably turned them off because they are incredibly annoying. The biggest culprit is usually your pager (`less`), which is used under the hood by `git`, `bat`, `rg`, and others. By default, `less` throws a terminal bell every single time you accidentally scroll past the end of a buffer or hit an invalid key.

If you want your AI notifications to actually mean something, you have to eliminate these "false positives."

You can tell `less` to be quiet by exporting the `-q` (or `--quiet`) flag in your shell environment:

```bash
export LESS="-R -q"
```

For tools that wrap or configure their own pagers, you'll need to pass the flag explicitly:
*   **bat**: Use `--pager "less -RF -q"`
*   **git**: Configure your `core.pager` (whether it's `delta` or `less`) to include `-q`.

With the pager silenced, the terminal bell transforms from a source of constant frustration into a highly effective, asynchronous notification system for agentic workflows.
