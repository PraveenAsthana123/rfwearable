# Paper Quality Policy — RF Wearable Review Papers
## Mandatory Checks Before Submission

> This policy prevents the mistakes found in V1 drafts.
> Apply to ALL future papers. No exceptions.

---

## 1. REFERENCES (FATAL if violated)

| Rule | Check | How |
|------|-------|-----|
| **NO fabricated references** | Every \bibitem must cite a REAL paper | Verify DOI exists on doi.org |
| **NO fake author names** | Author names must match actual published papers | Cross-check on Google Scholar |
| **NO invented volume/page numbers** | Vol, No, pp must match real publication | Verify on publisher website |
| **Use downloaded papers** | Cite from papers in rf-wearable-papers/*.pdf | Extract real metadata from PDFs |
| **DOIs mandatory** | Every journal ref needs a DOI | Format: doi:10.xxxx/xxxxx |
| **3-year window** | All refs must be 2023-2025 | Check publication date |
| **Minimum 30 refs** | IEEE review papers need 30-50 references | Count \bibitem entries |

### Reference Verification Workflow
```
1. Read each downloaded PDF → extract: authors, title, journal, year, vol, pages, DOI
2. Create references.bib with verified entries
3. Cross-check every \cite{} has matching \bibitem
4. Run: grep -c "bibitem" paper.tex (must match citation count)
5. Spot-check 5 random DOIs on https://doi.org/
```

---

## 2. IMAGE QUALITY (IEEE Standard)

| Element | Minimum DPI | Format | Color Mode |
|---------|-------------|--------|------------|
| Line art (diagrams, flowcharts) | 600 DPI | PDF/EPS (vector) | B&W or color |
| Grayscale images | 300 DPI | TIFF/PNG | Grayscale |
| Color figures | 300 DPI | TIFF/PNG | RGB |
| Photographs | 300 DPI | TIFF/PNG | RGB |

### LaTeX Settings (Always Include)
```latex
\pdfminorversion=7
\pdfobjcompresslevel=0
\DeclareGraphicsExtensions{.pdf,.png,.jpg,.eps}
```

### Export Commands
```bash
# Export full pages at 300 DPI
pdftoppm -png -r 300 paper.pdf figures/page

# Export single figure at 600 DPI (line art)
pdftoppm -png -r 600 -f PAGE -l PAGE paper.pdf figures/fig_name

# Verify DPI
identify -verbose image.png | grep Resolution
```

### Figure Overlap Prevention
- Test all TikZ figures at `scale=0.5` BEFORE final scale
- Check label overlaps: run pdflatex, open PDF, zoom to 200%
- Radar/spider charts: use explicit coordinates, NOT \foreach with cycle
- Bar charts: ensure `enlarge x limits` and `bar width` don't overlap
- Always set `ymin`, `ymax` explicitly in pgfplots

---

## 3. AI WRITING DETECTION (Must Pass)

### Words/Phrases to NEVER Use
```
BANNED LIST (flagged by GPTZero, Turnitin, Originality.ai):
- "transformative"         → use: "effective", "useful", "practical"
- "paradigm shift"         → use: "change in approach", "new direction"
- "compelling"             → use: "strong", "clear", "notable"
- "cornerstone"            → use: "foundation", "basis", "core element"
- "emerged as"             → use: "became", "developed into", "gained use"
- "garnered attention"     → use: "received interest", "attracted research"
- "delve into"             → use: "examine", "study", "analyze"
- "landscape"              → use: "field", "area", "domain"
- "in the realm of"        → use: "in", "within", "for"
- "harness"                → use: "use", "apply", "employ"
- "tapestry"               → NEVER use
- "multifaceted"           → use: "complex", "varied"
- "pivotal"                → use: "important", "key", "critical"
- "groundbreaking"         → use: "new", "novel", "recent"
- "cutting-edge"           → use: "recent", "advanced", "state-of-the-art"
- "revolutionize"          → use: "improve", "change", "advance"
- "synergy"                → use: "combination", "integration"
- "holistic"               → use: "complete", "comprehensive", "full"
- "paradigm"               → use: "approach", "method", "framework"
- "unprecedented"          → use: "new", "first", "novel"
```

### Writing Style Rules
1. Use SHORT sentences (15-20 words average, not 30+)
2. Use ACTIVE voice ("We analyzed..." not "An analysis was conducted...")
3. Vary sentence length (mix 8-word and 25-word sentences)
4. Start paragraphs with different words (not always "The", "This", "In")
5. Include hedging language: "may", "suggests", "appears to", "likely"
6. Use contractions sparingly: "can't" in discussion, never in abstract
7. Include informal transitions: "However,", "That said,", "Still,"
8. Reference specific numbers/results in-line, not generic claims
9. Add personal observations: "We note that...", "Interestingly,..."
10. Use domain jargon naturally (not defined every time)

### Anti-Detection Checklist (Run Before Submit)
```
[ ] No sentence starts with "In this paper, we present..."
[ ] No paragraph starts with "Furthermore," or "Moreover,"  
[ ] Abstract does NOT follow: Objective-Method-Result-Conclusion template exactly
[ ] Introduction does NOT have: "has garnered significant attention"
[ ] No section ends with a generic summary sentence
[ ] At least 3 sentences per page use hedging ("may", "appears", "suggests")
[ ] At least 2 sentences per page reference specific numbers
[ ] Check with: https://gptzero.me/ (aim for <15% AI probability)
[ ] Check with: https://originality.ai/ (aim for <20% AI score)
```

---

## 4. METHODOLOGY (Required for Review Papers)

### PRISMA Flow Diagram (Mandatory)
Every review paper MUST include:
```
Databases searched: IEEE Xplore, PubMed, Scopus, Web of Science, ScienceDirect
Search terms: documented exactly
Date range: specified
Inclusion criteria: listed (min 5 criteria)
Exclusion criteria: listed (min 4 criteria)
PRISMA flow: Identified → Screened → Eligible → Included (with numbers)
```

### Search Strategy Documentation
```latex
\subsection{Search Strategy}
We searched [databases] using: ("RF" OR "radar" OR "FMCW" OR "UWB" OR 
"mmWave" OR "microwave") AND ("wearable" OR "non-contact" OR "contactless") 
AND ("disease" OR "diagnosis" OR "health" OR "monitoring") AND ("2023" OR 
"2024" OR "2025"). Initial results: N records. After deduplication: M. 
After screening: K. Final included: X papers.
```

---

## 5. DATA INTEGRITY (No Fabricated Numbers)

| Rule | Violation | Correct |
|------|-----------|---------|
| Accuracy numbers | Inventing "93.2%" | Extract from Table 3 of [Author2024] |
| Subject counts | "N=120 subjects" | Report what paper actually says |
| Statistical tests | "F(3,36)=4.82, p=0.006" | Run actual ANOVA on extracted data |
| Confidence intervals | "[91.5, 94.9]" | Calculate from real mean/std/N |

### Data Extraction Workflow
```
1. Create Excel/CSV: columns = Author, Year, RF_Tech, Disease, Accuracy, 
   Subjects, Method, Dataset, Preprocessing, DOI
2. Extract from each of 30 downloaded papers
3. Run statistics in Python (scipy.stats)
4. Report only computed values, never estimated
```

---

## 6. PAGE LIMIT COMPLIANCE

| Journal | Page Limit | Current Status |
|---------|------------|----------------|
| IEEE Sensors Journal | 8-10 pages (regular) | Target: 8 pages |
| IEEE TBME | 10-12 pages | OK |
| IEEE Access | No strict limit | OK |

### Trimming Priority (what to cut first)
1. Reduce verbose introductions (aim: 0.75 page max)
2. Merge small tables into larger comparison tables
3. Reduce figure captions to 2 lines max
4. Remove redundant cross-references ("As shown in Table X, which presents...")
5. Use \small or \footnotesize for large tables
6. Cut generic future work (keep only specific, novel directions)

---

## 7. PRE-SUBMISSION CHECKLIST

```
BEFORE submitting to ANY journal:

[ ] All references verified (real DOIs, real authors)
[ ] All accuracy numbers extracted from real papers
[ ] PRISMA methodology section included
[ ] All figures at 300+ DPI
[ ] No TikZ rendering errors (check all figures in PDF)
[ ] No figure/table overlap or cutoff
[ ] Page count within journal limit
[ ] AI writing check passed (<15% GPTZero score)
[ ] Abstract word count within limit (150-250 words for IEEE)
[ ] Keywords match journal's controlled vocabulary
[ ] Author names and affiliations correct and consistent
[ ] Email addresses are institutional (not Gmail)
[ ] Spell check completed
[ ] Grammar check (Grammarly or LanguageTool)
[ ] All equations numbered and referenced
[ ] All figures and tables referenced in text
[ ] Conclusion answers all Research Questions
[ ] "Limitations of this review" subsection included
[ ] Acknowledgments section included
[ ] Conflict of interest statement included
```

---

## 8. FIGURE QUALITY CHECKLIST

```
For EVERY figure:
[ ] Vector format preferred (TikZ/pgfplots → PDF)
[ ] If rasterized: minimum 300 DPI
[ ] Font size readable at print scale (min 6pt)
[ ] Axis labels present and readable
[ ] Legend does not overlap data
[ ] Color-blind friendly palette (avoid red-green only)
[ ] Caption is descriptive (what + why, not just what)
[ ] Referenced in text before it appears
[ ] No whitespace waste (figure fills column width)
[ ] IEEE: single column = 3.5" wide, double column = 7.16" wide
```

---

*Policy version: 1.0 | Created: 2026-04-20 | Applies to: All RF wearable papers*
