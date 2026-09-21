# HADES software reproducibility demo

This directory contains a small, real-data demonstration of the custom analysis software used in the HADES Nature Methods manuscript:

**HADES: high-throughput end-to-end automation of multimodal phenotyping for root-microbe interactions**

The demo uses one real Exp62 acquisition set:

- **Experiment:** Exp62
- **Genotype:** *Arabidopsis thaliana* Col-0
- **Plate/tray:** 2
- **ROOT1 / FC1 acquisition round:** 20
- **VNIR2 acquisition round:** 19
- **Plants:** 5 plants on one tray
- **Fluorescence channel used here:** FC1 / F483
- **Hyperspectral sensor used in the manuscript:** VNIR2

The ROOT/FC and VNIR2 records correspond to the same experimental day. Acquisition-round numbers differ because the sensor schedules are independent.

The files in `demo.zip` are a minimal subset prepared from the Exp62 experiment record specifically for software verification. Scientific reuse should cite the full Exp62 dataset rather than the demo archive.

The purpose of this demo is to verify that the custom scientific analysis software can be installed and run on a small representative dataset. It is **not** a copy of the complete HADES experiment record and is **not** intended to reproduce every manuscript figure in one command.

The validated workflow is:

```text
ROOT1 raw TIFF
    |
    | historical vendor-equivalent conversion
    v
8-bit RGBA PNG
    |
    v
PyPhenotyper
    |
    +--> root/shoot/component masks + morphology measurements
    |
    +---------------------------+
                                |
                                v
                         HADES_FC
                         FC1 / F483
                                |
                                +--> registered fluorescence measurements
                                |    + QC overlays
                                |
                                v
                         HADES_HSI
                         VNIR2
                                |
                                +--> registered hyperspectral measurements
                                     + QC overlays
```

The complete HADES data and code index is maintained at:

https://npec-nl.github.io/hades-research-resources/

## Download the demo dataset

The input dataset for this reproducibility test is distributed as the `demo.zip`
asset attached to release **v1.0** of the HADES research-resources repository:

https://github.com/NPEC-NL/hades-research-resources/releases/download/v1.0/demo.zip

Release page:

https://github.com/NPEC-NL/hades-research-resources/releases/tag/v1.0

After downloading, extract `demo.zip` to a writable working directory. All
analysis outputs described below are generated locally from the contents of
that archive; generated analysis directories are not distributed as inputs.

---

## 1. Scope and relationship to the companion Data Descriptor

The companion Scientific Data Data Descriptor focuses on the durable HADES experiment records: vendor acquisition/export data, metadata, manifests, checksums, variable definitions, provenance, and raw-format access.

It deliberately does **not** duplicate the complete downstream PyPhenotyper segmentation trees, aligned fluorescence products, registered hyperspectral result trees, or figure-generation directories. Those downstream products are pipeline-version-specific and can be regenerated from the archived acquisition data using the separately maintained analysis code.

This demo is the executable bridge between those two layers:

```text
deposited acquisition record
        |
        v
small representative extracted dataset
        |
        v
custom HADES analysis code
        |
        v
regenerated downstream analysis products
```

For full experiment reuse, always begin with the README of the relevant experiment record. Some HADES releases use archive-optimized storage and therefore require the documented restoration procedure before the conventional logical sensor tree is available. This repository-level storage reconstruction is separate from the scientific analysis demonstrated here.

The present demo was taken from Exp62. Current access information for the full Exp62 record is provided on the HADES research-resources page.

---

## 2. Code repositories

### ROOT / morphology: PyPhenotyper

Frozen HADES branch:

https://github.com/NPEC-NL/pyphenotyper/tree/hades-paper-frozen

Archived release / software DOI:

https://doi.org/10.5281/zenodo.22283634

PyPhenotyper performs seedling segmentation, root-system reconstruction, primary/lateral-root assignment, landmark extraction, and morphology measurement.

### Fluorescence: HADES_FC

https://github.com/valerian-meline/HADES_FC

HADES_FC reads HADES fluorescence acquisitions, aligns fluorescence images to RootCam-derived masks, and exports pixel-level and summary fluorescence measurements together with registration overlays.

