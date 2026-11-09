# NEI Explorer

Interactive scatter of every tabulated index of the 165 networks (63 non-road, 102 road) in
*Inconsistency of network embeddings beyond degrees and modules* (G. Gim and S. H. Lee).

**Open `index.html`** (or the GitHub Pages site) to:

- choose any index for the x and y axes, with log or linear scales and presets for the figures of the paper;
- switch category layers on and off (20 categories with the manuscript markers and colours of SM Sec. I),
  per group (non-road / road) or one at a time;
- show the reference layers y = x and x = 1, y = 1, and outline the BH-significant networks;
- find a network, or click a point to list all of its indices;
- read the number of points shown, Spearman ρ, and the medians of the points on screen.

## Data

| file | content |
|---|---|
| `data/nei_indices.csv` | one row per network, all indices (165 × 52) |
| `data/nei_data.js` | the same, with the variable registry and the category styles, loaded by `index.html` |
| `data/changes_tex1102_vs_pdf.csv` | cells that differ between the 2026-11-02 LaTeX source and the 2026-11-09 PDF |

Sources, built by `build_data.ipynb`:

- **Values:** the manuscript PDF of 2026-11-09 (Tables S2, S3, S4, S6, S8), read with `pdftotext -layout`.
- **Row order, category headers, markers and colours:** the LaTeX source of 2026-11-02 (SM Sec. I `\cat` list, `\definecolor`).
- **Block-model nulls (`I_sbm`, `I_dcsbm`, `C_sbm`, `C_dcsbm`):** the `tab:sbm-null` table of the LaTeX source.
  That table is not printed in the PDF. Its rows are left empty for inf-USAir97 and ia-primary-school, whose
  real-network estimates changed after 2026-11-02.

Derived: ⟨k⟩ = 2E/N, √𝓘_real, √𝓢_real/𝓘_real, and 𝓘_intra/𝓘_inter (real network).

## Rebuild

```bash
jupyter nbconvert --to notebook --execute --inplace build_data.ipynb
```

Set `TEX` and `PDF` in the first code cell to the manuscript files. The notebook stops if a category count differs
from the SM text, if a row cannot be found in the PDF, or if the tabulated ratios disagree.

Plotly.js 2.35.2 is loaded from jsDelivr; everything else is in this repository.
