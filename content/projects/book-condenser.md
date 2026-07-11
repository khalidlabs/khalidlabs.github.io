---
title: "Book Condenser"
date: 2026-03-10T00:00:00Z
draft: false
description: "A tool that produces a shortened reading edition of a nonfiction book by extracting the author's own prose. The goal is to read less of the book without replacing it with a summary."
tags: ["LLM Applications", "Document Processing", "Open Source"]
categories: ["Projects"]
---

Book Condenser produces a shortened reading edition of a nonfiction book. Its
premise is narrow. The goal is to read less of the book without replacing the
book with a summary. Rather than asking a model to rewrite the content, it
identifies and keeps, word for word, the passages needed to preserve the
central question, thesis, key terms, argument, evidence, and conclusion.

**What it does**

- **Extractive, not generative.** Retained text stays word for word from the
  source. The model decides what to keep, not how to phrase it.
- **Argument-driven selection.** Passages are chosen against an analytical map
  of the book, and essential propositions are kept together with their
  supporting evidence.
- **Disclosed transitions.** When a bridge is needed for continuity, it is
  italicized and labelled, and it is never presented as the author's prose.
- **Traceable output.** It renders a tablet-optimized PDF (plus Markdown and
  optional DOCX) with omission markers, and produces audit artifacts
  documenting the selection decisions.

It accepts EPUB, PDF, DOCX, TXT, and Markdown, with configurable target length
ratios reported against retained source words only.

---

*The code is at* [github.com/khalidlabs/book-condenser](https://github.com/khalidlabs/book-condenser).
