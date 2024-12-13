# GitHub Pages on Custom Domains required `github.io` instead of `github.com` DNS

My personal homepage <https://www.vorburger.ch> is hosted on the [GitHub Pages](https://pages.github.com/) Content Delivery Network (CDN).

Tonight while I was having dinner, the uptime monitoring I set up for it using [Cronitor.io](https://cronitor.io/) (great product!) started firing 🚨 alerts - homepage down!

After poking around my domain registrar, DNS server and GitHub, I noticed, somewhat by chance, that I have been, since a very long time, using a `CNAME` of `vorburger.github.com` for `www.vorburger.ch`. This has been working since mid-2012, 12+ years!

But apparently, at some point, GitHub decided that _Pages_ would need to use `.github.io.` instead of `.github.com.` as CNAME... thanks for (not) notifying your customers about this!

It seems like 1h ago today (on 2024-12-13 at 11 AM on PST) they turned down serving GitHub Pages from `.github.com.` CNAMEs. And broke my homepage. And perhaps if you are reading this, your website too?

Adjusting it in my [zonefile](https://en.wikipedia.org/wiki/Zone_file) fixed it; phew - disaster 🌋 averted. With ~1h total from detection to mitigation. (Depending on DNS cache, due to 1h TTL.) That's not a bad service turn around, for an ancient personal website which nobody reads; I'm giving myself 7 stars out of 5 for this quick remediation! 😆 (Other sites need faster mitigation; but when those alert you, then you do not finish eating your dinner, first.)

But the fact that this "just happened", without any prior heads up from GitHub, is not cool. They could have easily found customers still using the old CNAME, and notified them, with a grace period to switch.
