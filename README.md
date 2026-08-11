# CloudFlare Pages linter

> [!CAUTION]
> This project is abandoned and all its updated knowledge base is [embedded into my blog repository](https://github.com/kdeldycke/blog/commit/ff4b7d9679ae6a2fea5781c4874fe505db363a5a).

This project was an attempt to simulate the constraints governing the [redirect rules](https://developers.cloudflare.com/pages/configuration/redirects/) supported by [CloudFlare Pages](https://pages.cloudflare.com).

The rules are obscure and are not all clearly laid down in the documentation. I had to reverse engineer them with experiments, A/B testing and looking at the source code of CloudFlare utilities. My goal was to consolidate all these learnings into a CLI that could lint, autofix and simulate your redirections rules. But I decided to abandon the project before its completion as it was too ambitious for its niche usage.

Still, its knowledge base has been recycled elsewhere and is live at:
- https://kevin.deldycke.com/2022/cloudflare-commands
- https://github.com/kdeldycke/blog/blob/main/tests/pages_redirects_engine.py
- https://github.com/kdeldycke/blog/blob/main/tests/test_redirects.py
- https://github.com/kdeldycke/blog/blob/main/docs/redirects.md
