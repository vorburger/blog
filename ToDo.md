# ToDo

1. Fix broken relative links... e.g. on https://blog3.vorburger.ch/security/ssh-tpm/
   the https://blog3.vorburger.ch/security/ssh-tpm/ed25519-sk.md is wrong.

1. Add link to GitHub repo or even direct article - surely Hugo has this built-in, like mkdocs?

1. Is http://blog3.vorburger.ch OK now? DNS resolves? HTTP reachable, returns 200, shows this `./site/index.html` ?
   created:2026-03-30 due:2026-03-31 completed:2026-03-31

1. Restructure `/images/` ... because as-is now, the
   linux/coreos/README.md and
   linux/dappnode/README.md are both
   static/images/README.png - which is bad.

1. Import all the old posts from both http://blog2.vorburger.ch as well as https://github.com/vorburger/TEMPLATE .. they were on Blogger, which I think has an Export somewhere - in what format? It will need to be transformed into our MD, with the required fields in the YAML header.

1. Make `./build` script validate all links (internal and external) that are reachable from the generated `site/index.html` with a suitable CLI tool; ideally one that caches external links for a little while.

1. Better AI image generation

1. Prettier HTML layout template
