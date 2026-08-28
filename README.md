# HADES research resources

A lightweight companion hub for the HADES project, connecting the **method paper**, experiment-level datasets, analysis code, supplementary workflow video, **Data Descriptor**, and reusable data-publication resources.

> **First-draft review:** persistent destinations that have not yet been frozen are marked **DOI / URL to add**.

## Project

HADES (High-throughput Automated Device for End-to-end Screening) is a fully automated platform for sterile in vitro root phenotyping and plant-microbe interaction studies at the Netherlands Plant Eco-phenotyping Centre (NPEC), Utrecht University. It integrates automated media preparation, imaging-based seed selection and robotic sowing, refrigerated stratification, climate-controlled cultivation, programmable microbial inoculation and multimodal imaging within one robotic workflow. The system can process up to 2,160 custom square Petri dishes in parallel and combines transmitted-light RootCam imaging, multi-channel fluorescence and visible-to-near-infrared hyperspectral imaging with automated analysis. The resulting longitudinal datasets support quantitative study of root architecture, reporter activity, microbial colonization and metabolite-associated fluorescence under standardized conditions.

## Method paper

**Title:** *HADES: high-throughput end-to-end automation of multimodal phenotyping for root-microbe interactions*  
**Paper:** **reference / DOI to add**

### Abstract

High-throughput analysis of root system architecture and plant-microbe interactions remains constrained by limited reproducibility, labour-intensive handling workflows, and the low throughput of multimodal imaging under sterile conditions. Here, we present HADES, a fully automated high-throughput phenotyping platform for in vitro root imaging and microbial interaction studies. HADES integrates automated media preparation, seed selection and sowing, robotic bacterial inoculation, environmental control, and high-resolution time-resolved image acquisition into a modular system that processes up to 2,160 custom square Petri dishes in parallel, enabling temporal analysis of plant growth and plant-microbe interactions. The platform combines bright-field, fluorescence, and hyperspectral imaging to quantify root morphology, reporter activity, and the spatiotemporal dynamics of root-associated metabolites. A deep-learning-based image-analysis pipeline performs root segmentation, graph-based trait extraction, and occlusion inpainting to generate robust longitudinal phenotypic datasets at scale. We demonstrate HADES by resolving genotype-specific effects of coumarin biosynthesis on Arabidopsis thaliana root development and metabolite-associated fluorescence, simultaneously monitoring auxin signalling and colonization by the beneficial bacterium Pseudomonas simiae WCS417, and screening a bacterial transposon-mutant collection for altered plant-associated phenotypes. HADES provides a scalable, sterile, and flexible platform for automated plant phenotyping, facilitating reproducible functional genomics and plant-microbiome research while enabling the reductionist approaches needed to mechanistically dissect complex plant-microbe interactions.

## Experiment datasets

### Exp32 — Arabidopsis coumarin-genotype root architecture and fluorescence dynamics

**Dataset:** **DOI / repository URL to add**  
**Release scope:** Arabidopsis reference record

- **Biological material:** Arabidopsis thaliana Col-0 and the coumarin-biosynthesis mutants f6'h1, cyp82c4 and s8h.
- **Experimental design:** Longitudinal in vitro phenotyping under iron deficiency. Plants are grown on iron-deficient Hoagland medium with Fe-EDTA omitted, solidified with 0.8% Gelrite at pH 7.3.
- **Acquisition:** Repeated transmitted-light RootCam imaging provides root and shoot morphology, while fluorescence imaging follows coumarin-associated signal over time.
- **Primary reusable content:** Root/shoot masks and organ- or ROI-specific measurements support longitudinal root architecture traits and fluorescence quantification in the primary root, lateral roots, peri-root/rhizosphere region and shoot.
- **Method-paper relationship:** Supports the root-architecture and coumarin-associated fluorescence demonstrations; associated time-lapse videos are Supplementary Videos S2 and S5.

#### Method paper figure source

Direct source tables used for the Exp32 method-paper figures are stored under [`/source`](source/):

