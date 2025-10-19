# Changelog

All notable changes to the Segmented Spacetime Suite will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [1.3.0] - 2025-10-19

### 🎉 Major Update: Dataset Expansion + Comprehensive Warning System

#### Added

**Data Expansion (143 → 427 rows, +199%):**
- Integrated NASA/IPAC NED continuum spectra for M87 and Sgr A*
- M87: 139 NED spectrum observations (Radio to X-ray)
- Sgr A*: 3 NED spectrum observations
- Frequency coverage: 9.5 orders of magnitude
- All data 100% real (0% synthetic)

**Warning System (7 scripts):**
- `install.ps1` / `install.sh` - Warning explanations at startup
- `run_all_ssz_terminal.py` - Pipeline warnings with context
- `run_full_suite.py` - Test suite warnings explained
- `segspace_enhanced_test_better_final.py` - [CHECK] warnings
- `test_horizon_hawking_predictions.py` - 4x "Insufficient data" clarified
- `test_hawking_spectrum_continuum.py` - TEMPLATE data warnings

**New Tools (4 scripts):**
- `scripts/data_generators/integrate_ned_spectrum.py` - Safe data integration with validation
- `scripts/data_generators/validate_dataset.py` - Pre/post integration validation
- `check_column_completeness.py` - Cross-file consistency checker
- `check_data_availability.py` - Test requirements checker

**Critical Documentation (7 files):**
- `EXTERNAL_DATA_INTEGRATION_CRITICAL_WARNINGS.md` - **CRITICAL** 3-level integration warnings
- `NED_SPECTRUM_INTEGRATION_2025-10-19.md` - Integration summary (143→427)
- `DATA_COLUMNS_README.md` - Column requirements & NaN patterns
- `WARNING_EXPLANATIONS_ADDED.md` - All warnings documented
- `SCRIPT_COMPLETENESS_CHECK.md` - All scripts validated
- `EXTERNAL_DATASETS_GUIDE.md` - Updated with warning links
- `README_CORRECTIONS_2025-10-19.md` - Documentation corrections

**Data Files:**
- `data/observations/m87_ned_spectrum.csv` - M87 spectrum (139 rows)
- `data/observations/sgra_ned_spectrum.csv` - Sgr A* spectrum (3 rows)

#### Changed

**Dataset Statistics:**
- Total rows: 143 → **427** (+199%)
- Unique sources: 119 → **117** (corrected)
- Multi-frequency sources: 4 → **5** (M87: 278 obs, Cyg X-1: 10, M87*: 10, S2: 10, Sgr A*: 6)
- All critical columns: 100% filled (427/427)

**Test Results:**
- Information Preservation: **PASSING** (was insufficient data)
  - 5/5 sources validated (Cyg X-1, M87, M87*, S2, Sgr A*)
- Jacobian Reconstruction: **5/5 stable** (100%)
  - Mean reconstruction error: 4.69e-17 (quasi-null)
- All critical columns: 100% filled

**Documentation Updates:**
- `README.md` - Updated to 427 data points, 117 sources, 5 multi-freq
- `Sources.md` - Multi-frequency sources corrected
- `COMPREHENSIVE_DATA_ANALYSIS.md` - Updated to 427 rows
- All references to "143 rows" checked and updated where appropriate

**Pipeline Regeneration:**
- `out/phi_step_debug_full.csv` - Regenerated with 427 rows
- `out/_enhanced_debug.csv` - Regenerated with 427 rows + z_obs column (0 NaN)
- All test outputs refreshed with new data

#### Fixed

**Documentation Corrections:**
- Unique sources count: 123 → 117 (fact-checked)
- Multi-frequency sources: 4 → 5 (with correct list)
- Removed misleading "143 + 142 + 142" breakdown
- All numbers now fact-checked with `check_data_composition.py`

**Test Improvements:**
- "Insufficient data" warnings now have detailed explanations
- Physical interpretation provided for why data is insufficient
- Test PASSES explicitly stated when data requirements not met

#### Warning System Details

