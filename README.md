# HADES research resources

A lightweight companion hub for the HADES project, connecting the **method paper**, experiment-level datasets, analysis code, supplementary workflow video, the companion **Data Descriptor**, and reusable data-publication resources.

> [!NOTE]
> **Resource status — 3 September 2026.** The HADES method paper has been submitted. Exp32, Exp35 and Exp68 have public Zenodo records. Exp62 has been submitted to the e!DAL Plant Genomics and Phenomics Research Data Repository (PGP) and is awaiting repository review; its dataset-specific access link and DOI are therefore not yet available. Exp44 remains a separate public-record preparation. The companion Data Descriptor is in final preparation for submission.

## Project

HADES (High-throughput Automated Device for End-to-end Screening) is a fully automated platform for sterile *in vitro* root phenotyping and plant–microbe interaction studies at the Netherlands Plant Eco-phenotyping Centre (NPEC), Utrecht University. It integrates automated media preparation, imaging-based seed selection and robotic sowing, refrigerated stratification, climate-controlled cultivation, programmable microbial inoculation and multimodal imaging within one robotic workflow.

The system can process up to 2,160 custom square Petri dishes in parallel and combines transmitted-light RootCam imaging, multi-channel fluorescence and visible-to-near-infrared hyperspectral imaging with automated analysis. The resulting longitudinal datasets support quantitative study of root architecture, reporter activity, microbial colonization and metabolite-associated fluorescence under standardized conditions.

## Method paper

**Title:** *HADES: high-throughput end-to-end automation of multimodal phenotyping for root-microbe interactions*  
**Status:** Submitted; reference / DOI to add when available.

### Abstract

High-throughput analysis of root system architecture and plant-microbe interactions is constrained by limited reproducibility, labour-intensive workflows, and low-throughput multimodal imaging under sterile conditions. Here, we present HADES, a fully automated phenotyping platform integrating media preparation, seed selection and sowing, robotic bacterial inoculation, environmental control, and time-resolved imaging of up to 2,160 Petri dishes in parallel. HADES combines bright-field, fluorescence, and hyperspectral imaging with deep-learning-based analysis to quantify root architecture, reporter activity, microbial colonisation, and metabolite-associated spectral signatures. We demonstrate its versatility by resolving coumarin-dependent differences in *Arabidopsis thaliana* root development and metabolite-associated fluorescence, simultaneously monitoring auxin signalling and colonisation by root-colonising *Pseudomonas simiae* WCS417 bacteria, and screening a bacterial transposon-mutant collection for altered plant-associated phenotypes. HADES provides a scalable, sterile, and flexible platform for reproducible functional genomics and plant-microbiome research, enabling high-throughput mechanistic dissection of plant-microbe interactions.

## Experiment datasets

