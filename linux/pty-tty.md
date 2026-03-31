---
title: 'Fun with Pseudo-Terminals (PTY) & TTY ("Teletypewriter") over `socat` & `websocat`'
date: 2025-05-25
tags: ["linux"]
image: "/images/placeholder.png"
---

# Fun with Pseudo-Terminals (PTY) & TTY ("Teletypewriter") over `socat` & `websocat`

In the context of [Enola.dev #1368](https://github.com/enola-dev/enola/issues/1368),
I recently learned a few things related to [`openpty`](https://man.archlinux.org/man/openpty.3) and
how to execute a program under a _"pseudo (virtual) terminal"_ so that it e.g. prints ANSI color codes,
and allows interactive control, like a Shell or Editor requires.

## socat

[`socat`](http://www.dest-unreach.org/socat/), the _"better netcat++"_ is one way do this. In one Terminal, run:

    socat file:/dev/tty,raw,echo=0 tcp-listen:12345

In another Terminal, run:

    socat tcp-connect:localhost:12345 exec:'/bin/bash -li',pty,stderr,setsid,sigint,sane

The former can now use the latter - with working ANSI escape sequences and keystrokes.
(You might need to `export TERM=xterm-256color`, if that's not already set.)

Just the terminal size won't be correct: `echo $LINES $COLUMNS` (likely) will show the default `24 80`.
Running `stty` over socat will also show that default. But running it "locally" and then "fixing" it with `stty rows 24 cols 182` can do the trick.
Unfortunately with socat it's difficult to do this automagically on connect, or even continuously on resize.

PS: `file:/dev/tty` is easier than `$(tty)`
or `file:``tty``` (which is Bash specific and does not work in Fish, and is also difficult to render correctly in Markdown).

## websocat

https://github.com/vi/websocat is a cool `socat`-like tool which would allow to do something similar to above but over `ws://` WebSocketss.

## Alternatives

SSH automatically handles all aspects of TTY allocation, environment propagation (`$TERM`), and
window resizing ([`SIGWINCH`](https://www.rkoucha.fr/tech_corner/sigwinch.html) to `TIOCGWINSZ`, `TIOCSWINSZ`, `TIOCSCTTY`).
(For Enola.dev's planned _"AI Shell",_ I might persue this avenue further.)

Another option would be a custom TTY binary, written e.g. with Python's `pty` and `termios` (minimally even just `python -c 'import pty; pty.spawn("/bin/bash")'`),
or in Go (e.g. with https://github.com/creack/pty; or https://github.com/mattn/go-tty),
or in Rust (with `nix` and `tokio` crates),
or even in Node.js (with [`node-pty`](https://github.com/microsoft/node-pty)),
or even Java with [Pty4J](https://github.com/JetBrains/pty4j),
which catches SIGWINCH and somehow sends the terminal dimensions over to the remote process,
which then performs the TIOCSWINSZ ioctl.

Such tools obviously already exist, and are sometimes referred to as "remote shells" (or "[web shells](https://github.com/vorburger/cloudshell)")
or "reverse shell" or "bind shell" when they are associated with "penetration testing" (AKA PenTest) [or worse] related projects:

* https://github.com/b23r0/cliws 🇨🇳
* https://github.com/topics/reverse-shell, like:
  * https://github.com/NHAS/reverse_ssh
  * https://github.com/Fahrj/reverse-ssh
* https://gtfobins.github.io
