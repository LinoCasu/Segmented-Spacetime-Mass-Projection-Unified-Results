# Segmented Spacetime – Mass Projection & Unified Results
© Carmen Wrede & Lino Casu

This repository provides a full Python-based implementation and verification of the **Segmented Spacetime Mass Projection Model**, offering a high-precision, testable alternative to traditional gravitational models.

## 📌 Overview

The method implemented here reconstructs the **effective mass** of physical objects based on the principle of **space segmentation**, using a universal scaling function that links gravitational behavior across micro and macro scales.

### Included Features

- ✅ Unified segment-based mass inversion from observed radii
- ✅ Comparison with established experimental values (e.g. electron mass, planetary bodies)
- ✅ Reproduction of classical observables (e.g. Mercury's perihelion, black hole shadow radius)
- ✅ Symbolic check for modified Einstein tensor compatibility (`Gμν = 0`)

## Contents
## Contents

| File                                             | Description                                                                                          |
|--------------------------------------------------|------------------------------------------------------------------------------------------------------|
| `ANTI-CAPITALIST SOFTWARE LICENSE (v 1.4)`       | License text for this project                                                                        |
| `README.md`                                      | Usage guide and documentation                                                                        |
| `bound_energy.py`                                | Calculates bound-electron mass and emitted photon energy based on local frequency shifts             |
| `bound_energy_english.py`                        | English version of the bound energy calculation script                                               |
| `bound_energy_plot.py`                           | Plots bound energy comparisons without ΔM correction                                                 |
| `bound_energy_plot_with_frequenz_shift_fix.py`   | Plots bound energy comparisons with frequency shift (ΔM) correction                                  |
| `bound_energy_results.csv`                       | CSV export of bound energy calculation results                                                       |
| `bound_energy_with_deltaM.csv`                   | CSV export of bound energy results including ΔM corrections                                          |
| `calculation_test.py`                            | Quick mass reconstruction tests and demos for segmented radius inputs                                |
| `check.py`                                       | Runs internal consistency checks for the segmented spacetime model                                   |
| `complete-math.py`                               | Step-by-step didactic demonstration of key calculations in segmented spacetime theory                |
| `fetch_ligo.py`                                  | Fetches and preprocesses LIGO observational data for benchmarking                                    |
| `final_test.py`                                  | Roundtrip validation tests for mass reconstruction via segmented radius                              |
| `paper.py`                                       | Implements detailed sections and example reproductions from the Carmen Wrede & Lino Casu paper       |
| `requirements.txt`                               | Lists Python package dependencies for reproducible setup                                             |
| `segment_mass_results.csv`                       | CSV of computed mass inversion results from segmented mass functions                                 |
| `segmented_full_calc_proof.py`                   | Full calculation proof routines for segmented mass inversion                                         |
| `segmented_full_compare_proof.py`                | Comparative analysis of proof results against established benchmarks                                 |
| `segmented_full_proof.py`                        | Main script to generate all model outputs and run symbolic checks                                    |
| `segmented_mass.py`                              | Core library module implementing mass inversion and segmentation algorithms                          |
| `segmented_spacetime_mass_validation.csv`        | CSV of segmented spacetime mass validation results                                                   |
| `segmented_spacetime_mass_validation_full.csv`   | Full CSV of detailed segmented spacetime mass validation                                             |
| `segmented_spacetime_mass_validation_perfect.csv`| CSV of perfect-case segmented spacetime mass validations                                             |
| `carmen_qed_incompleteness_demo.py`              | Calculates and explains, with real astrophysical data, why only a fraction of the original photon energy is accessible at the detector in segmented spacetime; includes all computational steps and physical interpretation. |


## Bound Energy Scripts and Validation

| File                                         | Purpose                                                                                                                                                                                           |
|----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| bound_energy_plot_with_frequenz_shift_fix.py | High-precision comparison between segmented spacetime (with ΔM correction) and classical gravitational redshift. Calculates, exports, and plots all values for selected astrophysical test cases. |
| bound_energy_plot.py                         | Same as above, but **without** ΔM correction. Pure numerical comparison of the models, including CSV export and plot.                                                                             |
| bound_energy_english.py                      | English version of the bound energy calculation script – implements all core functions, model comparison and CSV export for papers/presentations.                                                 |
| bound_energy_with_deltaM.csv                 | Exported CSV containing all calculated values from `bound_energy_plot_with_frequenz_shift_fix.py`.                                                                                                |



## 🚀 How to Run

Make sure you have Python 3 installed. Then simply run:

```bash
python segmented_full_proof.py
````

## ⚙️ Setup with Virtual Environment

To keep your environment clean and reproducible, it's recommended to run this project inside a virtual environment.

### 🧰 Steps

```bash
# 1. Create virtual environment (folder name: venv)
python3 -m venv venv

# 2. Activate the environment
# On Linux/macOS:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# 3. Install required dependencies
pip install -r requirements.txt
````
## Second Content

### `bound_energy.py`

Calculates the bound‐electron mass and emitted photon energy from a local frequency shift, using the segmented-spacetime model developed in:

> Wrede/Casu et al., “Segmented Spacetime: Bound Energy and the Structural Origin of the Fine-Structure Constant” (2025).

- **Usage**:  
  ```bash
  python bound_energy.py
  ````
## Third Content

`calculation_test.py`

`calculation_test.py` is the quick-start entry point for the **cycle-free mass calculation** via segment radius `r_phi`.

| Option / Mode      | Description                                                                                                  |
|--------------------|-------------------------------------------------------------------------------------------------------------|
| `--rphi <value>`   | Returns the mass in kilograms for a single measured `r_phi` value.                                           |
| `--demo`           | Runs a mini round (electron, moon, Earth, Sun) and demonstrates how precise the procedure works.             |

### Examples


# Calculate a single value
```
python calculation_test.py --rphi 1.0945634795e-57
````
# Start the demo round
```
python calculation_test.py --demo
````
### Fourth Content

## ✅ `final_test.py` – Roundtrip Validation of Segmented-Spacetime Mass Reconstruction

This script demonstrates that the segmented-spacetime model can reconstruct the rest mass of an object purely from its segmented radius – without relying on built-in constants like the Compton wavelength or classical radius.

### What It Does

- Takes known rest masses of test objects (electron, Moon, Earth, Sun).
- Computes the segmented radius using:

  r_phi = (G * m / c^2) * phi

- Then inverts that radius back into mass via:

  m = (c^2 * r_phi) / (G * phi)

- Finally, it compares the original mass (M_in) with the reconstructed mass (M_out), and prints the relative error.

### Why It Matters

- No circular dependency: The mass is not hidden in the inputs.
- No use of Compton wavelength or predefined scale lengths.
- The reconstruction is based only on geometry and physical constants.

This test directly avoids the circular logic found in other models, where mass is inserted via lambda_C and reappears in the result.

### Example Output

---

Segmented-Spacetime Roundtrip Mass Validation

## Objekt     M\_in \[kg]     r\_phi \[m]       M\_out \[kg]     rel. error

Electron   9.1094e-31    1.0946e-57      9.1094e-31      1.10e-50

Moon       7.3420e+22    8.8220e-5       7.3420e+22      1.36e-50

Earth      5.9722e+24    7.1761e-3       5.9722e+24      <1e-42

Sun        1.9885e+30    2.3893e+3       1.9885e+30      <1e-42

---

### Conclusion

The `final_test.py` script confirms:

- The segmented-spacetime model does not rely on hidden mass inputs.
- It is free of circular logic.
- Mass is derived from geometric structure alone.
- The numerical error is near machine precision.


This is a clean and direct demonstration that mass can be reconstructed from segmented spacetime – without assumptions, without shortcuts.

## Contents of `paper.py`

| Section                                      | Description                                                                                         |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------|
| 1. Constants & Imports                       | Naturkonstanten, mathematische Bibliotheken und Initialisierung                                      |
| 2. Effective Radius & Segmentation           | Definition und Berechnung von Segmentlänge, Segmentanzahl, effektivem Radius                        |
| 3. Classical Self-Energy                     | Berechnung der klassischen elektromagnetischen Selbstenergie                                         |
| 4. Structural Alpha Calculation              | Ableitung und Umkehrung der Feinstrukturkonstanten (α) aus strukturellen Parametern                 |
| 5. Effective Radius with Fixed Alpha         | Berechnung des klassischen Elektronenradius unter festen α- und m_e-Werten                          |
| 6. Segment Length Inversion                  | Rückrechnung der Segmentlänge ϕ aus Radius und Segmentanzahl                                        |
| 7. Bound vs Free Energy & Rydberg Energy     | Berechnung von gebundener/ungerichteter Energie, Rydberg-Energie                                    |
| 8. Photon Coupling Threshold                 | Berechnung der minimalen Wellenlänge und Grenzfrequenz für Photonen in segmentierter Raumzeit        |
| 9. Example Calculation: Sagittarius A* (S2)  | Vollständige Schritt-für-Schritt-Beispielrechnung aus dem Paper, numerisch reproduziert              |
| 10. Utility: Classical Electron Radius       | Direkter Nachweis der bekannten Werte aus α, m_e, c und e                                           |
| 11. Utility: Rydberg Energy                  | Demonstration des Energiebereichs gebundener Elektronen                                             |
| 12. Utility: Photon Threshold Wavelength     | Zusammenhang zwischen Feinstrukturkonstante und Photonenkopplung                                    |
| 13. Reference Statement                      | Klare Ausgabe/Print zur Zuordnung zum Originalpaper (DOI, Autoren, Jahr, Link)                      |

---

**Reference:**  
Carmen Wrede, Lino P. Casu, Bingsi (2025):  
_Segmented Spacetime – Bound Energy and the Structural Origin of the Fine-Structure Constant_  
Preprint · August 2025 · [DOI: 10.13140/RG.2.2.35006.80969](https://www.researchgate.net/publication/394248893)
---
## `complete-math.py` — Step-by-Step Script for Segmented Spacetime Theory

This script provides a **fully commented, didactic, and transparent step-by-step demonstration** of all key calculations from the papers by Carmen Wrede & Lino Casu, implementing the “Segmented Spacetime” model:

### What does the script do?

- **Mass reconstruction** from the segmented radius using the φ/2 constant and exponential correction, with **true Newtonian decimal-precision inversion**.
- **Calculation of the local fine-structure constant** α from a measured frequency (e.g., as in the S2/Sgr A* test), and computation of the associated bound electron mass and threshold photon wavelength.
- **Every single calculation step is explicitly explained in the output** — including all inputs, intermediate results, mathematical formulas, and the physical meaning of each result.

### Features

- **Explains every formula and physical constant** directly in the printout, line by line.
- **Reproduces the Earth mass example** from segmented radius, showing both theory and inversion.
- **Shows how to derive α<sub>local</sub> and m<sub>bound</sub>** from a single observed frequency.
- **Checks mathematical consistency** (e.g. α × m<sub>bound</sub> × c² / h should recover the input frequency).
- **Ideal for reviewers, teaching, or anyone who wants to understand the model without reading the full paper**.

### Usage

```bash
python complete-math.py
````
---
### Why is there an energy difference between emitter and detector? (Physical explanation)

The script `carmen_qed_incompleteness_demo.py` demonstrates that the classical idea of a photon "losing energy" as it travels through a gravitational field is incomplete.  
In the segmented spacetime model, the **measured energy at the detector** (e.g., on Earth) does **not** decrease because the photon "loses" energy, but because the **local segmentation** (the discrete structure of space at the detector) limits how much energy can be extracted from the photon.

- The photon's energy remains constant along its entire path.
- However, our measuring instruments (the electrons on Earth) can only "tap" a **fraction of the original photon energy** – this fraction is set by the local segmentation parameter (N).
- The stronger the gravitational field and the higher the segmentation at the detector, the less energy can be accessed from the original photon.
- The apparent energy loss is thus **not a real energy loss of the photon itself**, but an effect of the spacetime structure at the detector.

**Conclusion:**  
The observed energy difference is directly explained by our model – it is not due to energy dissipation "on the way", but to the **local coupling/segmentation** between the photon and the detector.
---
---

## QED Incompleteness Demo (`carmen_qed_incompleteness_demo.py`)

This script demonstrates why the classical formula `E = m_e * c^2` and even QED are incomplete when strong gravity or segmented spacetime are present:

- It uses a real astrophysical example (S2 star and Earth) to show how local segmentation (N) affects the measurable energy and the local electron mass.
- The script calculates, from observed and emitted frequencies, the local fine-structure constant (`alpha_local`) and the bound electron mass (`m_bound`).
- It explains and numerically demonstrates why, at the detector (e.g., on Earth), only a **portion of the original photon energy** can be accessed.
- All formulas, calculation steps, and interpretations are printed and explained.

**How to run:**
```bash
python carmen_qed_incompleteness_demo.py
````