### Hyperspectral: HADES_HSI

https://github.com/valerian-meline/HADES_HSI

HADES_HSI processes the hyperspectral data used in the Nature Methods manuscript.

The manuscript uses **VNIR** as the generic name of the visible-to-near-infrared hyperspectral modality. In the PlantScreen export and in the analysis code, the actual sensor/export identifier used for the manuscript hyperspectral results is **`VNIR2`**. The other VNIR sensor is not required to reproduce the manuscript analyses.

---

## 3. Demo directory layout

After extracting `demo.zip`, the distributed demo contains **inputs only**:

```text
demo/
├── FC1_TAR/
│   └── *.tar
│
├── ROOT1/
│   ├── 122_20_2025-07-17_09-04-48_exp62_col_02_ROOT1_FishEyeCorrected.tif
│   └── reference/
│       └── vendor_png.png    # validation reference; not an analysis input
│
└── VNIR2/
    └── Measurement/
        ├── *_Data.bil
        ├── *_Data.hdr
        ├── *_DarkCalibration.bil
        ├── *_DarkCalibration.hdr
        ├── *_WhiteCalibration.bil
        └── *_WhiteCalibration.hdr
```

The Git repository itself does not track these large binary demo inputs. The
authoritative reviewer copy is the `demo.zip` release asset linked above.

The analysis directories are **not** distributed as demo inputs. They are generated during the workflow:

```text
demo/
├── ROOT1_analysis/   # created after PyPhenotyper
├── FC1_analysis/     # created by HADES_FC
└── VNIR2/
    └── Analysis/     # created by HADES_HSI
```

`SENSOR/Measurement/` is part of the original PlantScreen vendor export layout. HADES_HSI preserves this layout and writes corresponding results under `VNIR2/Analysis/`.

PyPhenotyper and HADES_FC do not require their inputs to be under a `Measurement/` directory.

`ROOT1/reference/vendor_png.png` is kept in a subdirectory deliberately. PyPhenotyper scans `.png` files directly under the supplied ROOT input directory, so placing the historical reference PNG in `ROOT1/` itself would risk it being interpreted as an additional analysis input. The `reference/` directory must therefore remain separate from the generated analysis PNG.

The filename contains `FishEyeCorrected` because this field is part of the historical vendor naming convention. In HADES RootCam acquisitions used here, the fish-eye-correction setting is fixed to **FEC = 0**, i.e. no fish-eye correction is applied.

---

# Software requirements

## 4. Tested platform

The complete demo was successfully run on Windows x86-64 with:

- **CPU:** Intel Xeon Gold 5317
- **GPU:** not required
- **ROOT runtime:** ~19 s
- **FC runtime:** ~20 s
- **VNIR2 runtime:** ~120 s
- **Total scientific-analysis runtime:** ~159 s

The test used CPU execution for PyPhenotyper. No unusual RAM pressure was observed during the small demo.

A CUDA-capable NVIDIA GPU is optional. The historical TensorFlow environment can emit CUDA-library warnings on a modern Windows installation when the legacy TensorFlow-compatible CUDA runtime is not installed. These warnings do not prevent CPU execution.

---

## 5. Recommended Python environments

Two environments are recommended.

### Environment A — PyPhenotyper

- Python 3.10
- historical frozen `requirements.txt` from the PyPhenotyper HADES branch

The tested environment includes the historical TensorFlow 2.10 / Keras 2.10 generation and the pinned dependencies recorded by the frozen repository.

### Environment B — HADES_FC + HADES_HSI

- Python 3.12
- HADES_FC environment
- HADES_HSI requirements added to the same environment

The fluorescence and hyperspectral pipelines were successfully run in one shared Python 3.12 conda environment.

---

# Installation

## 6. Conda solver

For conda installations, the libmamba solver is strongly recommended because the classic solver can be unnecessarily slow:

```powershell
conda config --set solver libmamba
```

---

## 7. Clone the repositories

```powershell
git clone --branch hades-paper-frozen https://github.com/NPEC-NL/pyphenotyper.git
git clone https://github.com/valerian-meline/HADES_FC.git
git clone https://github.com/valerian-meline/HADES_HSI.git
```

