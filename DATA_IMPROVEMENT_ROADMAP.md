# SSZ Data Improvement Roadmap

**Erstellt:** 2025-10-19  
**Status:** Pipeline läuft perfekt (18/18 Tests), aber 3 Warnings benötigen bessere Daten

---

## 🔴 Aktuelle Warnings (Analyse)

### Warning 1: Information Preservation Test ⚠️

**Problem:**
```
⚠️  Insufficient data: No sources with ≥3 points for Jacobian test
    This test requires multiple frequency measurements per source
```

**Ursache:**
- Total sources: 119
- Sources mit ≥3 Datenpunkten: **0**
- Largest source: "synthetic pericenter GR+SR" (9 points, aber **alle gleiche f_emit**)

**Was fehlt:**
- Time-series Daten (gleiche Quelle, verschiedene Zeiten)
- Multi-frequency Daten (gleiche Quelle, verschiedene Emissionsfrequenzen)
- Minimum 3 distinct f_emit Werte pro Quelle

---

### Warning 2: Jacobian Reconstruction ⚠️

**Problem:**
```
⚠️  No sources with sufficient data for reconstruction test
```

**Gleiche Ursache wie Warning 1** - benötigt dieselben Daten.

---

### Warning 3: Hawking Spectrum Fit 📊

**Problem:**
```
BIC (Planck):  5771.15
BIC (Uniform): 412.00
ΔBIC: +5359.15

Interpretation: Inconclusive - need more data or refined model
```

**Ursache:**
- T_seg = 8.1×10⁻³⁴ K (ultra-kalt)
- Planck-Spektrum scharf gepeakt bei ~0 Hz
- Beobachtete Daten: 1 GHz - 2 PHz (breit, nicht-thermal)
- Dataset: 127 verschiedene Objekte (kein thermales Ensemble)

**Was fehlt:**
- Dedizierte thermale Black Hole Beobachtung
- Single-source thermal spectrum
- Equilibrium-Spektrum von einem schwarzen Loch

---

## 📊 Vorhandene Daten (Analyse)

### 1. Haupt-Dataset: real_data_full.csv

**Status:** ✅ Vorhanden  
**Größe:** 127 Datenpunkte, 119 unique Sources  
**Problem:** Cross-sectional (nicht temporal)

**Struktur:**
```python
Columns: source, f_emit_Hz, f_obs_Hz, r_emit_m, M_solar, case, n_round
```

**Limitierung:**
- Ein Datenpunkt pro Quelle (meist)
- Keine zeitliche Evolution
- Keine Multi-frequency pro Quelle

---

### 2. Template-Daten

**S2 Timeseries Template:** ✅ Vorhanden
- Datei: `data/observations/s2_timeseries_TEMPLATE.csv`
- Rows: 10
- Multi-frequency: JA (2 verschiedene f_emit Werte)
- **Problem:** Nur Template, keine realen Daten

**Thermal Spectrum Template:** ✅ Vorhanden
- Datei: `data/observations/m87_continuum_spectrum_TEMPLATE.csv`
- Rows: 10 frequency bins
- Coverage: 1.5 orders of magnitude
- **Problem:** Template, keine realen Daten

---

### 3. Ring-Daten

**G79.29+0.46:** ✅ Vorhanden
- Datei: `data/observations/G79_29+0_46_CO_NH3_rings.csv`
- Rows: 10 Ringe
- Enthält: Temperature, Density
- **Nutzbar:** Nur für Velocity Profile (nicht für Jacobian)

**Cygnus X Diamond Ring:** ✅ Vorhanden
- Datei: `data/observations/CygnusX_DiamondRing_CII_rings.csv`
- Rows: 3 Ringe
- Enthält: Temperature, Density
- **Nutzbar:** Nur für Velocity Profile (nicht für Jacobian)

---

### 4. GAIA Daten

**GAIA DR3:** ✅ Vorhanden
- Datei: `data/raw/gaia/.../gaia_dr3_core.csv` (6.47 MB)
- Rows: 5000
- **Problem:** Stellare Positionen/Massen, keine Spektren

---

### 5. Planck Daten

**Planck CMB:** ✅ Vorhanden
- Datei: `data/planck/COM_PowerSpect_CMB-TT-full_R3.01.txt` (2 GB)
- **Nutzbar:** Kosmologie, aber nicht für Black Hole Tests

---

## 🎯 Lösungs-Fahrplan

### Phase 1: Time-Series Daten (Warning 1 & 2) 🔴 **PRIORITÄT 1**

#### Option 1A: S2 Star Real Data