- [`masterfile-exp32-cumarins_FC1.xlsx`](source/masterfile-exp32-cumarins_FC1.xlsx) — longitudinal Exp32 master table containing the morphology/fluorescence measurements used for the root-architecture and coumarin-associated fluorescence figure outputs.
- [`exp32_auc_results.csv`](source/exp32_auc_results.csv) — area-under-the-curve statistical results used for longitudinal Exp32 comparisons.

### Exp35 — Potato root-colonization dynamics under WCS417-mCherry and WCS358-mCherry inoculation

**Dataset:** **DOI / repository URL to add**  
**Release scope:** Separate potato public record

- **Biological material:** Solanum tuberosum true-potato-seed genotypes HYB007 and RP043.
- **Experimental design:** Longitudinal plant-microbe colonization assay with mock, Pseudomonas simiae WCS417-mCherry or Pseudomonas capeferrum WCS358-mCherry treatments. Bacteria are applied as a 10-µL droplet at OD600 = 0.1 to the root-shoot junction; plants are grown on 1/2 MS without sucrose and with 0.8% Gelrite.
- **Acquisition:** RootCam morphology and mCherry fluorescence are acquired repeatedly to follow root development and bacterial signal along the root system.
- **Primary reusable content:** The main quantitative readout is mCherry fluorescence along the primary-root ROI, enabling comparison of host-genotype- and bacterial-strain-dependent colonization dynamics.
- **Method-paper relationship:** Supports the potato root-colonization experiment and Supplementary Video S4.

#### Method paper figure source

Direct source tables used for the Exp35 method-paper figure are stored under [`/source`](source/):

- [`masterfile_Exp35_FC2_V2.xlsx`](source/masterfile_Exp35_FC2_V2.xlsx) — longitudinal potato root-colonization master table used for the fluorescence-based colonization figure.
- [`Exp35_auc_tukey.csv`](source/Exp35_auc_tukey.csv) — area-under-the-curve and Tukey multiple-comparison results used for the Exp35 statistical comparisons.

### Exp44 — Arabidopsis Col-0 screen of GFP-labelled WCS417 transposon mutants

**Dataset:** **DOI / repository URL to add**  
**Release scope:** Separate WCS417 transposon-screen public record

- **Biological material:** Arabidopsis thaliana Col-0 seedlings challenged with individual GFP-labelled Pseudomonas simiae WCS417 mariner transposon mutants.
- **Experimental design:** High-throughput longitudinal screen of a non-saturating collection of 480 random mutants, with mock controls. Individual mutants are applied robotically; the method paper reports inoculum adjusted to OD600 = 0.001 and daily imaging over seven days.
- **Acquisition:** Repeated root morphology and bacterial fluorescence imaging are processed through the HADES segmentation and analysis workflow.
- **Primary reusable content:** Fifteen morphological and fluorescence parameters capture root architecture, shoot growth and bacterial colonization. The proof-of-concept analysis emphasizes primary-root size and mean fluorescence of the primary root to identify candidate outliers.
- **Method-paper relationship:** Supports the high-throughput WCS417 mutant-screen demonstration and the candidate-mutant supplementary table.

#### Method paper figure source

The direct source table used for the Exp44 method-paper screening figure is stored under [`/source`](source/):

- [`masterfile_exp44_FC1_filled_7DAI_corrected_with_P3map_checked_7only.xlsx`](source/masterfile_exp44_FC1_filled_7DAI_corrected_with_P3map_checked_7only.xlsx) — curated seven-day screening master table used to generate the WCS417 transposon-mutant phenotyping figure, including root-growth and fluorescence readouts.

#### Sequence data

**GFP-labelled** ***Pseudomonas simiae*** **WCS417 mariner transposon mutants**

[`EC00167691.zip`](source/EC00167691.zip)

Raw Sanger sequencing data for the 96 GFP-labelled *P. simiae* WCS417 mariner transposon mutants. Individual sequence files are labelled according to the position of each mutant in the 96-well screening plate. The corresponding transposon-disrupted genes and mutant annotations are provided in Supplementary Table S4.

### Exp62 — Arabidopsis VNIR hyperspectral coumarin-emission profiling with Boxeed seed imaging component

**Dataset:** **DOI / repository URL to add**  
**Release scope:** Arabidopsis reference record

