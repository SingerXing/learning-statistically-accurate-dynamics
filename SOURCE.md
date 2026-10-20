# Source and attribution

Research materials exported individually from the MXM-2026 Overleaf project on October 19, 2026.

The report and figures are preserved without content changes. The Overleaf project was not edited.

Report authors: Daniel Youngberg, Tan Bui, Cody McKenna, and Singer Xing. The report is identified as the MXM Spring 2026 Final Report, University of Wisconsin–Madison.

The initial collection includes the compiled report and its seven figures. The research poster and a code-free methods guide have been added as described below. Computational source code and the original code-containing walkthrough are not included. Reference-paper PDFs and mentors' teaching notes are also excluded; background works remain credited in the report's references.

## Exported files

SHA-256 hashes identify the exact exported files.

| Repository file | Original Overleaf file | SHA-256 |
| --- | --- | --- |
| `report/final-report.pdf` | `Compiled main.tex` | `c4f32eaa5e1887e79a05d66879181403ee883ac5c0347c996d38e61d8d407db3` |
| `figures/autoencoder-results.png` | `Results/autoencoder-results.png` | `b6316ebde4640b2fde42bfeae4fe67df4a8fad7c0b4017f78b1f9b70034af17a` |
| `figures/lstm-results.png` | `Results/lstm-results.png` | `46c9103952a21f430cdaf36ee0f13c8f741cbddb1be02d45c72e9dad5f0b14b7` |
| `figures/FHNLatent.png` | `Results/FHNLatent.png` | `1b8e2dec171845ae70d99a5f6e0126cb2aa5e83dd80aae02d5b8a35605fcc5e6` |
| `figures/FHNvSlice.png` | `Results/FHNvSlice.png` | `876a6f50e2bd554393c04df630155ddf8569dfce99029f6f7b880702c41d7fa3` |
| `figures/FHNuSlice.png` | `Results/FHNuSlice.png` | `0bb02514c9808b12a37998c301400fff4313c3afb44dcf09b844be0dc370adaf` |
| `figures/FHNSpikeStats.png` | `Results/FHNSpikeStats.png` | `fa795d3e5b78282b00340311a69378af7a2e19835cd328ea8352aebf26523a8c` |
| `figures/summary_visual.png` | `Final Visual and Paragraph/summary_visual.png` | `466708cc473fbc25bc7dc22682657e7dd17cfe45d83b741c8b9adab0d63181b6` |

## Explanatory adaptation

`docs/methods-walkthrough.md` was prepared on October 19, 2026 from the locally retained Overleaf source snapshot of `Lorenz_Autoencoder_Walkthrough.tex`, with `main.tex` and `Poster/main_poster.tex` used to check the evidence and implementation status. The live Overleaf file tree and walkthrough section outline were also inspected that day.

This guide is a condensed explanation, not an original research artifact or a complete transcription. It omits Python examples and line-by-line programming commentary, preserves the distinction between results and proposed work, and flags conflicting source details. It does not independently reproduce experiments or establish who wrote particular source files. The original Overleaf documents have not been modified.

## Poster compilation

`poster/research-poster.pdf` was compiled locally on October 19, 2026 from the retained Overleaf source snapshot. It is a one-page, 42 by 32.5 inch poster. The TeX text and all referenced assets were left unchanged. Local file links resolved the source's mixed relative paths; pdfLaTeX and Biber produced the PDF. No shared Overleaf file or compile setting was changed.

The poster credits Tan Bui, Cody McKenna, Singer Xing, and Daniel Youngberg with equal contribution and acknowledges Pouria Behnoudfar and Marios Andreou. Its original wording is preserved, including the explicit statement that full EnKF implementation is future work. The README and methods guide distinguish this proposed stage from the displayed LSTM forecasting results.

Poster PDF SHA-256: `808fd91892b3a895605183011315598d528b3293b4de28be79c99c7bf93d87df`.

Source files used for the local build:

| Original Overleaf file | SHA-256 |
| --- | --- |
| `Poster/main_poster.tex` | `28eb34bf6861aa2983e137f1eec295094e41a4ea2dbd8845c732f23e42ad7cae` |
| `Poster/uwtheme.sty` | `410ccee1cc7d6d63aa70e3cec90d6a013d259d33f256f3cc59cf3286b8477144` |
| `Poster/refs.bib` | `74f55ddee16dc53167c5383e7589ac384f0b345ae68d3fc23492297384b4e5ba` |
| `Poster/uwlogocenter.png` | `40c01e021cc646a84eab9f1c8e41d6fc9fa84970ba0691912c7b129c442200a2` |
| `Poster/LogoA.png` | `83a1cda8f0902cbe9774adede678ec30842f65e50fc79bbfff394e6515c747f6` |
| `Poster/figure/method_diagram.png` | `b4680cb5f48d21b0045052a1408a8585fcf286afd0778e0fba52d3fe31349907` |
| `Poster/results/LabellessFHNResults.png` | `1a500b965abed7a305f26e2041792fd2e57c75e365bb9d167dfd476ca5aeb5d2` |

## Research narrative

`docs/research-narrative.pdf` contains the ten research pages exported on October 19, 2026 from the research tab (`t.is72mosq307v`) in Singer Xing's Google Docs master document. Other tabs and the automatically generated tab divider are excluded.

The wording, figures, and layout are preserved. Ten subscript-t characters that appeared as missing-glyph boxes in Google's PDF export were repaired locally with an embedded font. No Google Docs or shared Overleaf content was edited.

These explanatory working notes include unresolved verification items and accompany the original research materials. They do not establish additional completed experiments; full EnKF implementation remains future work.

Research narrative PDF SHA-256: `0b82808e9651624c1d61a24dd90021ba6dc45ae6416818fd77a8fbbef14c1925`.
