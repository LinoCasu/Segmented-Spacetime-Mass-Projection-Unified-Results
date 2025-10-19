# real_data_full.csv - Column Documentation

## 📊 **Column Categories**

### **Category 1: CRITICAL (Required for ALL sources)**

These columns must be filled for **every single row**. NaN here is an error.

| Column | Description | Unit | Must be filled |
|--------|-------------|------|----------------|
| `source` | Source name | - | ✅ Always |
| `f_emit_Hz` | Emitted frequency | Hz | ✅ Always |
| `f_obs_Hz` | Observed frequency | Hz | ✅ Always |
| `r_emit_m` | Emission radius | m | ✅ Always |
| `M_solar` | Mass in solar masses | M☉ | ✅ Always |
| `n_round` | Segment count | - | ✅ Always |
| `z` | Redshift | - | ✅ Always |

**Used by:** ALL tests

**Current status:** ✅ 285/285 filled (100%)

---

### **Category 2: ORBITAL PARAMETERS (Only for binary systems/orbits)**

These columns are **only applicable** to sources with orbital motion (S2, binary pulsars, X-ray binaries).

| Column | Description | Unit | Applicable to |
|--------|-------------|------|---------------|
| `a_m` | Semi-major axis | m | Orbital sources only |
| `e` | Eccentricity | - | Orbital sources only |
| `P_year` | Orbital period | years | Orbital sources only |
| `T0_year` | Periastron epoch | years | Orbital timing only |
| `f_true_deg` | True anomaly | degrees | Orbital timing only |

**Used by:** 
- `test_orbital_parameters.py` (filters with `.notna()`)
- Orbital analysis scripts

**NaN is CORRECT for:**
- ✅ Continuum spectra (M87, Sgr A* from NED)
- ✅ Single stars
- ✅ Non-binary pulsars

**Current status (427 rows total):** 
- 143 rows WITH orbital params (S2, pulsars, binaries - 115 unique sources)
- 284 rows WITHOUT orbital params (M87 + Sgr A* NED continuum spectra - 2 unique sources, 142 rows each, correct!)

---

### **Category 3: WAVELENGTH (Optional - frequency is primary)**

Wavelength is redundant with frequency (λ = c/f). We use frequency as primary.

| Column | Description | Unit | When filled |
|--------|-------------|------|-------------|
| `lambda_emit_nm` | Emitted wavelength | nm | Optional |
| `lambda_obs_nm` | Observed wavelength | nm | Optional |

**Used by:** Visualization scripts (can calculate from frequency)

**NaN is OK:** Most sources only have frequency, not wavelength

**Current status:** 113 filled, 172 NaN (optional!)

---

### **Category 4: VELOCITY (Only for Doppler measurements)**

| Column | Description | Unit | When filled |
|--------|-------------|------|-------------|
| `v_los_mps` | Line-of-sight velocity | m/s | Doppler sources only |
| `v_tot_mps` | Total velocity | m/s | Orbital/motion sources |

**Used by:** 
- Velocity analysis (filters with `.notna()`)
- Orbital motion studies

**NaN is CORRECT for:**
- ✅ Stationary sources
- ✅ Spectra without velocity info

**Current status:** 113 filled, 172 NaN (correct!)

---

### **Category 5: ANALYSIS HINTS (Optional analysis parameters)**

| Column | Description | Unit | When filled |
|--------|-------------|------|-------------|
| `z_geom_hint` | Geometric redshift hint | - | Optional |
| `N0` | Analysis parameter | - | Optional |
| `category` | Source category | - | Classification |

**Used by:** Specific analysis scripts

**NaN is OK:** Not required for standard tests

**Current status:** Various (optional columns)

---

## 🎯 **How Tests Handle NaN:**

### **Example 1: Orbital Parameters Test**
```python
def test_orbital_parameters():
    df = pd.read_csv('real_data_full.csv')
    
    # Filter ONLY orbital sources (NaN excluded automatically!)
    orbital = df[df['a_m'].notna() & df['e'].notna() & df['P_year'].notna()]
    
    assert len(orbital) > 0, "Need at least one orbital source"
    
    # Test only on orbital sources
    assert (orbital['e'] >= 0).all()
    assert (orbital['e'] < 1).all()  # Elliptical orbits
```

### **Example 2: Spectrum Test**
```python
def test_spectrum():
    df = pd.read_csv('real_data_full.csv')
    
    # ALL sources must have frequency (no NaN allowed!)
    assert df['f_obs_Hz'].notna().all()
    assert df['f_emit_Hz'].notna().all()
    
    # Test on all 285 sources
    assert (df['f_obs_Hz'] > 0).all()
```