For archival reproduction, use the frozen/released revisions linked from the HADES research-resources page rather than an arbitrary future development state.

---

## 8. Create the PyPhenotyper environment

```powershell
conda create -n hades-pyphenotyper python=3.10 pip
conda activate hades-pyphenotyper

cd path\to\pyphenotyper
python -m pip install -r pyphenotyper\requirements.txt
python -m pip check
```

Optional smoke test:

```powershell
python -c "import numpy, cv2, tensorflow, scipy, skimage, pandas; print('PyPhenotyper imports OK')"
```

The demo was successfully reproduced from a newly created Python 3.10 environment using the frozen `requirements.txt`.

---

## 9. Create the shared downstream environment

Create the HADES_FC environment and add the HADES_HSI requirements:

```powershell
conda env create -f path\to\HADES_FC\environment.yml
conda activate fc-improvement

python -m pip install -r path\to\HADES_HSI\requirements.txt
```

Optional smoke test:

```powershell
python -c "import numpy, pandas, scipy, skimage, sklearn, cv2, imageio, spectral, pybaselines; print('FC/HSI imports OK')"
```

---

# ROOT input reconstruction

## 10. ROOT1 TIFF and historical PNG representation

The distributed ROOT1 demo input contains one original acquisition file and one historical vendor PNG retained only for validation:

```text
ROOT1/
├── 122_20_2025-07-17_09-04-48_exp62_col_02_ROOT1_FishEyeCorrected.tif
└── reference/
    └── vendor_png.png
```

Only the TIFF is an analysis source file. `reference/vendor_png.png` is never supplied to PyPhenotyper.

The `FishEyeCorrected` token is part of the historical vendor filename. For the HADES acquisition used here, **FEC = 0**, meaning that no fish-eye correction was applied.

The TIFF payload contains **12-bit grayscale values stored in a 16-bit container**. The historical vendor PNG exports used by PyPhenotyper were 8-bit RGBA images generated as:

```text
g = floor(TIFF × 255 / 4095)

R = g
G = g
B = g
A = 255
```

This mapping was reconstructed by direct comparison with historical vendor-generated PNG exports.

The PNG needed by PyPhenotyper can be generated **in place inside `ROOT1/` using the PyPhenotyper Python 3.10 environment**. No separate preprocessing environment is required.

Minimal conversion example:

```python
import cv2
import numpy as np

src = r"D:\path\to\demo\ROOT1\122_20_2025-07-17_09-04-48_exp62_col_02_ROOT1_FishEyeCorrected.tif"
dst = src[:-4] + ".png"

raw = cv2.imread(src, cv2.IMREAD_UNCHANGED)

if raw is None:
    raise RuntimeError(f"Could not read {src}")
if raw.ndim != 2:
    raise ValueError(f"Expected a single-channel TIFF, got shape {raw.shape}")
if raw.dtype != np.uint16:
    raise ValueError(f"Expected uint16 TIFF container, got {raw.dtype}")
if raw.max() > 4095:
    raise ValueError(
        f"Maximum pixel value is {raw.max()}; do not assume 12-bit input."
    )

g = (raw.astype(np.uint32) * 255 // 4095).astype(np.uint8)
rgba = cv2.cvtColor(g, cv2.COLOR_GRAY2BGRA)
rgba[..., 3] = 255

if not cv2.imwrite(dst, rgba):
    raise RuntimeError(f"Could not write {dst}")

print(dst)
```

This creates the analysis PNG directly under `ROOT1/` while leaving the reference PNG isolated in its subdirectory:

```text
ROOT1/
├── 122_20_2025-07-17_09-04-48_exp62_col_02_ROOT1_FishEyeCorrected.tif
├── 122_20_2025-07-17_09-04-48_exp62_col_02_ROOT1_FishEyeCorrected.png
└── reference/
    └── vendor_png.png
```

The generated PNG directly under `ROOT1/` is the PyPhenotyper input.