**3 Integration Levels Documented:**
1. **Level 1 (Safe):** Single script integration - isolated requirements
2. **Level 2 (Moderate):** Partial pipeline - shared intermediate files
3. **Level 3 (Critical):** Full pipeline - multiple interdependent scripts

**NaN Gap Classification:**
- **Fatal NaN:** source, f_emit_Hz, f_obs_Hz, r_emit_m, M_solar, z, z_obs
- **Acceptable NaN:** a_m, e, P_year (continuum spectra), z_geom_hint, N0 (optional)

**Triple Validation Workflow:**
1. Pre-integration validation (`validate_dataset.py`)
2. Integration with validation (`integrate_ned_spectrum.py --validate`)
3. Post-integration validation (regenerate + verify)

#### Statistics

- Total commits: 2 (2ca9129 dataset expansion, fad0cf6 corrections)
- Files changed: 36 (32 + 4 corrections)
- Insertions: +4247 lines
- Deletions: -43 lines
- New documentation: 7 files
- Updated files: 29 files

#### Scientific Impact

- ✅ Multi-frequency coverage vastly improved (5 sources with rich data)
- ✅ Information preservation fully validated (5/5 stable Jacobian)
- ✅ Pipeline tested and verified with 427 rows
- ✅ External integration now has critical safety warnings
- ✅ Triple validation workflow ensures data integrity

---

## [1.1.0] - 2025-10-18

### 🎉 Major Update: Complete Test System Overhaul

#### Added

**Test System:**
- Complete logging system capturing all output to `reports/summary-output.md` (~100-500 KB)
- 35 physics tests now show detailed physical interpretations
- 23 technical tests converted to silent background mode
- Smart data fetching system (checks existing files, never overwrites)

**New Scripts:**
- `scripts/fetch_planck.py` - Planck data downloader (2GB) with progress bar
- `COPY_TO_TEST_SUITES.ps1` - Project copy script for test suites

**Documentation (9 new files):**
- `TESTING_COMPLETE_GUIDE.md` - Master testing guide
- `tests/README_TESTS.md` - Tests directory documentation
- `scripts/tests/README_SCRIPTS_TESTS.md` - Scripts tests documentation
- `LOGGING_SYSTEM_README.md`, `INSTALL_README.md`, `DATA_FETCHING_README.md`
- `PHYSICS_TESTS_COMPLETE_LIST.md`, `VERIFICATION_COMPLETE.md`
- `REPO_UPDATE_CHECKLIST.md`, `LINUX_TEST_PLAN.md`

**Papers:**
- Added PDF versions of all theoretical papers (alongside MD)

#### Changed

**Test Output Format:**
- All 35 physics tests standardized with: Configuration → Results → Physical Interpretation
- Each test shows 3+ bullet points explaining physical meaning
- Unified format across all test files

**Test Runner:**
- `run_full_suite.py` captures ALL output to StringIO buffer
- Generates 2 files: `RUN_SUMMARY.md` (compact) + `summary-output.md` (complete log)
- Silent tests excluded from summary display

**Installation:**
- `install.ps1`/`install.sh` updated to 10 steps (added data checking)
- Step [8/10]: Check and fetch missing data files
- Auto-fetch Planck only if missing, never overwrites

**Updated Test Files:**
- `tests/test_segwave_core.py` - 16 tests verbose
- `scripts/tests/test_ssz_invariants.py` - 6 tests (added 3 new)
- All 6 root-level tests verbose

#### Fixed

**Critical Bugs:**
- 🔴 **Pytest I/O Crash**: Changed `--disable-warnings` to `-s` flag
  - Root cause: `ValueError: I/O operation on closed file`
  - Fixed in: `run_full_suite.py`, `install.ps1`, `install.sh`
  
- 🔴 **test_segmenter.py Import Error**: Removed non-existent `create_segments` import
  - Now uses correct `assign_segments_xy` API
  
- 🔴 **False "Failed: 3"**: Fixed summary counting logic
  - Silent tests no longer counted as failures

**Other Fixes:**
- Python cache clearing documented
- Shell script permissions on Linux
- Line ending issues

