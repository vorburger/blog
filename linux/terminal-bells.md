# Terminal Bells: From Noise to Notifications

I've finally fixed my terminal notification workflow. For a long time, I had terminal bells completely silenced because they were just too "noisy." But I recently realized I was missing out on a very useful feature: being notified when a long-running background task finishes.

The problem was two-fold:
1. **Accidental Bells:** Every time I scrolled past the end of a file in `less` (which is used by `git`, `bat`, `rg`, etc.), my terminal would "ring." This was annoying and made me disable bells everywhere.
2. **Silenced tmux:** Because of the noise, I had `set -g bell-action none` in my `.tmux.conf`.

I recently changed this in my [dotfiles](https://github.com/vorburger/dotfiles/commit/ed6a1dadbb9ed8172762df648518059c81c6dd71) to make bells actually useful.

### 1. Silencing the "Noise" (Pagers)

The first step was to tell `less` to be quiet. You can do this with the `-q` (or `--quiet`) flag. This prevents it from ringing the bell for common "errors" like hitting the end of a buffer.

I added this to my shell environment and tool configurations:

```bash
export LESS="-R -q"
```

And for tools that use their own pagers or wrappers:
- **bat**: Use `--pager "less -RF -q"`
- **git**: Configure `core.pager` to include `-q` for `delta` or `less`.

### 2. Enabling Bells in tmux

With the accidental bells gone, I could safely re-enable them in `tmux` so they actually reach my terminal emulator:

```tmux
# .tmux.conf
set -g bell-action any
```

### 3. Triggering Notifications for Long-Running Tasks

Now that the plumbing is working, I can use it for actual notifications. For example, in the Gemini CLI, I added hooks to trigger a bell and even play a system sound when an agent finishes its work:

```json
// .gemini/settings.json
{
  "hooks": {
    "Notification": "printf '\\a' && paplay /usr/share/sounds/freedesktop/stereo/message.oga",
    "AfterAgent": "printf '\\a' && paplay /usr/share/sounds/freedesktop/stereo/complete.oga"
  }
}
```

Now, instead of constantly checking my terminal to see if a background task is done, I get a nice subtle sound (and a visual indicator in my terminal/tmux status bar) only when it's intentional.