`ROOT1/reference/vendor_png.png` is a historical vendor-generated PNG retained **only as a validation reference**. It must remain in the `reference/` subdirectory so that PyPhenotyper does not interpret it as a second input image. The newly reconstructed PNG can be compared with this reference to confirm the historical TIFF-to-PNG mapping.

For example:

```python
import cv2
import numpy as np

a = cv2.imread(
    r"D:\path\to\demo\ROOT1\122_20_2025-07-17_09-04-48_exp62_col_02_ROOT1_FishEyeCorrected.png",
    cv2.IMREAD_UNCHANGED,
)
b = cv2.imread(
    r"D:\path\to\demo\ROOT1\reference\vendor_png.png",
    cv2.IMREAD_UNCHANGED,
)

print("identical:", np.array_equal(a, b))
```

For the validated conversion, the reconstructed and historical vendor PNG representations should be identical.

Do **not** copy or move `reference/vendor_png.png` into the top level of `ROOT1/` before running PyPhenotyper. No deletion step is required: keeping the reference file in its subdirectory prevents it from being read as an analysis image.

A separate lossless 16-bit representation can be constructed by left-shifting the 12 meaningful bits:

```text
PNG16 = TIFF << 4
```

but this is **not** the historical PyPhenotyper input and is not needed for the demo.


# Running the demo

## 11. Step 1 — PyPhenotyper / ROOT1

Activate the ROOT environment:

```powershell
conda activate hades-pyphenotyper
cd path\to\pyphenotyper
```

For a clean run, remove any output directories left by an earlier execution:

```powershell
Remove-Item -Recurse -Force .\input -ErrorAction SilentlyContinue
Remove-Item -Recurse -Force .\timeseries -ErrorAction SilentlyContinue
Remove-Item -Recurse -Force .\final_timeseries -ErrorAction SilentlyContinue
```

Run the five-plant Arabidopsis workflow:

```powershell
python main_batches_five_arabidopsis.py
```

Before running PyPhenotyper, generate the vendor-equivalent PNG in the `ROOT1/` directory using the conversion shown above.

When prompted, provide the `ROOT1/` directory:

```text
D:\path\to\hades-research-resources\source\demo\ROOT1
```

For the demo, use:

```text
batch size: 1
```

PyPhenotyper scans lowercase `.png` files directly in the supplied input directory. For this demo, the only such top-level PNG should be the newly generated `122_20_2025-07-17_09-04-48_exp62_col_02_ROOT1_FishEyeCorrected.png`; the validation image remains under `ROOT1/reference/`.

### Expected ROOT output

Completed results are written under the PyPhenotyper repository:

```text
final_timeseries/
```

Representative outputs include:

```text
measurements.xlsx

plant_<n>/
├── root_mask.png
├── main_root_mask.png
├── lateral_root_mask.png
├── tip_mask.png
├── node_mask.png
├── shoot_mask.png
├── plant_measurements.xlsx
├── plant_data.xlsx
└── landmarks.xlsx

root_structure.rsml
```

The demo should produce outputs for five plants.

The generated masks should be visually plausible and should correspond to the roots and shoots in the input image.

### Validated runtime

On the test workstation:

```text
CPU: Intel Xeon Gold 5317
GPU used: no
Input: one tray, one day, five plants
Runtime: approximately 19 s
```

---

## 12. Copy ROOT output for downstream analysis

The historical PyPhenotyper script writes to `final_timeseries/`; HADES_FC and HADES_HSI consume a stable RootCam analysis tree.

Create `ROOT1_analysis/` in the demo and copy the completed PyPhenotyper output into it:

```powershell
New-Item -ItemType Directory -Force "D:\path\to\demo\ROOT1_analysis"

Copy-Item `
  ".\final_timeseries\*" `
  "D:\path\to\demo\ROOT1_analysis\" `
  -Recurse -Force