### **Example 3: Multi-Frequency Test**
```python
def test_multifreq():
    df = pd.read_csv('real_data_full.csv')
    
    # Group by source, count frequencies
    freq_count = df.groupby('source')['f_obs_Hz'].count()
    
    # Sources with multiple frequencies
    multifreq = freq_count[freq_count >= 3]
    
    assert len(multifreq) > 0, "Need multi-frequency sources"
```

---

## ✅ **Best Practices:**

### **DO:**
- ✅ Use `.notna()` filters for optional columns
- ✅ Check critical columns with `.notna().all()`
- ✅ Document which columns are required for each test
- ✅ Use `dropna(subset=['col1', 'col2'])` for specific tests

### **DON'T:**
- ❌ Assume all columns are always filled
- ❌ Use `df.dropna()` without `subset=` (drops too much!)
- ❌ Treat NaN as error in optional columns
- ❌ Create separate datasets for each test

---

## 🔬 **Why This Approach is Scientific Standard:**

### **Real-World Examples:**

**1. GAIA DR3 (1.8 billion stars):**
```
parallax: filled for all
radial_velocity: NaN for ~90% (no RV measurement)
→ Tests filter: gaia[gaia['radial_velocity'].notna()]
```

**2. SDSS DR17 (millions of galaxies):**
```
z_photo: filled for all
z_spec: NaN for ~70% (no spectroscopy)
→ Tests filter: sdss[sdss['z_spec'].notna()]
```

**3. Chandra X-ray Catalog:**
```
x_ray_flux: filled for all
optical_magnitude: NaN for ~50% (no optical counterpart)
→ Multi-wavelength tests filter on .notna()
```

---

## 📊 **Current Dataset Status (285 rows):**

```
Critical Columns (7):     285/285 filled (100%) ✅
Orbital Parameters (5):   143/285 filled (50%) - CORRECT for source types
Wavelength (2):           113/285 filled (40%) - Optional (have frequency!)
Velocity (2):             113/285 filled (40%) - CORRECT for source types
Analysis Hints (3):       Various - Optional

Total NaN: 1999 / 5700 cells (35%)
  → ALL in optional/not-applicable columns ✅
  → 0% in critical columns ✅
```

---

## 🚨 **Error Cases (When to worry):**

### **❌ BAD: NaN in critical column**
```python
source  f_obs_Hz  r_emit_m  M_solar
M87     2.3e11    NaN       6.5e9     ← ERROR! r_emit required!
```
**Action:** Fill or remove row

### **✅ GOOD: NaN in optional column**
```python
source  f_obs_Hz  a_m       e
M87     2.3e11    NaN       NaN       ← OK! M87 spectrum has no orbit
S2      2.2e14    1.451e14  0.88      ← OK! S2 has orbital params
```
**Action:** None needed (scientifically correct!)

---

## 🎯 **Future Data Additions:**

When adding new data sources:

### **1. Check applicability:**
```python
# Example: Adding new M87 spectrum point
new_row = {
    # ALWAYS fill:
    'source': 'M87',
    'f_obs_Hz': 1.4e9,
    'f_emit_Hz': 1.4059e9,
    'r_emit_m': 1.2e13,
    'M_solar': 6.5e9,
    'n_round': calculate_n(r, M),
    'z': 0.0042,
    
    # Only if applicable:
    'a_m': np.nan,  # No orbit for continuum spectrum
    'e': np.nan,
    'v_los_mps': np.nan  # No Doppler measurement
}
```

### **2. Verify critical columns:**
```python
assert new_df[critical_cols].notna().all().all()
```

### **3. Document NaN rationale:**
```
Add to commit message:
"NaN in orbital params: source is continuum spectrum (no orbital motion)"
```

---

## 📚 **References:**

**Pandas Best Practices:**
- https://pandas.pydata.org/docs/user_guide/missing_data.html

**Astropy Unified I/O:**
- https://docs.astropy.org/en/stable/io/unified.html

**GAIA Archive:**
- https://gea.esac.esa.int/archive/

---

© 2025 Carmen Wrede, Lino Casu  
Licensed under the ANTI-CAPITALIST SOFTWARE LICENSE v1.4

**Version:** 1.0.0  
**Last Updated:** 2025-10-19  
**Dataset Rows:** 285  
**Critical Columns Complete:** ✅ 100%
