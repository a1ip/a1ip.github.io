---
title: LaTeX math formulas in SVG
lang: en
description: Export LaTeX math formulas to SVG with MathJax and ObservableHQ
tags: lifehacks LaTeX SVG Math
categories: en
---

You can easily create LaTeX math formulas in SVG format using [this ObservableHQ notebook][1]

If you need linebreaks, and `\\` does not work for you, then wrap formula into the `\displaylines{}` as suggested [here][2].

![Euler's formula][3]

![arithmetic progression formula][4]

![sin squared sum][5]

[1]: https://observablehq.com/@oberbichler/formulator
[2]: https://github.com/mathjax/MathJax/issues/2312
[3]: https://raw.githubusercontent.com/gist/a1ip/e76cb6c0e6d16370f4ebf7a8e650b434/raw/euler.svg
[4]: https://raw.githubusercontent.com/gist/a1ip/e76cb6c0e6d16370f4ebf7a8e650b434/raw/arithmetic-progression.svg
[5]: https://raw.githubusercontent.com/gist/a1ip/e76cb6c0e6d16370f4ebf7a8e650b434/raw/sin-squared-sum.svg
