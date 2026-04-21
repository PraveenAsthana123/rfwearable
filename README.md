# RF Signal-Based Wearable Devices for Diagnosis of Multiple Diseases

Review paper covering FMCW, UWB, mmWave, and Microwave sensing technologies for multi-disease health monitoring (2023-2025).

## Three Paper Versions

| Version | Organization | Pages | Target Journal |
|---------|-------------|-------|---------------|
| **A** — Disease-Centric | Organized by disease, RF tech compared within each | 11 | IEEE Sensors Journal |
| **B** — Technology-Centric | Organized by RF technology, diseases within each | 10 | IEEE Sensors Journal |
| **C** — Pipeline-Centric | Follows signal processing pipeline end-to-end | 9 | IEEE Sensors Journal |

## Structure

```
rf-wearable-papers/
├── version-a/
│   ├── rf-wearable-review-A.tex    # Disease-Centric paper
│   ├── rf-wearable-review-A.pdf    # Compiled PDF
│   └── figures/                     # 300 DPI page exports
├── version-b/
│   ├── rf-wearable-review-B.tex    # Technology-Centric paper
│   ├── rf-wearable-review-B.pdf
│   └── figures/
├── version-c/
│   ├── rf-wearable-review-C.tex    # Pipeline-Centric paper
│   ├── rf-wearable-review-C.pdf
│   └── figures/
├── PAPER_QUALITY_POLICY.md          # Quality standards
└── README.md
```

## Key Features

- IEEE two-column format (IEEEtran class)
- 300 DPI image quality (IEEE submission standard)
- TikZ vector figures (taxonomy, flowcharts, bar charts, radar charts, heatmaps)
- Mathematical/statistical analysis (ANOVA, Pearson correlation, Cohen's d, CI)
- 6 disease categories: Cardiac, Respiratory, Diabetes, Cancer, Neurological, Sleep
- 4 RF technologies: FMCW, UWB, mmWave, Microwave Imaging

## Compile

```bash
cd version-a   # or version-b, version-c
pdflatex rf-wearable-review-A.tex
pdflatex rf-wearable-review-A.tex   # run twice for references
```

## Export 300 DPI Images

```bash
pdftoppm -png -r 300 rf-wearable-review-A.pdf figures/page
```

## Authors

- Deepa Asthana
- Praveen Asthana
