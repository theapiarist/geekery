---
title: Nice tables in Ghost's 'Dawn' theme
created:
updated:
draft: "true"
tags:
---
I use a modified version of Ghost's Dawn theme for a website. It's a little bit plain and boring, but that's the point as it doesn't distract too much from the writing.

However, inserted Markdown tables are a mess. If they have any significant amounts of data in each cell you need to scroll horizontally to read the entire line.

Alternatively, inject the following CSS code to the page header (*via* Post settings … Code injection) and the table will be nicely formatted.

```

<style>
  .gh-content table {
    width: 100%;
    border-collapse: collapse;
    margin: 1.75em 0;
    font-size: 0.92em;
    line-height: 1.45;
    table-layout: auto;
  }
  .gh-content table th,
  .gh-content table td {
    white-space: normal;
    word-break: normal;
    overflow-wrap: break-word;
    hyphens: none;
    padding: 10px 14px;
    vertical-align: top;
    text-align: left;
    border-bottom: 1px solid #e5e5e5;
  }
  .gh-content table th {
    border-bottom: 2px solid #333;
    font-weight: 600;
  }
  .gh-content table tbody tr:last-child td {
    border-bottom: 1px solid #333;
  }
  @media (max-width: 720px) {
    .gh-content table {
      display: block;
      overflow-x: auto;
      -webkit-overflow-scrolling: touch;
    }
  }
</style>


```