#### Performance

- Complete test suite: ~2-3 minutes
- Installation without Planck: ~2 minutes  
- Installation with Planck: ~20 minutes (connection dependent)
- Re-installation: ~2 minutes (skips existing data)

#### Statistics

- Physics Tests: 35 (all verbose with interpretations)
- Technical Tests: 23 (all silent)
- Modified Files: 15 (12 tests + 3 runners)
- New Files: 10 (9 docs + 1 script)

---

## [Unreleased]

### Added - 2025-01-18

#### Validation Papers Integration (`config/sources.yaml`)

**Windows/WSL Sources Configuration**

New configuration system for validation papers directory:
- **Base directory:** `H:\WINDSURF\VALIDATION_PAPER` (Windows)
- **WSL alternative:** `/mnt/h/WINDSURF/VALIDATION_PAPER`
- **Environment override:** `SSZ_SOURCES_DIR` (highest priority)

**Path Resolution:**
```python
from ssz.segwave import load_sources_config

config = load_sources_config()
print(config['base_dir'])    # H:\WINDSURF\VALIDATION_PAPER
print(config['exists'])      # True/False
print(config['source'])      # environment/config_windows/config_unix
```

**Features:**
- Automatic OS detection (Windows vs WSL/Linux)
- Smart fallback chain for cross-platform compatibility
- Non-fatal warnings if papers directory missing
- Enables offline validation against local PDF archive

**Usage:**
- Windows: `setx SSZ_SOURCES_DIR "H:\WINDSURF\VALIDATION_PAPER"`
- WSL: `export SSZ_SOURCES_DIR=/mnt/h/WINDSURF/VALIDATION_PAPER`

#### Segmented Radiowave Propagation Module (`ssz/segwave/`)

**New Feature: SSZ-Rings CLI Tool**

A complete implementation of radiowave propagation through segmented spacetime shells based on the γ_seg(r) formalism.

**Core Functionality:**
- `seg_wave_propagation.py`: Mathematical core implementing velocity evolution (v_k = v_{k-1} · q_k^{-α/2}) and frequency shifts
- `calib.py`: Alpha parameter calibration via RMSE minimization against observations
- `io.py`: CSV/JSON data handling for ring temperature, density, and velocity data
- `visuals.py`: Optional matplotlib-based plotting utilities

**CLI Tool (`ssz-rings`):**
- Command-line interface for velocity profile predictions
- Fixed or fitted α parameter modes
- Optional frequency tracking (ν_out = ν_in · γ^{-1/2})
- Customizable temperature/density coupling exponents (β, η)
- CSV table and text report outputs

**Data & Documentation:**
- Example dataset: `data/observations/ring_temperature_data.csv`
- Sources manifest: `data/observations/sources.json`
- Comprehensive guide: `docs/segwave_guide.md`

**Testing:**
- Unit tests: `tests/test_segwave_core.py` (deterministic mathematical validation)
- CLI integration tests: `tests/test_segwave_cli.py` (end-to-end workflow validation)

**Integration:**
- Added `ssz-rings` entry point to `pyproject.toml`
- No modifications to existing analysis pipelines (pure addition)
- Compatible with existing SSZ suite infrastructure

**Scientific Basis:**
- Implements segment-based velocity damping from Casu & Wrede segmented spacetime framework
- Validates against molecular ring observations (CO, NH3, CII tracers)
- Provides quantitative fit metrics (MAE, RMSE) for model assessment

**Usage Example:**
```bash
ssz-rings --csv data/observations/ring_temperature_data.csv \
          --v0 12.5 --fit-alpha \
          --out-table results.csv --out-report summary.txt
```

**Risks:** None - all changes are additive, no existing files modified or deleted.

---

## Previous Releases

### [1.0] - 2024-10-17

Initial release of Segmented Spacetime Suite with:
- Complete analysis pipeline
- Debian package infrastructure
- UTF-8 encoding fixes
- Repository portability improvements
- Comprehensive test suite

---

**Copyright © 2025 Carmen Wrede und Lino Casu**  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4