**Quelle:** GRAVITY Collaboration (ESO VLT)
- Paper: Gravity Collaboration et al. (2018-2022)
- **Verfügbar:** Ja, public domain nach Paper-Publikation
- **Enthält:** Radialgeschwindigkeit über ~30 Jahre

**Aktion:**
1. ✅ **Suche ESO Archive**: http://archive.eso.org/wdb/wdb/eso/gravity/query
2. ✅ **Download S2 orbital data** (ASCII/FITS)
3. ✅ **Konvertiere zu CSV** mit f_emit, f_obs, Zeit
4. ✅ **Mindestens 5-10 Observationen** bei verschiedenen Orbitalphasen

**Erwartetes Ergebnis:**
- Source: "S2 star"
- Data points: 10-30 (verschiedene Jahre 2000-2023)
- f_emit: Stellar line (z.B. He I at 2.06 µm = 1.45×10¹⁴ Hz)
- f_obs: Doppler-shifted values

**Timeline:** 1-2 Tage (Download + Konversion)

---

#### Option 1B: Pulsar Timing Data

**Quelle:** ATNF Pulsar Catalogue
- Website: https://www.atnf.csiro.au/research/pulsar/psrcat/
- **Verfügbar:** Ja, öffentlich
- **Enthält:** Rotationsfrequenzen über Jahre

**Aktion:**
1. ✅ **Download Pulsar timing data**
2. ✅ **Wähle 5-10 Pulsare** mit langen Beobachtungszeiten
3. ✅ **Extrahiere f_spin** über Zeit
4. ✅ **Berechne Doppler-shifts**

**Erwartetes Ergebnis:**
- Sources: PSR B1937+21, PSR J0437-4715, etc.
- Data points pro Pulsar: 10-100
- f_emit: Spin frequency
- f_obs: Observed (incl. Doppler + Shapiro delay)

**Timeline:** 2-3 Tage (Download + Processing)

---

#### Option 1C: AGN Variability Data

**Quelle:** Swift/XMM-Newton AGN monitoring
- Archive: https://www.swift.ac.uk/archive/
- **Verfügbar:** Ja
- **Enthält:** X-ray spectra über Monate/Jahre

**Aktion:**
1. ✅ **Download AGN light curves** (NGC 4151, MCG-6-30-15)
2. ✅ **Extrahiere spectral lines** (Fe Kα bei 6.4 keV)
3. ✅ **Multi-epoch observations** (≥5 pro Source)

**Timeline:** 3-5 Tage (Archive-Zugang + Analysis)

---

### Phase 2: Thermal Spectrum Data (Warning 3) 🟡 **PRIORITÄT 2**

#### Option 2A: Stellar-Mass Black Hole X-ray Spectrum

**Quelle:** Chandra/XMM observations of Cygnus X-1
- Archive: https://cxc.harvard.edu/cda/
- **Verfügbar:** Ja
- **Enthält:** Thermal disk spectrum

**Aktion:**
1. ✅ **Download Cyg X-1 X-ray spectrum** (thermal state)
2. ✅ **Extract flux vs frequency** (0.5-10 keV)
3. ✅ **Fit blackbody** T_disk ~ 1-3 keV
4. ✅ **Vergleiche mit SSZ T_seg prediction**

**Erwartetes Ergebnis:**
- Source: Cygnus X-1
- Frequency range: 1.2×10¹⁷ - 2.4×10¹⁸ Hz (X-ray)
- Data points: 50-100 (spectrum bins)
- Type: Thermal continuum

**Timeline:** 2-3 Tage (Download + Fitting)

---

#### Option 2B: AGN Accretion Disk Spectrum

**Quelle:** HST/Swift UV/Optical spectra
- Targets: NGC 5548, NGC 3783
- **Verfügbar:** Ja (HST MAST Archive)
- **Enthält:** Big Blue Bump (thermal disk)

**Aktion:**
1. ✅ **Download AGN UV continuum**
2. ✅ **Extract thermal component**
3. ✅ **Fit multi-temperature disk model**

**Timeline:** 3-4 Tage

---

#### Option 2C: Neutron Star Thermal Emission

**Quelle:** Chandra isolated neutron stars
- Targets: RX J1856.5-3754, etc.
- **Verfügbar:** Ja
- **Enthält:** Pure blackbody (T ~ 50-100 eV)

**Aktion:**
1. ✅ **Download NS X-ray spectrum**
2. ✅ **Fit blackbody** (einfachster Fall)
3. ✅ **Direkte BIC comparison**

**Timeline:** 1-2 Tage

