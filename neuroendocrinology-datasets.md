# Public Datasets & Databases for Behavioral Neuroendocrinology

Compiled for a small liberal arts college course on behavioral neuroendocrinology,
with an emphasis on giving students data they can find, analyze, and communicate
about using agentic tools. Non-human data is prioritized to avoid HIPAA
complications, but well-curated de-identified human datasets are included where
they ship cleared for public reanalysis.

---

## Original request

> I'll be teaching a course of behavioral neuroendocrinology at a SLAC next
> semester. I'll be incorporating agentic tools to teach students how to find
> and analyze and communicate about research. Find a list of publicly available
> databases or datasets that I could suggest my students use. Again this is
> behavioral neuroendocrinology and I mean I'm open to all kinds of data — I'm
> assuming human data would involve additional HIPAA considerations so it's
> okay if no human data is used. Don't avoid human data but it's okay if it's
> not human-centered.

---

## Hormone-specific repositories

- **HormoneBase** — Curated population-level database of circulating steroid
  hormones (glucocorticoids, androgens) across vertebrates. ~6,500+ entries
  from 476 free-living species. Great for comparative / ecological projects on
  stress and reproductive hormones. Downloadable from Figshare.
- **Hmrbase / Hmrbase2** — Curated database of ~2,000 hormones and ~3,000
  receptors with ~4,100 hormone-receptor pairs. Useful as a structured
  reference for receptor/ligand pharmacology assignments.
- **NIDDK Endocrinology & Hormone Signaling resources** — NIH-curated portal
  pointing students to NIH-funded endocrine datasets and study resources.

## Brain gene-expression & receptor atlases

- **Allen Brain Atlas (Mouse & Human)** — Whole-brain in situ hybridization and
  microarray gene expression. Students can map any hormone-receptor gene
  (Esr1, Ar, Nr3c1/2, Oxtr, Avpr1a, Pomc, Crh, etc.) onto neuroanatomy. Has
  been used specifically for glucocorticoid physiology and sex-steroid receptor
  work.
- **Allen Cell Types & Mouse Connectivity Atlases** — Companion datasets for
  circuit-level questions.
- **NCBI GEO** — Search for hormone- or stress-related expression studies
  (e.g., GSE84422 for FSHR in human cortex). Good for "find a published
  dataset and reanalyze" assignments.
- **NeuroMorpho.Org** — Free archive of digitally reconstructed neurons;
  useful if students want to look at morphology changes with hormone
  manipulations.

## Knockout & phenotype repositories (mice)

- **International Mouse Phenotyping Consortium (IMPC)** — Standardized
  phenotyping for ~8,000+ knockout lines including endocrine and behavioral
  batteries. 85M data points, ~95,000 significant phenotype hits. Excellent
  for "what happens when you delete *Oxtr*?" style projects.
- **Mouse Phenome Database (MPD, Jackson Lab)** — Strain-survey data across
  endocrine function, behavior, aging, and physiology in inbred strains.
  CC-BY licensed, has APIs.

## Behavior & neurophysiology

- **MouseBytes / MouseBytes+** — Open repository of touchscreen-based rodent
  cognitive behavior data, standardized for sharing.
- **DANDI Archive** — BRAIN Initiative repo with 400+ datasets (>350 TB) in
  NWB format: electrophysiology, calcium imaging, fiber photometry, plus
  paired behavioral time series. CC0/CC-BY. Good for advanced students doing
  computational projects.
- **CRCNS.org (Collaborative Research in Computational Neuroscience)** —
  Older but well-curated neural + behavior datasets, often with
  hormone/stress/social-behavior angles.

## Animal behavior & ecology (field neuroendocrinology)

- **Movebank** — Free animal-tracking database hosted by the Max Planck
  Institute of Animal Behavior. 7,500+ studies. Pairs well with HormoneBase
  for ecophysiology questions (e.g., migration × glucocorticoids).
