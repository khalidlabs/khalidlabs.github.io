---
title: "Book Condenser"
date: 2025-04-25T00:00:00Z
draft: false
description: "A tool that produces a shortened reading edition of a nonfiction book by extracting the author's own prose — reading less of the book without replacing it with a summary."
tags: ["LLM Applications", "Document Processing", "Open Source"]
categories: ["Projects"]
---

Book Condenser produces a shortened reading edition of a nonfiction book. Its
premise is deliberately narrow: *read less of the book, without replacing the
book with a summary.* Rather than asking a model to rewrite the content, it
identifies and keeps the author's own passages — verbatim — that are needed to
preserve the central question, thesis, key terms, argument, evidence, and
conclusion.

{{< figure src="/projects/book-condenser-pipeline.svg" align="center" alt="Book Condenser pipeline: parse the source, build an analytical map, select verbatim passages, control length and completeness, then render a reading edition." caption="The condensation pipeline. Selection is organized around the book's argument structure rather than chapter coverage, and any bridge inserted between non-contiguous passages is labelled as an editorial transition." >}}

**What it does**

- **Extractive, not generative.** Retained text is quotation-dominant and stays
  word-for-word from the source; the model decides what to keep, not how to
  phrase it.
- **Argument-driven selection.** Passages are chosen against an analytical map of
  the book, and essential propositions are protected together with their
  supporting evidence.
- **Disclosed transitions.** When a bridge is needed for continuity it is
  italicized and labelled — never presented as the author's prose.
- **Traceable output.** It renders a tablet-optimized PDF (plus Markdown and
  optional DOCX) with omission markers, and produces audit artifacts documenting
  the selection decisions.

It accepts EPUB, PDF, DOCX, TXT, and Markdown, with configurable target length
ratios reported against retained source words only.

---

*Code:* [github.com/khalidlabs/book-condenser](https://github.com/khalidlabs/book-condenser)