```

Do not rename the internal acquisition identifiers. Downstream matching relies on the existing HADES naming convention.

---

## 13. Step 2 — HADES_FC / FC1 / F483

Activate the shared downstream environment:

```powershell
conda activate fc-improvement
cd path\to\HADES_FC
```

This demo uses:

```text
RootCam: ROOT1
Fluorescence sensor: FC1
Emission/filter setting: F483
```

The current HADES_FC script does not expose these settings through a command-line interface. Before running, edit the `PYCHARM_SETTINGS` block at the bottom of `FC_analysis.py`.

For this demo:

```python
PYCHARM_SETTINGS = {
    "working_directory": r"D:\path\to\demo",
    "filter_fc1": "F483",
    "filter_fc2": "F635",
    "root_set": "ROOT1",
}
```

`filter_fc2` is not used by this demo.

The required input structure is:

```text
demo/
├── FC1_TAR/
│   └── *.tar
└── ROOT1_analysis/
    └── ... PyPhenotyper output ...
```

Run:

```powershell
python FC_analysis.py
```

### Expected FC output

HADES_FC automatically creates:

```text
FC1_analysis/
```

Representative products include:

```text
*_pixels.csv
*_summary.csv
*_overlay.png
run_parameters.json
```

The first QC check should be the generated overlay image. The RootCam-derived masks should align correctly with the fluorescence image.

### Validated runtime

```text
CPU: Intel Xeon Gold 5317
Input: one tray, one day, five plants
Runtime: approximately 20 s
```

---

## 14. Step 3 — HADES_HSI / VNIR2

Activate the shared downstream environment:

```powershell
conda activate fc-improvement
cd path\to\HADES_HSI
```

The hyperspectral records used by the Nature Methods manuscript are stored under the PlantScreen sensor/export identifier:

```text
VNIR2
```

For this demo, the vendor layout is preserved:

```text
VNIR2/
└── Measurement/
    ├── *_Data.bil
    ├── *_Data.hdr
    ├── *_DarkCalibration.bil
    ├── *_DarkCalibration.hdr
    ├── *_WhiteCalibration.bil
    └── *_WhiteCalibration.hdr
```

Run:

```powershell
python scripts\run_hpx_hades.py `
  --vnir2-root-dir "D:\path\to\demo\VNIR2\Measurement" `
  --root-mask-dir "D:\path\to\demo\ROOT1_analysis"
```

No optional export flags are required for the minimal demo.

### Expected VNIR2 output

The pipeline writes corresponding results under:

```text
VNIR2/Analysis/
```

Representative products include:

```text
*_summary.csv
*_OverlayQualityCheck.png
preprocessing / QC metrics
run-parameter JSON files
master_summary.csv
```

The first QC check should be `*_OverlayQualityCheck.png`. Registered RootCam masks should overlap the corresponding structures in the hyperspectral image.

### Validated runtime

```text
CPU: Intel Xeon Gold 5317
Input: one tray, one day, five plants
Runtime: approximately 120 s
```

---

# Expected total runtime

## 15. Measured analysis runtime

On the validation workstation:

```text
PyPhenotyper / ROOT1:  ~19 s
HADES_FC / FC1 F483:  ~20 s
HADES_HSI / VNIR2:   ~120 s
--------------------------------
Total:                ~159 s
```

These timings exclude repository cloning, environment installation, and user interaction.

No GPU is required for the demo.

---

# Troubleshooting

## 16. TensorFlow reports that CUDA DLLs are missing

A typical CPU-only run may print warnings similar to:

```text
Could not load dynamic library 'cudart64_110.dll'
Could not load dynamic library 'cudnn64_8.dll'
Skipping registering GPU devices...
No GPU found
```

This is expected when the legacy CUDA runtime required by native-Windows TensorFlow 2.10 is not installed.

It does **not** indicate that the demo has failed. The validated ROOT analysis completed correctly on CPU.

---

## 17. PyPhenotyper results are written inside the code repository

This is expected behavior of the historical workflow.

PyPhenotyper writes completed results under:

```text
pyphenotyper\final_timeseries\
```

Copy these results into:

```text
demo\ROOT1_analysis\
```

before running HADES_FC or HADES_HSI.

---

## 18. FC requires editing `FC_analysis.py`

This is expected in the current HADES_FC implementation.

Before execution, change only the configuration block at the bottom of the script so that:

- `working_directory` points to the demo;
- `filter_fc1` matches the experiment;
- `filter_fc2` matches the experiment if FC2 is used;
- `root_set` matches the relevant RootCam.

For this demo:

```text
ROOT1 + FC1 + F483
```

---

## 19. Why does VNIR2 use `Measurement/`?

`Measurement/` is part of the original PlantScreen export structure, not a directory invented for this demo.

The HADES_HSI workflow also derives the corresponding analysis location from this layout:

```text
VNIR2/Measurement/
        |
        v