- **Biological material:** Arabidopsis thaliana coumarin-biosynthesis genotypes, including Col-0, f6'h1, cyp82c4 and s8h, under iron-deficient conditions.
- **Experimental design:** VNIR hyperspectral fluorescence-emission profiling is combined with RootCam/mask context where applicable. Boxeed seed-imaging and selection records are treated as a component of the same experiment where present.
- **Acquisition:** The HADES hyperspectral unit records visible-to-near-infrared data across 380–900 nm, with BIL/HDR data and calibration companions. The method-paper analysis extracts fluorescence-emission profiles from root and surrounding dilated-root regions, focusing on the 425–600 nm range.
- **Primary reusable content:** Wavelength-resolved root and peri-root spectra are used to compare genotype-specific coumarin-associated emission profiles. The associated Boxeed records capture seed images and morphology/selection information before sowing.
- **Method-paper relationship:** Supports the hyperspectral coumarin-emission experiment and the Boxeed seed-imaging component.

#### Method paper figure source

Direct source tables used for the Exp62 method-paper hyperspectral figure are stored under [`/source`](source/):

- [`masterfile_Exp62_VNIR_root_4genotype.csv`](source/masterfile_Exp62_VNIR_root_4genotype.csv) — wavelength-resolved VNIR fluorescence measurements extracted from the root region across the four-genotype Exp62 dataset.
- [`masterfile_Exp62_VNIR_rhizosphere_4genotype.csv`](source/masterfile_Exp62_VNIR_rhizosphere_4genotype.csv) — wavelength-resolved VNIR fluorescence measurements extracted from the dilated peri-root/rhizosphere region across the four-genotype Exp62 dataset.

### Exp68 — Arabidopsis DR5v2/WCS417-mCherry dual-channel fluorescence assay

**Dataset:** **DOI / repository URL to add**  
**Release scope:** Arabidopsis reference record

- **Biological material:** Arabidopsis thaliana Col-0 and DR5v2::mTurquoise2 reporter seedlings.
- **Experimental design:** Longitudinal dual-fluorescence plant-microbe assay comparing mock treatment with Pseudomonas simiae WCS417-mCherry. The bacterial treatment is incorporated into the medium at 10^5 CFU/mL; seedlings are grown on standard Hoagland medium solidified with 0.8% Gelrite.
- **Acquisition:** RootCam morphology images provide the segmentation masks used to define root regions, while mCherry and mTurquoise2 fluorescence channels report bacterial colonization and auxin-responsive host signalling.
- **Primary reusable content:** Channel-specific fluorescence is quantified along the primary root over time, allowing spatial and temporal comparison of microbial colonization with auxin-responsive reporter activity.
- **Method-paper relationship:** Supports the dual-channel fluorescence experiment and Supplementary Video S3.

#### Method paper figure source

Direct source tables used for the Exp68 method-paper dual-channel fluorescence figure are stored under [`/source`](source/):

- [`masterfile_exp68_FC1_mTurquoise_25DAG.xlsx`](source/masterfile_exp68_FC1_mTurquoise_25DAG.xlsx) — longitudinal mTurquoise2 reporter measurements used for the auxin-responsive fluorescence analysis.
- [`masterfile_exp68_mcheery_FC2.xlsx`](source/masterfile_exp68_mcheery_FC2.xlsx) — longitudinal mCherry-channel measurements used for WCS417 bacterial-colonization analysis.
- [`exp68_auc_results_bacteria_FC2.csv`](source/exp68_auc_results_bacteria_FC2.csv) — area-under-the-curve statistical results for the Exp68 bacterial fluorescence comparisons.

## Analysis code

### ROOT / root architecture analysis pipeline

**Repository (fixed frozen branch):** https://github.com/NPEC-NL/pyphenotyper/tree/hades-paper-frozen  
**Frozen archive DOI:** awaiting final confirmation. The `hades-paper-frozen` branch and repository URL above are fixed for the method-paper release.

Processes monochromatic backlit RootCam images through plate detection/cropping, U-Net-based seedling segmentation, skeletonization and graph-based root reconstruction. Dijkstra’s shortest-path algorithm reconstructs the primary root between the root-shoot junction and primary-root tip. Outputs include shoot size, primary-root length, lateral-root length, lateral-root number, nodes and tips, together with structural masks reused by the fluorescence and hyperspectral workflows.

