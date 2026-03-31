---
title: "NixCon 2025"
date: 2025-09-07
tags: ["conferences"]
image: "/images/placeholder.png"
---

# NixCon 2025

I've attended https://2025.nixcon.org in Rapperswil-Jona near Zürich in Switzerland, and here are some thoughts about it, written up on my way home.

Nix is several things:

* an interesting but at least initially to me a bit scary _functional_ [configuration language](https://github.com/vorburger/LearningLinux/blob/develop/nix/bookmarks.md#configuration-language)
* a package 📦 manager (like `apt` or `dnf`), which can be used on any Linux distro, as well as on 🍎 Macs (like Homebrew 🍺 `brew`)
* a _declarative_ Linux distro called NixOS (like Fedora, Ubuntu or Debian)

This may be one part of what makes it a little hard to grasp in the beginning. Other parts could be the at least initially somewhat confusing old (`nix-*` commands) vs. new ([Flakes](https://vtimofeenko.com/posts/practical-nix-flake-anatomy-a-guided-tour-of-flake.nix/); and `nix …` commands) usage styles, the several docs sites (and [Wiki](https://nixos.wiki/wiki/NixOS_Wiki:History)), and different ways of doing many things. On the other hand, perhaps some of this “I need to figure out things for myself like I used to on my first 8bit home computer” (if you’re old enough to remember?) is also what appeals to people interested in Nix? ✅ Check for myself personally! 😆

I'm quite new to nixing, but what I've seen and learned at this conference, both technical and cultural, made me want to continue learning more about and start using it. The learning curve is certainly non-trivial, but it seems fun, and it's the best answer for package management hell, across distros and platforms, that I know of.

I've attended this conference in a personal capacity, not representing the company that currently employs me. There were several other people working at said same company attending as well, and it was great fun to chat with some of them; including hearing about how https://firebase.studio uses Nix (instead of Dockerfile) to build its containers.

The conference was held at a university on an absolutely gorgeous campus that's directly on a lakeside, with a Mountain View. It still felt very "grassroots" (in a good sense), and “diverse” in more than one aspect - both 🌈 people attending, and because of booths of a variety of small consulting companies, but with no single dominant main vendor; personally I quite liked seeing this. This is open source at its best!

It was good fun, and great learning of Nixacious magic incantations for me, to hack together with Artem (Thank You!) on making [my Enola.dev project available a Nix flake](https://docs.enola.dev/use/#nix). Combining Bazel with Nix, which I personally view as fairly complementary, turns out to be [a lot more “fun” (cough) than one would have thought at first](https://github.com/enola-dev/enola/issues/1713#issuecomment-3262363532)!

Thank You 🙏 to https://leona.is for having patiently answered my Noobie “so how would I get started with home manager if I have an existing dotfiles repo” question during Hack Sunday. Our parting exchange, my Q: “So how do you use Nix?” - unassuming A: “Oh, I'm release manager for NixOS 25.05”, with a “and doing a great job at it!” shout-out from across the room was… well yeah, open source at its best.

I've run into other kind random strangers like [@thefossguy](https://github.com/thefossguy) and @Pol [offering to answer](https://mathstodon.xyz/@Pol/115168596288038824) any Nix questions you might have.

I'm keeping [some Nix related bookmarks here](https://github.com/vorburger/LearningLinux/blob/develop/nix/bookmarks.md).

Some things I'd like to follow up on at home, time permitting:

1. Ponder if I could hack a MVP POC of a simple incremental build tool using Nix packages
1. Nix [my dotfiles](https://github.com/vorburger/vorburger-dotfiles-bin-etc) with Home Manager (WIP)
1. Continue adopting Nix [in (my) Enola.dev project](https://github.com/enola-dev/enola/blob/main/flake.nix)
1. Finally get around setting up that long planned Home NAS with ZFS, now definitely using NixOS - of course
1. Try out https://clan.lol

PS: Also start a new project (ANY project, really), with an awesome 😆 `.lol` TLD!
