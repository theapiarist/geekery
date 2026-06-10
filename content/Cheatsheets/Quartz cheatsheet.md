---
title: Quartz cheatsheet
created:
updated:
draft: "false"
tags:
  - quartz
---
[Full installation instructions](https://quartz.jzhao.xyz/getting-started/installation)

## Configuration file changes

`nano quartz.config.yaml` [^1]

## Custom CSS

`nano ./quartz/styles/custom.scss`

## Serve locally for testing

`npx quartz build --serve`

## Sync the site to Github

`npx quartz sync`

Or `npx quartz sync --commit` if you want to add a commit message

%%

## Check for broken links

`npx linkinator --recurse --silent http://localhost:8080`
%%

[^1]: These assume you are in the root directory of your quartz installation