### Fluorescence analysis — HADES_FC

**Repository:** https://github.com/valerian-meline/HADES_FC

Uses masks from corresponding monochromatic RootCam images to quantify fluorescence without re-segmenting fluorescence frames. Geometric registration aligns modalities; region-specific measurements cover the root system, primary and lateral roots, root tip, nodes, shoot and a dilated peri-root/rhizosphere region. Mean intensity, total signal and pixel counts support reporter, microbial-colonization and coumarin-associated fluorescence analyses.

### VNIR hyperspectral analysis — HADES_HSI

**Repository:** https://github.com/valerian-meline/HADES_HSI

Processes VNIR fluorescence cubes using dark-reference correction, spectral smoothing and spatial filtering. RootCam masks are registered in two stages using a 670-nm leaf reference and a 410-nm root-enhanced reference. Registered root and peri-root regions are used to derive wavelength-resolved mean, summed and standard-deviation spectra plus pixel-level spectra and spatial coordinates.

## Supplementary video

### Supplementary Video S1 — Automated workflow of the HADES platform

**YouTube:** https://youtu.be/F-a306otM4A

Demonstration of the fully automated HADES workflow, from preparation of plant growth plates and imaging-based seed selection with robotic sowing, through refrigerated stratification and climate-controlled cultivation, to RootCam and hyperspectral phenotyping followed by sterile robotic microbial inoculation. Robotic transfer systems connect the modules for continuous, unattended cultivation, phenotyping and experimental manipulation.

## Data Descriptor

**Title:** *A HADES reference release for longitudinal multimodal root phenotyping*  
**Paper:** **reference / DOI to add**

### Abstract

Automated root phenotyping platforms generate large, time-resolved image collections whose reuse depends on retaining experimental context, variable definitions and links between sensor records. This Data Descriptor presents selected Arabidopsis experiments used in the companion HADES method study. The deposited records include longitudinal transmitted-light RootCam images, reporter and bacterial fluorescence acquisitions, coumarin-associated fluorescence, visible-to-near-infrared hyperspectral records, vendor-generated analysis products and Boxeed seed records where available. Detailed biological protocols and scientific interpretation are reported in the companion paper; here we describe the deposited records, metadata curation, variable definitions, file organization and release validation. Each experiment is accompanied by reviewed metadata, a package-scoped snapshot of the HADES variable registry, manifests, checksums and minimal loaders for vendor-specific raw formats. psi_export_rebuilder converts readable PlantScreen exports into these traceable research products, preserves mappings for facility-mediated reanalysis, and separates system-specific export rules from generic release operations so that the same workflow can be adapted to other PlantScreen-derived systems. Large downstream segmentation, alignment and figure-generation result trees are not duplicated in the data records; frozen analysis code is archived separately for regeneration. Together, the deposited experiments, registry and rebuilding workflow provide a reusable release pattern for future HADES datasets and related PlantScreen data at NPEC.

### psi_export_rebuilder

**Repository:** **GitHub URL to add**

Uses readable PlantScreen user exports as the public-release source; inventories records, preserves Measurement/Analysis structure, converts supported tables, creates manifests and hashes, integrates reviewed metadata and package-scoped registry definitions, and retains mappings to facility-side representations. System-specific source rules are isolated in adapters so the generic release workflow can be reused.

### HADES variable registry

**Registry:** **registry URL to add**

Versioned definitions for variables produced by PlantScreen Data Analyzer, Boxeed and custom ROOT, fluorescence and VNIR pipelines. Entries describe stable identity, source software, type/scale, acquisition method, observation level and trait or ontology mappings; experiment packages include the relevant registry subset.

## Partners

1. **Netherlands Plant Eco-phenotyping Centre (NPEC):** https://www.npec.nl/
2. **Utrecht University:** https://www.uu.nl/en
3. **Photon Systems Instruments (PSI):** https://psi.cz/

The GitHub Pages-ready landing page is [`docs/index.html`](docs/index.html).