VNIR2/Analysis/
```

Keep the `Measurement` directory name unchanged.

---

# Using the code on complete HADES datasets

## 20. Start from the experiment README

The full HADES datasets are much larger and more heterogeneous than this one-tray demo.

For complete experiments:

1. open the relevant experiment record from the HADES research-resources page;
2. read that experiment's README;
3. if the release is archive-optimized, restore the documented logical dataset layout using the release-specific restoration procedure;
4. use the experiment metadata and file/provenance mappings rather than guessing sensor or treatment associations;
5. regenerate historical RootCam PNG analysis inputs from archived TIFF files where needed;
6. run the relevant custom analysis pipeline;
7. retain experiment, plate/tray, plant position, sensor, round, acquisition time, software version, and source path in downstream provenance.

Different experiments use different sensor combinations. Do not assume that the `ROOT1 + FC1/F483 + VNIR2` configuration used in this demo applies to every HADES experiment.

---

## 21. TIFF-to-PNG conversion in full datasets

The ROOT TIFF-to-PNG transformation is part of the reproducibility path from archived raw acquisition to the historical PyPhenotyper input.

For relevant full experiment records, the dataset README should document the same deterministic TIFF-to-PNG mapping, either directly or by linking to a versioned implementation.

The transformation must not introduce per-image contrast normalization or other undocumented image processing.

---

# Validation record

## 22. What has been tested

The following sequence has been reproduced successfully from newly created Python environments:

```text
[PASS] PyPhenotyper installed in fresh Python 3.10 environment
[PASS] frozen PyPhenotyper requirements installed successfully
[PASS] historical ROOT TIFF -> vendor PNG mapping reconstructed
[PASS] reconstructed PNG accepted by PyPhenotyper
[PASS] ROOT1 analysis completed for five plants
[PASS] ROOT masks visually checked
[PASS] FC1/F483 analysis completed using generated ROOT1 masks
[PASS] fluorescence registration overlays visually checked
[PASS] VNIR2 analysis completed using the same ROOT1 masks
[PASS] VNIR2 registration overlays visually checked
[PASS] CPU-only execution confirmed sufficient for this demo
```

---

# Licences and citation

## 23. Software

Consult the `LICENSE` file in each software repository for the authoritative licence terms.

The frozen PyPhenotyper HADES release is archived at:

https://doi.org/10.5281/zenodo.22283634

For HADES_FC and HADES_HSI, cite the version/release linked from the HADES research-resources page at the time of publication.

## 24. Data

The demo is a small subset of Exp62. Use the current Exp62 dataset citation and access information provided by:

https://npec-nl.github.io/hades-research-resources/

The full experiment record, rather than this demo subset, should be cited for scientific reuse of Exp62 data.

---

# Recommended reviewer workflow

For the fastest verification of the custom analysis software:

1. download `demo.zip` from the v1.0 release and extract it to a writable directory;
2. install the PyPhenotyper Python 3.10 environment;
3. generate the historical vendor-equivalent PNG in `demo/ROOT1/` from the supplied TIFF using the short OpenCV conversion shown above;
4. run PyPhenotyper on `demo/ROOT1/`;
5. copy `final_timeseries/` into `demo/ROOT1_analysis/`;
6. install/activate the shared Python 3.12 downstream environment;
7. edit the HADES_FC settings block for `ROOT1 + FC1 + F483`;
8. run HADES_FC and inspect its overlay;
9. run HADES_HSI on `demo/VNIR2/Measurement/` and inspect the VNIR2 QC overlay.

`ROOT1/reference/vendor_png.png` is included only as a validation reference for the TIFF-to-PNG conversion. Keep it in the `reference/` subdirectory; it is not an analysis input and should not be moved into the top level of `ROOT1/`.