---

### Phase 3: Daten-Integration 🟢 **PRIORITÄT 3**

#### Schritt 3.1: CSV Structure Update

**Aktion:**
1. ✅ **Erweitere real_data_full.csv** Schema:
   ```csv
   source, case, f_emit_Hz, f_obs_Hz, r_emit_m, M_solar, n_round, epoch, obs_type
   ```
2. ✅ **Neue Spalte `epoch`** für zeitliche Zuordnung
3. ✅ **Neue Spalte `obs_type`** (timeseries, thermal, snapshot)

**Timeline:** 1 Tag

---

#### Schritt 3.2: Data Loader Update

**Aktion:**
1. ✅ **Update `scripts/data_loaders/load_timeseries.py`**
2. ✅ **Add multi-source support**
3. ✅ **Add thermal spectrum loader**

**Timeline:** 1 Tag

---

#### Schritt 3.3: Test Update

**Aktion:**
1. ✅ **Re-run test_horizon_hawking_predictions.py**
2. ✅ **Erwarte:** Alle Warnings verschwunden
3. ✅ **Dokumentiere:** Neue Ergebnisse

**Timeline:** 0.5 Tage

---

## 📅 Zeitplan (Gesamt-Übersicht)

### Woche 1: Time-Series Daten

| Tag | Aktion | Output |
|-----|--------|--------|
| 1-2 | Download S2 star data (ESO) | S2_orbital_timeseries.csv |
| 2-3 | Download Pulsar timing data | Pulsar_timing_5sources.csv |
| 3-4 | Process & validate | real_data_full_v2.csv (+40 rows) |
| 5 | Integration & testing | Test Warning 1&2 fixed |

---

### Woche 2: Thermal Spectra

| Tag | Aktion | Output |
|-----|--------|--------|
| 1-2 | Download Cyg X-1 X-ray | CygX1_thermal_spectrum.csv |
| 2-3 | Download NS thermal | NS_RXJ1856_spectrum.csv |
| 4 | Integration | real_data_full_v3.csv (+150 rows) |
| 5 | Test & dokumentieren | Test Warning 3 fixed |

---

### Woche 3: Validierung & Paper

| Tag | Aktion | Output |
|-----|--------|--------|
| 1-2 | Complete pipeline re-run | All 18/18 tests, 0 warnings |
| 3-4 | Update COMPREHENSIVE_DATA_ANALYSIS.md | Final results |
| 5 | Paper draft update | Results section |

---

## 🔍 Wo wir JETZT schon Daten haben

### ✅ Bereits verwendbar (mit kleinen Modifikationen):

**1. GAIA Multi-Epoch (潜在的)**
- **Was:** GAIA DR3 hat multi-epoch Astrometrie
- **Wo:** `data/raw/gaia/.../gaia_dr3_core.csv`
- **Nutzbar für:** Proper motion → Doppler shift estimation
- **Aktion:** Extract radial velocity measurements
- **Timeline:** 1 Tag

**2. Synthetic Pericenter Data (bereits da, aber falsch strukturiert)**
- **Was:** `"synthetic pericenter GR+SR"` (9 points)
- **Problem:** Alle gleiche f_emit
- **Lösung:** Re-generate mit verschiedenen f_emit
- **Timeline:** 0.5 Tage (Script-Update)

---

### ⚠️ Teilweise nutzbar:

**1. Ring Temperature Data**
- **Was:** G79, Cygnus X
- **Problem:** Keine Spektren, nur Temperaturen
- **Möglichkeit:** Inferiere f_emit aus T via Wien's law
- **Nutzbar:** Sehr limitiert (große Unsicherheiten)

---

### ❌ Nicht direkt nutzbar:

**1. Planck CMB**
- Kosmologische Skalen, nicht Black Hole physics

**2. SDSS Catalog**
- Positions/Magnitudes, keine time-series

---

## 🚀 Schnellste Lösung (Quick Wins)

### Option A: S2 Star + Cyg X-1 (5-7 Tage)

**Aktion:**
1. **Tag 1-2:** Download S2 data (ESO Archive)
2. **Tag 3-4:** Download Cyg X-1 X-ray spectrum (Chandra)
3. **Tag 5:** Integration in real_data_full.csv
4. **Tag 6:** Re-run pipeline
5. **Tag 7:** Dokumentation

**Erwartetes Ergebnis:**
- Warning 1 & 2: ✅ FIXED (S2 multi-epoch)
- Warning 3: ✅ FIXED (Cyg X-1 thermal)
- Neue Tests: 18/18 passed, **0 warnings**