The experiment records and the method-paper figure sources serve different purposes. The **public experiment datasets** preserve acquisition-level records, PlantScreen Data Analyzer outputs, reviewed metadata, variable definitions, manifests and provenance. The large customized ROOT, fluorescence and hyperspectral downstream result trees used for the method-paper analyses are not duplicated in these dataset records; their code is maintained separately under [Analysis code](#analysis-code). The lightweight tables under [`/source`](https://github.com/NPEC-NL/hades-research-resources/tree/main/source) are the direct quantitative inputs used for method-paper figures and are provided for transparent figure provenance.

The companion Data Descriptor focuses on the three Arabidopsis reference records **Exp32, Exp62 and Exp68**. Exp35 and Exp44 remain separate supporting HADES records because they represent a potato study and a large bacterial-mutant screen, respectively.

### Exp32 — Arabidopsis coumarin-genotype root architecture and fluorescence dynamics

> [!IMPORTANT]
> **Method-paper relationship:** Figure 2, longitudinal root-system architecture; Figure 5, coumarin-associated fluorescence; Supplementary Videos S2 and S5.

**Dataset:** [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22148825.svg)](https://doi.org/10.5281/zenodo.22148825)  
**Release scope:** Full Exp32 experiment; Arabidopsis Data Descriptor reference record  
**Product form:** Archive-optimized  
**Deposited `data/` payload:** 38.752 GB  
**Reviewed scope:** 20 trays; 100 plant-position rows

- **Biological material:** *Arabidopsis thaliana* Col-0 and the coumarin-biosynthesis mutants f6'h1, cyp82c4 and s8h.
- **Experimental design:** Longitudinal *in vitro* phenotyping under iron deficiency. Plants are grown on iron-deficient Hoagland medium with Fe-EDTA omitted, solidified with 0.8% Gelrite at pH 7.3.
- **Deposited content:** Daily transmitted-light RootCam acquisitions, repeated fluorescence acquisitions, PlantScreen Data Analyzer analysis products, reviewed metadata, package-scoped HADES registry definitions, manifests and provenance records.
- **Method-paper analysis:** The custom ROOT and fluorescence pipelines generate the segmentation masks and organ-/ROI-specific measurements used for longitudinal root architecture and coumarin-associated fluorescence figures; these large downstream result trees are not duplicated in the experiment deposit.

#### Method paper figure source

Direct source tables used for the Exp32 method-paper figures are stored under [`/source`](https://github.com/NPEC-NL/hades-research-resources/tree/main/source):

- [`masterfile-exp32-cumarins_FC1.xlsx`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/masterfile-exp32-cumarins_FC1.xlsx) — longitudinal Exp32 master table containing the morphology/fluorescence measurements used for the root-architecture and coumarin-associated fluorescence figure outputs.
- [`exp32_auc_results.csv`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/exp32_auc_results.csv) — area-under-the-curve statistical results used for longitudinal Exp32 comparisons.

### Exp35 — Potato root-colonization dynamics under WCS417-mCherry and WCS358-mCherry inoculation

> [!IMPORTANT]
> **Method-paper relationship:** Supplementary Figure S3, fluorescence-based quantification of bacterial colonization dynamics on potato roots; Supplementary Video S4.

**Dataset:** [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22282859.svg)](https://doi.org/10.5281/zenodo.22282859)  
**Release scope:** Separate potato public record; outside the three-record Data Descriptor scope

- **Biological material:** *Solanum tuberosum* true-potato-seed genotypes HYB007 and RP043.
- **Experimental design:** Longitudinal plant-microbe colonization assay with mock, *Pseudomonas simiae* WCS417-mCherry or *Pseudomonas capeferrum* WCS358-mCherry treatments. Bacteria are applied as a 10-µL droplet at OD600 = 0.1 to the root-shoot junction; plants are grown on 1/2 MS without sucrose and with 0.8% Gelrite.
- **Acquisition:** RootCam morphology and mCherry fluorescence are acquired repeatedly to follow root development and bacterial signal along the root system.
- **Method-paper analysis:** The main figure-level quantitative readout is mCherry fluorescence along the primary-root ROI, enabling comparison of host-genotype- and bacterial-strain-dependent colonization dynamics.

#### Method paper figure source

Direct source tables used for the Exp35 method-paper figure are stored under [`/source`](https://github.com/NPEC-NL/hades-research-resources/tree/main/source):

- [`masterfile_Exp35_FC2_V2.xlsx`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/masterfile_Exp35_FC2_V2.xlsx) — longitudinal potato root-colonization master table used for the fluorescence-based colonization figure.
- [`Exp35_auc_tukey.csv`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/Exp35_auc_tukey.csv) — area-under-the-curve and Tukey multiple-comparison results used for the Exp35 statistical comparisons.

### Exp44 — Arabidopsis Col-0 screen of GFP-labelled WCS417 transposon mutants

> [!IMPORTANT]
> **Method-paper relationship:** Figure 4, high-throughput screening of GFP-labelled WCS417 transposon mutants for altered root-colonization and root-development phenotypes; Supplementary Table S4 provides annotations for sequenced candidate mutants.

**Dataset:** **DOI / repository URL to add**  
**Release scope:** Separate WCS417 transposon-screen public record; outside the three-record Data Descriptor scope

- **Biological material:** *Arabidopsis thaliana* Col-0 seedlings challenged with individual GFP-labelled *Pseudomonas simiae* WCS417 mariner transposon mutants.
- **Experimental design:** High-throughput longitudinal screen of a non-saturating collection of 480 random mutants, with mock controls. Individual mutants are applied robotically; the submitted method paper reports a 10-µL bacterial droplet at OD600 = 0.1 to the root-shoot junction and daily imaging over seven days.
- **Acquisition:** Repeated root morphology and bacterial fluorescence imaging are processed through the HADES segmentation and analysis workflow.
- **Method-paper analysis:** Fifteen morphological and fluorescence parameters capture root architecture, shoot growth and bacterial colonization. The proof-of-concept analysis emphasizes primary-root size and mean fluorescence of the primary root to identify candidate outliers.

#### Method paper figure source

The direct source table used for the Exp44 method-paper screening figure is stored under [`/source`](https://github.com/NPEC-NL/hades-research-resources/tree/main/source):

- [`masterfile_exp44_FC1_filled_7DAI_corrected_with_P3map_checked_7only.xlsx`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/masterfile_exp44_FC1_filled_7DAI_corrected_with_P3map_checked_7only.xlsx) — curated seven-day screening master table used to generate the WCS417 transposon-mutant phenotyping figure, including root-growth and fluorescence readouts.

#### Sequence data

**GFP-labelled** ***Pseudomonas simiae*** **WCS417 mariner transposon mutants**

[`EC00167691.zip`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/EC00167691.zip)

Raw Sanger sequencing data for the 96 GFP-labelled *P. simiae* WCS417 mariner transposon mutants. Individual sequence files are labelled according to the position of each mutant in the 96-well screening plate. The corresponding transposon-disrupted genes and mutant annotations are provided in Supplementary Table S4.

### Exp62 — Multimodal Arabidopsis phenotyping with Boxeed seed imaging and VNIR hyperspectral fluorescence

> [!IMPORTANT]
> **Method-paper relationship:** Figure 6, VNIR hyperspectral discrimination of coumarin-associated emission profiles in the Col-0, f6'h1, cyp82c4 and s8h subset; Supplementary Figure S2, Boxeed seed-imaging and selection component.

**Dataset title submitted to e!DAL-PGP:** *HADES Exp62 dataset: Multimodal Arabidopsis phenotyping with Boxeed seed imaging and VNIR hyperspectral fluorescence across eight genotypes under iron deficiency*  
**Repository:** [e!DAL - Plant Genomics and Phenomics Research Data Repository (PGP)](https://edal-pgp.ipk-gatersleben.de/)  
**Status:** Submitted 3 September 2026; repository review in progress  
**Dataset-specific link / DOI:** **pending repository review**  
**Licence:** CC BY 4.0  
**Release scope:** Full eight-genotype Exp62 batch; Arabidopsis Data Descriptor reference record  
**Product form:** Repository-browsable  
**Submitted data payload:** 637.435 GB  
**Reviewed scope:** 149 trays; 745 plant-position rows

- **Biological material:** *Arabidopsis thaliana* Col-0, f6'h1, cyp82c4, s8h, bglu42, arf1, arf19 and tir1-1 afb2-3 afb3-4 under iron-deficient conditions.
- **Experimental design:** Exp62 is a broader follow-up to Exp32 that adds Boxeed seed phenotyping and VNIR hyperspectral fluorescence measurements. The companion method paper uses the Col-0, f6'h1, cyp82c4 and s8h subset for its hyperspectral demonstration; the public record preserves the complete eight-genotype experiment.
- **Deposited content:** VNIR BIL/HDR hyperspectral cubes and calibration companions, RootCam/mask context where applicable, PlantScreen Data Analyzer analysis outputs, Boxeed seed images and seed measurement/selection records, reviewed metadata, package-scoped registry definitions, manifests and provenance records.
- **Repository design:** Exp62 is prepared as a file-browsable data tree rather than the archive-optimized form used for Exp32 and Exp68, matching e!DAL-PGP's repository model for direct browsing of individual files.

#### Method paper figure source

Direct source tables used for the Exp62 method-paper hyperspectral figure are stored under [`/source`](https://github.com/NPEC-NL/hades-research-resources/tree/main/source):

- [`masterfile_Exp62_VNIR_root_4genotype.csv`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/masterfile_Exp62_VNIR_root_4genotype.csv) — wavelength-resolved VNIR fluorescence measurements extracted from the root region for the four-genotype method-paper subset.
- [`masterfile_Exp62_VNIR_rhizosphere_4genotype.csv`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/masterfile_Exp62_VNIR_rhizosphere_4genotype.csv) — wavelength-resolved VNIR fluorescence measurements extracted from the dilated peri-root/rhizosphere region for the four-genotype method-paper subset.

### Exp68 — Arabidopsis DR5v2/WCS417 dual-channel fluorescence experiment

> [!IMPORTANT]
> **Method-paper relationship:** Figure 3, dual-channel fluorescence imaging of auxin-responsive DR5v2::mTurquoise2 signalling and WCS417-mCherry colonization; Supplementary Video S3. The method-paper demonstration uses the no-added-sucrose, non-pvd WCS417-mCherry subset and corresponding controls.

**Dataset:** [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22181454.svg)](https://doi.org/10.5281/zenodo.22181454)  
**Release scope:** Complete 12-condition Exp68 batch; Arabidopsis Data Descriptor reference record  
**Product form:** Archive-optimized  
**Deposited `data/` payload:** 78.604 GB  
**Reviewed scope:** 30 trays; 150 plant-position rows

- **Biological material:** *Arabidopsis thaliana* Col-0 and DR5v2::mTurquoise2 reporter seedlings.
- **Experimental design:** The complete experiment combines two plant genotype/reporter states with mock, WCS417-mCherry and WCS417_pvd-mCherry bacterial conditions in media with or without 5% sucrose. The narrower subset analysed in the method paper is identified above.
- **Deposited content:** RootCam morphology records, native fluorescence acquisition containers, PlantScreen Data Analyzer analysis products, reviewed metadata, package-scoped HADES registry definitions, manifests and provenance records.
- **Method-paper analysis:** Custom fluorescence processing uses RootCam-derived masks and geometric registration to quantify mCherry bacterial signal and mTurquoise2 auxin-responsive reporter activity along defined root regions. These downstream result trees are not duplicated in the experiment deposit.

#### Method paper figure source

Direct source tables used for the Exp68 method-paper dual-channel fluorescence figure are stored under [`/source`](https://github.com/NPEC-NL/hades-research-resources/tree/main/source):

- [`masterfile_exp68_FC1_mTurquoise_25DAG.xlsx`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/masterfile_exp68_FC1_mTurquoise_25DAG.xlsx) — longitudinal mTurquoise2 reporter measurements used for the auxin-responsive fluorescence analysis.
- [`masterfile_exp68_mcheery_FC2.xlsx`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/masterfile_exp68_mcheery_FC2.xlsx) — longitudinal mCherry-channel measurements used for WCS417 bacterial-colonization analysis.
- [`exp68_auc_results_bacteria_FC2.csv`](https://github.com/NPEC-NL/hades-research-resources/blob/main/source/exp68_auc_results_bacteria_FC2.csv) — area-under-the-curve statistical results for the Exp68 bacterial fluorescence comparisons.

## Analysis code

The experiment deposits preserve acquisition and vendor-generated records. The customized analysis code used for the method paper is maintained separately so that segmentation, registration and figure-level products can be regenerated without permanently duplicating large image-derived result trees.

### ROOT / root architecture analysis pipeline

**Repository (fixed frozen branch):** https://github.com/NPEC-NL/pyphenotyper/tree/hades-paper-frozen  
**Frozen release page:** https://github.com/NPEC-NL/pyphenotyper/releases/tag/hades-method-submission-2026-08-26  
**Frozen archive DOI:** [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22283634.svg)](https://doi.org/10.5281/zenodo.22283634)

Processes monochromatic backlit RootCam images through plate detection/cropping, U-Net-based seedling segmentation, skeletonization and graph-based root reconstruction. Dijkstra's shortest-path algorithm reconstructs the primary root between the root-shoot junction and primary-root tip. Outputs include shoot size, primary-root length, lateral-root length, lateral-root number, nodes and tips, together with structural masks reused by the fluorescence and hyperspectral workflows.

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
**Status:** Final manuscript preparation for submission; reference / DOI to add when available.  
**Scope:** Exp32, Exp62 and Exp68. Exp35 and Exp44 are linked supporting records but are not part of the three-experiment Data Descriptor release.

### Abstract

Automated root phenotyping platforms generate large, time-resolved image collections whose reuse depends on experimental context, variable definitions and links between sensor records. This Data Descriptor presents three Arabidopsis experiments from the companion HADES method paper, covering longitudinal RootCam imaging, fluorescence, VNIR hyperspectral records, PlantScreen analysis products and, for Exp62, Boxeed seed records. Each experiment is released with reviewed metadata, a package-scoped snapshot of the versioned HADES variable registry, manifests, checksums and minimal raw-format loaders. The registry acts as a data dictionary for machine- and pipeline-generated measurements, providing stable identifiers, definitions, methods and scales. `psi_export_rebuilder` converts contextual PlantScreen exports into traceable research products and separates HADES-specific export rules from reusable scanning, mapping, metadata and packaging operations that can be adapted to other PlantScreen-derived systems. Large downstream segmentation, alignment and figure-generation trees are excluded because they can be regenerated from frozen analysis code. Together, the datasets, registry and rebuilding workflow establish a reusable release pattern for HADES and related PlantScreen data at NPEC.

### psi_export_rebuilder

**GitHub repository:** https://github.com/NPEC-NL/psi-export-rebuilder  
**Frozen version used to create the reference datasets:** `0.1.0`  
**Frozen archive DOI:** [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22213177.svg)](https://doi.org/10.5281/zenodo.22213177)

`psi_export_rebuilder` uses readable PlantScreen user exports as the research-facing release source. It inventories records, preserves `Measurement`/`Analysis` structure, converts supported tables, creates manifests and hashes, integrates reviewed metadata and package-scoped registry definitions, and retains content mappings to facility-side recovery representations.

The release software supports two repository-facing product forms used here:

- **Archive-optimized products** for Exp32 and Exp68, with reversible packaging operations recorded in the release metadata.
- **Repository-browsable products** for file-oriented repositories such as e!DAL-PGP; Exp62 uses this form so individual native files remain directly navigable.

Exp32 was also used for the complete facility round-trip test: the rebuilt product was reverse-transformed to the NPEC internal recovery layout, loaded into the NPEC PlantScreen environment, and used to regenerate a fresh PlantScreen Data Analyzer user-export tar with PlantScreen Data Analyzer 3.4.28.0.

System-specific source rules are isolated in adapters so the generic release workflow can be reused for other PlantScreen-derived installations after their local layouts and variables have been audited. A separate stewardship Article is in preparation to evaluate this broader architecture, storage strategy and adaptation beyond HADES; it is not required to interpret the HADES experiment records described in the Data Descriptor.

### HADES variable registry

**Registry:** https://github.com/NPEC-NL/hades-registry  
**Frozen version used by the reference release:** `1.0.0`  
**Archive DOI:** [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22240635.svg)](https://doi.org/10.5281/zenodo.22240635)

The registry is a versioned data dictionary for variables produced by PlantScreen Data Analyzer, Boxeed and the custom ROOT, fluorescence and VNIR pipelines. Entries describe stable identity, definitions, source software, type/scale, acquisition method, observation level and trait or ontology mappings. The registry provides the observed-variable layer used for MIAPPE-oriented export, while biological study design and treatment metadata are curated separately. Each experiment package contains the registry subset relevant to its deposited records; the complete registry is available from the repository and Zenodo release above.

## Repository services and credits

- **Zenodo** hosts the current public Exp32, Exp35 and Exp68 records and the frozen `psi_export_rebuilder`, HADES variable-registry and ROOT-pipeline releases. Repository information and recommended citation: https://about.zenodo.org/ ; repository-level DOI [![DOI](https://zenodo.org/badge/DOI/10.25495/7GXK-RD71.svg)](https://doi.org/10.25495/7GXK-RD71).
- **e!DAL - Plant Genomics and Phenomics Research Data Repository (PGP)** is used for the large, file-browsable Exp62 release: https://edal-pgp.ipk-gatersleben.de/ . The repository framework is described by Arend et al. (2014), *BMC Bioinformatics* 15, 214: https://doi.org/10.1186/1471-2105-15-214 .

## Partners

1. **Netherlands Plant Eco-phenotyping Centre (NPEC):** https://www.npec.nl/
2. **Utrecht University:** https://www.uu.nl/en
3. **Photon Systems Instruments (PSI):** https://psi.cz/
4. **CropXR:** https://cropxr.org/

The GitHub Pages-ready landing page is [`docs/index.html`](docs/index.html).
