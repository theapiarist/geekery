---
created: 2026-05-12
tags:
  - obsidian
  - kiln
  - goatcounter
draft: "true"
---
If you use [Kiln](https://kiln.talesign.com/) to generate a static site from your [Obsidian](https://obsidian.md/) vault you can embed a simply pagecounter using [Goatcounter](https://www.goatcounter.com). Simply paste the following code into the footer of your page (or —&nbsp;better —&nbsp;add it to a template, so you don't forget it):

```
<img src="https://WEBSITE.goatcounter.com/count?p=/{{title}}">
```

You need to have an account on Goatcounter, and use the site identifier in place of WEBSITE. In the published page the code is invisible. The handlebars \{\{title}} is replaced by the post title.