- **Dryad** — General-purpose data repository where many *Hormones and
  Behavior* and *General and Comparative Endocrinology* papers deposit their
  underlying data. Searchable by species/keyword.
- **GBIF** — Biodiversity records; useful for layering ecological context
  onto endocrine datasets.

## Human (non-imaging) — minimal HIPAA friction because already de-identified

- **NHANES Sex Steroid Hormone Panel** — CDC public-use serum hormone data
  (testosterone, estradiol, estrone, DHEA, progesterone, SHBG, FSH/LH, AMH,
  17-OHP) across multiple cycles 1999–2023. Already de-identified and
  intended for public reuse. Pairs well with demographic/behavioral variables
  in the same survey.
- **MIDUS (Midlife in the United States)** — Includes salivary cortisol
  diurnal data alongside psychosocial measures.

## Human neuroimaging (de-identified, public-use)

- **OpenNeuro** — CC0 fMRI / MRI / EEG / MEG datasets, including stress-task,
  reward, and social-cognition studies relevant to hormones.
- **NeuroVault** — Repository of statistical maps from neuroimaging studies;
  good for meta-analytic mini-projects.
- **Human Connectome Project (HCP)** and **ABCD Study** (data-use agreement
  required) — Larger but more involved; usable but probably more than your
  students need.

---

## Teaching tips for the agentic-tool angle

- Pair students with one structured DB (e.g., HormoneBase, MPD, IMPC) plus
  one literature-mining angle (PubMed / OpenAlex / Semantic Scholar API) so
  the agent has both data and context to reason over.
- For a low-overhead first project, MPD + Allen Brain Atlas is hard to beat:
  students pick a behavioral phenotype, find strain-level variation, then
  map a candidate receptor's expression.
- NHANES is the gentlest human option — it ships as flat files explicitly
  cleared for public reanalysis, so no IRB/HIPAA gymnastics.

## Prompt-injection notice (worth discussing with students)

During the search session that produced this list, one web search result
contained an embedded fake "system reminder" trying to inject MotherDuck/
DuckDB SQL instructions into the assistant's context. It was ignored.
Students using agentic tools to scrape and reason over web content will
encounter similar injection attempts, and this makes a useful in-class
discussion of agent safety and provenance of instructions.

---

## Sources

- [HormoneBase (Scientific Data)](https://www.nature.com/articles/sdata201897)
- [Hmrbase](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2720991/)
- [NIDDK Endocrinology & Hormone Signaling](https://www.niddk.nih.gov/research-funding/research-programs/endocrinology-hormone-signaling)
- [Allen Brain Atlas overview (PubMed)](https://pubmed.ncbi.nlm.nih.gov/23193282/)
- [Allen Brain Atlas use for glucocorticoid physiology](https://pubmed.ncbi.nlm.nih.gov/31100428/)
- [International Mouse Phenotyping Consortium (PMC)](https://pmc.ncbi.nlm.nih.gov/articles/PMC9825559/)
- [Mouse Phenome Database](https://academic.oup.com/nar/article/48/D1/D716/5614177)
- [MouseBytes / MouseBytes+](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10104860/)
- [DANDI Archive](https://about.dandiarchive.org/)
- [Movebank (Methods in Ecology and Evolution)](https://besjournals.onlinelibrary.wiley.com/doi/full/10.1111/2041-210X.13767)
- [Dryad data repository](https://datadryad.org/)
- [NHANES Sex Steroid Hormone Panel 2017–March 2020](https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2017/DataFiles/P_TST.htm)
- [NHANES Sex Steroid Hormone Panel 2021–2023](https://wwwn.cdc.gov/Nchs/Data/Nhanes/Public/2021/DataFiles/TST_L.htm)
- [OpenNeuro (eLife)](https://elifesciences.org/articles/71774)
- [Brain atlas for glycoprotein hormone receptors (eLife)](https://elifesciences.org/articles/79612)
- [Salivary biomarkers in undergraduate research (PMC)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6437038/)