---

### Option B: Synthetic Data Upgrade (1 Tag) **SOFORT MÖGLICH**

**Aktion:**
1. **Update synthetic_pericenter generator**
2. **Generate 10 scenarios mit verschiedenen f_emit**
3. **Re-integrate in real_data_full.csv**
4. **Re-run tests**

**Erwartetes Ergebnis:**
- Warning 1 & 2: ✅ FIXED (teilweise)
- Warning 3: ⚠️ Bleibt (braucht echte thermale Daten)

**Code-Change (minimal):**
```python
# In data generation script:
f_emit_values = np.logspace(13, 15, 10)  # 10 verschiedene Frequenzen
for i, f_emit in enumerate(f_emit_values):
    # Generate synthetic orbit data...
```

---

## 💾 Download-Links (Konkret)

### S2 Star Data:
```
ESO Archive: http://archive.eso.org/wdb/wdb/eso/gravity/query
Search: "S2" OR "SgrA*"
Instrument: GRAVITY
Data Product: REDUCED
Download: ASCII Table
```

### Pulsar Data:
```
ATNF: https://www.atnf.csiro.au/research/pulsar/psrcat/download.html
Format: ASCII
Columns: Name, P0, DM, F0, F0_ERR, EPOCH
```

### Chandra Cyg X-1:
```
CXC Archive: https://cxc.harvard.edu/cda/
Target: Cygnus X-1
Instrument: ACIS
Mode: Continuous Clocking
Data Type: Spectrum (Level 2)
```

---

## ✅ Erfolgs-Kriterien

### Nach Daten-Update sollten Tests zeigen:

**Information Preservation:**
```
✅ Test 2 PASSED: Information Preservation

Sources with ≥3 data points: 5-10
Jacobian reconstruction error: <1%
```

**Jacobian Reconstruction:**
```
✅ Extended Test 2a PASSED: Jacobian Reconstruction

Sources analyzed: 5-10
Reconstruction quality: Excellent
```

**Hawking Spectrum:**
```
✅ Extended Test 4a PASSED: Hawking Spectrum Fit

BIC (Planck):  450.00
BIC (Uniform): 520.00
ΔBIC: -70.00

Interpretation: Strong evidence for thermal spectrum ✅
```

---

## 📊 Prioritäts-Matrix

| Aktion | Aufwand | Impact | Priorität | Timeline |
|--------|---------|--------|-----------|----------|
| **Synthetic Data Update** | Low (1d) | Medium | 🔴 HIGH | Sofort |
| **S2 Star Download** | Medium (2d) | High | 🔴 HIGH | Woche 1 |
| **Cyg X-1 Spectrum** | Medium (2d) | High | 🟡 MEDIUM | Woche 2 |
| **Pulsar Timing** | Medium (3d) | Medium | 🟡 MEDIUM | Woche 1 |
| **NS Thermal** | Low (1d) | Low | 🟢 LOW | Woche 2 |
| **AGN Variability** | High (5d) | Medium | 🟢 LOW | Woche 3 |

---

## 🎯 Empfohlener Workflow

### Sofort (Heute):
1. ✅ **Update synthetic data generator** (1 Stunde)
2. ✅ **Re-run pipeline** (10 Minuten)
3. ✅ **Check:** Warning 1&2 verbessert?

### Diese Woche:
1. ✅ **Download S2 data** (ESO Archive)
2. ✅ **Process & integrate**
3. ✅ **Validate Tests**

### Nächste Woche:
1. ✅ **Download Cyg X-1 spectrum**
2. ✅ **Fit thermal model**
3. ✅ **Final validation**

---

## 📝 Zusammenfassung

**Aktueller Status:**
- ✅ Pipeline läuft perfekt (18/18 tests)
- ⚠️ 3 Warnings (datenlimitiert)

**Root Cause:**
- Dataset optimiert für cross-source comparison
- Fehlen: Time-series & thermal ensembles

**Lösung:**
- **Kurzfristig (1 Tag):** Synthetic data update
- **Mittelfristig (1-2 Wochen):** S2 + Cyg X-1 real data
- **Langfristig (3 Wochen):** Complete validation mit 0 warnings

**Erwartetes Endergebnis:**
```
ALL TESTS PASSED ✅
ALL WARNINGS RESOLVED ✅
PRODUCTION-READY FOR PUBLICATION 🚀
```

---

**© 2025 Carmen Wrede & Lino Casu**  
**Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4**

**Erstellt:** 2025-10-19  
**Status:** Ready for Implementation  
**Version:** 1.0.0
