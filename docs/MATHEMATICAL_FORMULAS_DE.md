# Mathematische Formeln – Segmented Spacetime (SSZ)

**Vollständige mathematische Formulierung mit Herleitungen**

© Carmen Wrede & Lino Casu, 2025

Lizenz: Anti-Capitalist Software License v1.4

**🌐 Languages:** [🇬🇧 English](MATHEMATICAL_FORMULAS.md) | [🇩🇪 Deutsch](MATHEMATICAL_FORMULAS_DE.md)

---

## 📋 Inhalt

1. [Fundamentale Konstanten](#1-fundamentale-konstanten)
2. [Segment-Radius](#2-segment-radius-rphi)
3. [Metrischer Tensor](#3-metrischer-tensor)
4. [PPN-Parameter](#4-ppn-parameter)
5. [Dual-Geschwindigkeiten](#5-dual-geschwindigkeiten)
6. [Redshift-Formeln](#6-redshift-formeln)
7. [Energie-Bedingungen](#7-energie-bedingungen)
8. [Schwarze Löcher](#8-schwarze-löcher)
9. [Numerische Methoden](#9-numerische-methoden)
10. [Statistische Tests](#10-statistische-tests)

---

## 1. Fundamentale Konstanten

### Physikalische Konstanten

```
G = 6.67430 × 10^(-11) m³ kg^(-1) s^(-2)    Gravitationskonstante
c = 2.99792458 × 10^8 m/s                    Lichtgeschwindigkeit  
ℏ = 1.054571817 × 10^(-34) J·s              Reduzierte Planck-Konstante
k_B = 1.380649 × 10^(-23) J/K               Boltzmann-Konstante
M_☉ = 1.98847 × 10^30 kg                    Sonnenmasse
```

### Der Goldene Schnitt φ

**Definition:**
```
φ = (1 + √5)/2 ≈ 1.618033988749894...
```

**Fundamentale Eigenschaft:**
```
φ² = φ + 1
```

**Weitere Relationen:**
```
1/φ = φ - 1 ≈ 0.618...
φ^n = F_n·φ + F_(n-1)    (Fibonacci-Zahlen)
```

**Warum φ?**
- Selbstähnliche Raumzeit-Struktur
- Optimale Segment-Packung
- Algebraisch einfach (√5)
- Natürliche Zeitbasis

---

## 2. Segment-Radius r_φ

### 2.1 Hauptformel

**SSZ-Charakteristischer Radius:**
```
r_φ(M) = φ · (GM/c²) · (1 + Δ(M)/100)
```

**Vergleich Schwarzschild:**
```
r_s(M) = 2 · (GM/c²)
```

**Verhältnis:**
```
r_φ/r_s = (φ/2) · (1 + Δ(M)/100)
        ≈ 0.809 · (1 + Δ/100)
```

**Bedeutung:**
- r_φ: Charakteristische Längenskala der Masse M
- φ statt 2: Fundamentale SSZ-Struktur
- Δ(M): Massenabhängige Korrektion

### 2.2 Δ(M)-Modell

**Formel:**
```
Δ(M) = A · exp(-α·r_s(M)) + B
```

**Gefittete Parameter:**
```
A = 98.01
α = 2.7177 × 10^4 m^(-1) 
B = 1.96
```

**Wobei:**
```
r_s(M) = 2GM/c²   (Schwarzschild-Radius)
```

**Grenzfälle:**

**Kleine Massen (r_s → 0):**
```
exp(-α·r_s) → 1
Δ(M) → A + B ≈ 100%
r_φ ≈ φ·(GM/c²)·2 ≈ 1.62·r_s  (nahe GR!)
```

**Große Massen (r_s >> 1/α):**
```
exp(-α·r_s) → 0  
Δ(M) → B ≈ 2%
r_φ ≈ φ·(GM/c²)·1.02 ≈ 0.83·r_s  (SSZ-Effekte)
```

---

## 3. Metrischer Tensor

### 3.1 SSZ-Metrik (Sphärisch)

**Linienelement:**
```
ds² = -A(r)dt² + B(r)dr² + r²(dθ² + sin²θ dφ²)
```

**Metrische Koeffizienten:**
```
A(r) = 1 - 2U + 2U² + ε₃U³ + O(U⁴)
B(r) = 1/A(r)
```

**Wobei:**
```
U = GM/(c²r) = r_s/(2r)  (Schwach-Feld-Parameter)
ε₃ = -24/5               (Kubischer Koeffizient)
```

### 3.2 Herleitung A(r)

**Ansatz:**
```
A(r) = f(U) mit U → 0 für r → ∞
```

**Taylor-Entwicklung:**
```
f(U) = f(0) + f'(0)·U + f''(0)/2·U² + f'''(0)/6·U³ + ...
```

**Randbedingungen:**
1. f(0) = 1              (flach im Unendlichen)
2. f'(0) = -2            (Newton-Limit)
3. f''(0) = 4            (φ-Korrektur)
4. f'''(0) = -24/5·6     (Eindeutigkeit)

**Ergebnis:**
```
A(U) = 1 - 2U + 2U² - 24/5·U³ + ...
```

---

## 4. PPN-Parameter

### 4.1 Post-Newtonian-Formalismus

**Standard PPN-Metrik:**
```
A(r) = 1 - 2GM/(c²r) + 2β(GM/(c²r))²
B(r) = 1 + 2γ·GM/(c²r)
```

**GR-Werte:**
```
β_GR = 1
γ_GR = 1
```

### 4.2 SSZ-Extraktion

**SSZ-Metrik:**
```
A(r) = 1 - 2U + 2U² + ...
B(r) = 1 + 2U + ...
```

**Vergleich:**
```
β_SSZ = 1.0
γ_SSZ = 1.0
```

**Bedeutung:**
- **SSZ = GR im Post-Newtonian-Limit!**
- Perihel-Präzession: ✓
- Lichtablenkung: ✓
- Shapiro-Verzögerung: ✓

---

## 5. Dual-Geschwindigkeiten

### 5.1 Fundamentale Invariante

**Theorem:**
```
v_esc(r) · v_fall(r) = c²
```

**Beweis:**

**Definition v_esc:**
```
v_esc = √(2GM/r)
```

**Definition v_fall (dual):**
```
v_fall = c²/v_esc
```

**Produkt:**
```
v_esc · v_fall = v_esc · (c²/v_esc) = c²  ∎
```

### 5.2 Lorentz-Faktoren

**GR-Zeitdilatation:**
```
γ_GR(r) = 1/√(1 - r_s/r)
        = 1/√(1 - 2GM/(c²r))
```

**Dualer Lorentz-Faktor:**
```
γ_dual(v) = 1/√(1 - (c/v)²)
```

**Konsistenz:**
```
γ_dual(v_fall) = γ_GR(r)  [exakt!]
```

---

## 6. Redshift-Formeln

### 6.1 Gravitativer Redshift (GR)

**Formel:**
```
z_GR = 1/√(1 - r_s/r) - 1
```

**Herleitung:**
```
dt_∞/dt_r = 1/√(g_tt) = 1/√(A(r))

Für A(r) = 1 - r_s/r:
z_GR = dt_∞/dt_r - 1
     = 1/√(1 - r_s/r) - 1
```

### 6.2 Kombinierter Redshift

**GR+SR:**
```
z_total = (1 + z_GR)(1 + z_SR) - 1
```

**SSZ-Modifikation:**
```
z_SSZ = (1 + z_GR,scaled)(1 + z_SR) - 1
```

**Wobei:**
```
z_GR,scaled = z_GR · (1 + Δ(M)/100)
```

---

## 7. Energie-Bedingungen

### 7.1 Energie-Impuls-Tensor

**Perfektes Fluid:**
```
T_μν = (ρ + p)u_μu_ν + p·g_μν
```

### 7.2 Hauptbedingungen

**Weak Energy Condition (WEC):**
```
ρ ≥ 0
ρ + p ≥ 0
```

**Dominant Energy Condition (DEC):**
```
ρ ≥ |p|
```

**Strong Energy Condition (SEC):**
```
ρ + 3p ≥ 0
ρ + p ≥ 0
```

### 7.3 SSZ-Erfüllung

**Test-Ergebnisse:**
- **WEC:** ✓ für r ≥ 5r_s
- **DEC:** ✓ für r ≥ 5r_s
- **SEC:** ✓ für r ≥ 5r_s

---

## 8. Schwarze Löcher

### 8.1 Horizont-Struktur

**Event Horizon:**
```
A(r_H) = 0
r_H ≈ r_s = 2GM/c²
```

**Photonen-Sphäre:**
```
r_ph = 3GM/c² · (1 - ε_φ)
ε_φ ≈ 0.05  (φ-Korrektur)
```

**ISCO:**
```
r_ISCO = 6GM/c² · (1 - δ_φ)
δ_φ ≈ 0.07
```

### 8.2 Schwarzschild-Schatten

**Kritischer Stoßparameter:**
```
b_crit² = r_ph² / A(r_ph)
```

**SSZ vs GR:**
```
b_SSZ ≈ 0.94 · b_GR
Unterschied: ~6%
```

---

## 9. Numerische Methoden

### 9.1 Masse-Inversion

**Problem:** Gegeben r_φ, finde M

**Newton-Verfahren:**
```
f(M) = r_φ(M) - r_obs
M_new = M_old - f(M_old)/f'(M_old)
```

**Ableitung:**
```
f'(M) = ∂r_φ/∂M
      = φ·G/c² · [1 + Δ(M)/100 + M·Δ'(M)/100]
```

**Konvergenz:**
- Typ: Quadratisch
- Iterationen: ~10...20
- Toleranz: 10⁻¹²⁰ (Decimal)

### 9.2 Precision-Handling

**Decimal-Arithmetik:**
```python
from decimal import Decimal, getcontext
getcontext().prec = 200  # 200 Stellen
```

**Warum?**
- Exponentielle Terme: exp(-α·r_s)
- Große Massenunterschiede: 10⁻³¹...10⁴⁰ kg
- Residuen-Minimierung

---

## 10. Statistische Tests

### 10.1 Paired Sign Test

**Hypothese:**
```
H₀: Median(z_SSZ - z_GR×SR) = 0
H₁: Median(z_SSZ - z_GR×SR) ≠ 0
```

**Test-Statistik:**
```
S = Anzahl(z_SSZ < z_GR×SR)
p = P(S | Binomial(N, 0.5))
```

**Ergebnis:**
```
S = 82/127 Objekte
p ≈ 0.0013  (signifikant!)
```

### 10.2 Bootstrap-Konfidenzintervalle

**Algorithmus:**
```
1. Resample N Datenpunkte (mit Zurücklegen)
2. Berechne Median
3. Wiederhole 10,000× 
4. Sortiere → Perzentile = CI
```

**95% CI:**
```
[Median - 1.96·SE, Median + 1.96·SE]
```

**Ergebnis:**
```
Median|Δz| = 0.00927
95% CI: [0.0081, 0.0104]
```

---

## 📚 Weiterführende Literatur

**Für Herleitungen:**
- [PHYSICS_FOUNDATIONS.md](PHYSICS_FOUNDATIONS.md) - Physikalische Interpretation
- [CODE_IMPLEMENTATION_GUIDE.md](CODE_IMPLEMENTATION_GUIDE.md) - Numerische Umsetzung

**Theorie-Papers:**
- `papers/SegmentedSpacetime-ANewPerspectiveonLightGravityandBlackHoles.md`
- `papers/DualVelocitiesinSegmentedSpacetime.md`

---

**Vollständige mathematische Formulierung der SSZ-Theorie! 📐**
