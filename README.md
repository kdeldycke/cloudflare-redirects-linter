# Cloudflare redirects linter

> [!CAUTION]
> This project is abandoned, but now lives as part of [kdeldycke/repomatic](https://github.com/kdeldycke/repomatic): starting with repomatic `7.13.0`, `repomatic lint-repo` audits every committed `_redirects` file with a faithful Python replica of the engine Cloudflare Pages actually runs, and fails on the rules production would silently drop.

This project was an attempt to simulate the constraints governing the [redirect rules](https://developers.cloudflare.com/pages/configuration/redirects/) supported by [Cloudflare Pages](https://pages.cloudflare.com).

The rules are obscure and are not all clearly laid down in the documentation. I had to reverse engineer them with experiments, A/B testing and looking at the source code of Cloudflare utilities. My goal was to consolidate all these learnings into a CLI that could lint, autofix and simulate your redirection rules. But I decided to abandon the project before its completion as it was too ambitious for its niche usage.

The dangerous part turned out to be exactly what this project existed for: the engine's undocumented budget accounting means a rule's *position* decides whether it exists at all, `wrangler pages deploy` prints nothing when the parser drops rules or abandons the file, and a dead redirect looks exactly like a URL nobody visits. My own site lost its last 18 rules for years this way.

Its knowledge base has been recycled elsewhere and lives on at:

- [`repomatic/pages_redirects.py`](https://github.com/kdeldycke/repomatic/blob/main/repomatic/pages_redirects.py): the engine replica (parsing, budget accounting, matching semantics), transcribed from the reference implementation in [cloudflare/workers-sdk](https://github.com/cloudflare/workers-sdk) and enforced by the `pages-redirects` check of `repomatic lint-repo`.
- [Cloudflare Pages guide](https://kdeldycke.github.io/repomatic/cloudflare.html): the engine as it actually is, written up, silent budget abort included.
- [`tests/test_redirects.py`](https://github.com/kdeldycke/blog/blob/0f18cbdd7404800725a826b620281a03d38a716f/tests/test_redirects.py) in [kdeldycke/blog](https://github.com/kdeldycke/blog): the live-probing suite auditing a twenty-year URL inventory against production, with [`docs/redirects.md`](https://github.com/kdeldycke/blog/blob/0f18cbdd7404800725a826b620281a03d38a716f/docs/redirects.md) telling that inventory's story.
- [Cloudflare commands § Pages redirects](https://kevin.deldycke.com/2022/cloudflare-commands#pages-redirects): the 2022 findings that started it all.
