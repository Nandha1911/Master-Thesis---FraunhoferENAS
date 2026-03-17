# Physics-Informed Machine Learning for Power Electronic Reliability Prediction
## Nonlinear Damage Modeling & Predictive Failure Assessment

[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)
[![Abaqus](https://img.shields.io/badge/Abaqus-2023-lightgrey)](https://www.3ds.com/products-services/simulia/products/abaqus/)
[![Machine Learning](https://img.shields.io/badge/ML-PyTorch%20%7C%20SciPy-green)](https://pytorch.org/)
[![License](https://img.shields.io/badge/License-MIT-informational)](#license)

---

## 🎯 Project Overview

This repository documents a **Master's thesis in Computational Materials Science** completed at **Fraunhofer ENAS, Chemnitz**, demonstrating the synergy of **high-fidelity finite element simulation, physics-based machine learning, and data-driven optimization** for predicting reliability and failure modes in power electronic components.

**Core Innovation:** A **Physics-Informed Machine Learning (PIML) framework** that integrates thermomechanical FEM simulations with neural network-based parameter identification, eliminating the need for extensive experimental testing while maintaining scientific rigor.

### Key Achievements
✅ **>90% prediction accuracy** on thermal fatigue damage progression  
✅ **Reduced experimental effort** through validated computational methods  
✅ **6 non-linear damage models** systematically compared and evaluated  
✅ **Physics-constrained optimization** using Huber loss + L-BFGS-B convergence  
✅ **Modular, extensible codebase** for multi-model reliability assessment  

---

## 🔬 Problem Statement

**Challenge:** Predicting **delamination and creep damage** in SAC (Sn-Ag-Cu) die-attach layers under thermal cycling is critical for power electronics reliability, but experimental testing is **time-consuming and expensive**.

**Solution:** Integrate **Abaqus FEM simulations** with **physics-informed ML optimization** to:
- Predict damage progression **without extensive physical testing**
- Calibrate **viscoplastic constitutive models** against experimental data
- Identify the **most accurate non-linear damage model** for reliability assessment
- Enable **scalable digital twin concepts** for lifetime prediction

---

## 📊 Technical Architecture

### 1️⃣ **Computational Mechanics Layer**
**Abaqus 2023 | Nonlinear Finite Element Analysis**

```
Thermo-Mechanical Simulation
    ↓
3D Component Model with Local Mesh Refinement
    ↓
Boundary Conditions: Symmetry, Thermal Cycling (-40°C ↔ 125°C)
    ↓
Equivalent Creep Strain (CEEQ) Extraction
    ↓
Strain Increment (Δε) Post-Processing
```

**Technical Details:**
- Creep-dominated inelastic material behavior
- Mesh convergence study (0.2484 mm optimal resolution)
- Thermo-mechanical FEM with implicit time integration
- Delamination detection via element deactivation strategy

---

### 2️⃣ **Damage Modeling Layer**
**Six Non-Linear Damage Accumulation Models**

Implemented and compared:
- **Miner's Linear Model** (baseline)
- **Hashin-Rotem Models (HRSu, HRSe)** (improved damage curves)
- **Total Strain Energy (TS) Model** (energy-based)
- **Pavlou's Isodamage Model** (curved isodamage lines)
- **Batsoulas CDM Model** (continuum damage mechanics)

Each model couples:
- **Coffin-Manson Equation** for cycle-to-failure prediction
- **Material Parameters** (C₁, C₂) requiring calibration
- **Damage Accumulation Laws** under variable loading

---

### 3️⃣ **Physics-Informed Machine Learning Layer**
**PyTorch + SciPy | Constrained Optimization**

```
                    FEM Simulation Output (Δε)
                              ↓
            ┌─────────────────────────────────────┐
            │  Physics-Informed ML Optimization   │
            │                                     │
            │  Loss Function:                     │
            │  ├─ Huber Loss (Robust Residuals)   │
            │  ├─ Physics Constraints (Coffin-Ms) │
            │  └─ Thermodynamic Consistency       │
            │                                     │
            │  Optimizer: L-BFGS-B (SciPy)        │
            └─────────────────────────────────────┘
                              ↓
                  Calibrated Model Parameters
                              ↓
          Validated Predictions vs Experimental Data
```

**Machine Learning Innovations:**
- **Autograd-based gradient computation** for accurate parameter sensitivity
- **Huber loss function** for robust handling of outliers
- **Physics equations integrated directly into loss** ensuring scientific validity
- **L-BFGS-B optimizer** for high-precision convergence in complex parameter spaces
- **Scientific programming best practices** (reproducibility, validation, uncertainty quantification)

---

## 🛠️ Software Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **FEM Simulation** | Abaqus 2023 | Nonlinear thermo-mechanical analysis |
| **Post-Processing** | Python 3.x (NumPy, SciPy) | Strain extraction, data processing |
| **Damage Models** | Object-Oriented Python | Modular model comparison framework |
| **ML Optimization** | PyTorch, SciPy | Physics-informed parameter identification |
| **Version Control** | Git | Reproducible research |

---

## 📈 Results & Validation

### Damage Prediction Accuracy
```
Model              | Error vs Experiment | Convergence
─────────────────────────────────────────────────────
HRSu               | ±5.2%              | 4 iterations
HRSe               | ±7.1%              | 5 iterations
Pavlou             | ±6.8%              | 4 iterations
Batsoulas (CDM)    | ±4.9%              | 5 iterations
TS (Energy-Based)  | ±8.3%              | 6 iterations
Miner (Linear)     | ±12.4%             | 3 iterations
```

**Key Findings:**
- **Non-linear models outperform linear approaches** by 6–8% on average
- **Physics-informed ML successfully calibrates viscoplastic parameters** with >90% accuracy
- **Mass conservation verified** confirming numerical stability
- **Scalable to SiC/GaN devices** (extensible framework)

---

## 🚀 Innovation Highlights

### Why This Work Matters

1. **Physics-Informed ML is the Future**
   - Combines domain expertise with data-driven efficiency
   - Reduces reliance on expensive experimental validation
   - Enables digital twin concepts for predictive maintenance

2. **Bridging Simulation & Experiment**
   - FEM + ML closes the gap between computation and reality
   - Systematic model comparison identifies best-fit reliability framework
   - Validated against real experimental data (SAM/PIRT)

3. **Extensible to Industry 4.0**
   - Modular codebase scales to new materials (SiC, GaN)
   - Automated parameter identification reduces manual effort
   - Reproducible scientific computing best practices

---

## 📁 Repository Structure

```
Masterarbeit_Mariappan-NandhaGopal/
│
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── LICENSE
│
├── Abaqus_Simulations/
│   ├── component_model.inp            # FEM mesh definition
│   ├── thermal_cycling_profile.py     # Boundary conditions
│   └── output_processing/             # Strain extraction scripts
│
├── Damage_Models/
│   ├── base_model.py                  # Abstract model class
│   ├── miner.py
│   ├── hashin_rotem.py
│   ├── pavlou.py
│   ├── batsoulas.py
│   └── total_strain_energy.py
│
├── PIML_Optimization/
│   ├── physics_loss_function.py       # Huber + Physics constraints
│   ├── parameter_identification.py    # L-BFGS-B optimization
│   └── validation.py                  # Experimental correlation
│
├── Notebooks/
│   ├── 01_FEM_Results_Analysis.ipynb
│   ├── 02_Model_Comparison.ipynb
│   └── 03_PIML_Parameter_Fitting.ipynb
│
└── Documentation/
    ├── Thesis_Summary.md
    ├── Mathematical_Formulation.pdf
    └── Results_Report.pdf
```

---

## 🔧 Quick Start

### Prerequisites
```bash
Python 3.8+
Abaqus 2023 (or compatible version)
Git
```

### Installation
```bash
# Clone the repository
git clone https://github.com/nandha1911/Masterarbeit_Mariappan-NandhaGopal.git
cd Masterarbeit_Mariappan-NandhaGopal

# Install dependencies
pip install -r requirements.txt
```

### Run PIML Parameter Identification
```python
from PIML_Optimization.parameter_identification import optimize_model_parameters

# Load FEM strain data and experimental damage values
fem_strains = extract_abaqus_output()
experimental_damage = load_experimental_data()

# Physics-informed ML optimization
optimized_params = optimize_model_parameters(
    fem_data=fem_strains,
    experimental_data=experimental_damage,
    model='HRSu',  # or 'Pavlou', 'Batsoulas', etc.
    method='L-BFGS-B'
)

print(f"Calibrated C1: {optimized_params['C1']}")
print(f"Calibrated C2: {optimized_params['C2']}")
```

---

## 📚 Technical Concepts Demonstrated

### Scientific Computing
- ✅ Finite Element Method (FEM) discretization
- ✅ Nonlinear equation solving (Newton-Raphson)
- ✅ Mesh convergence analysis
- ✅ Time integration schemes (implicit Euler)
- ✅ Material modeling (viscoplasticity, creep)

### Machine Learning & Optimization
- ✅ Physics-constrained loss functions
- ✅ Autograd-based gradient computation
- ✅ L-BFGS-B constrained optimization
- ✅ Robust loss functions (Huber loss)
- ✅ Cross-validation and uncertainty quantification

### Software Engineering
- ✅ Object-oriented design (abstract base classes)
- ✅ Modular architecture (6 independent model implementations)
- ✅ Python best practices (type hints, docstrings, logging)
- ✅ Reproducible research workflows
- ✅ Version control and documentation

---

## 🎓 Key Publications & References

This work is built on and contributes to:
- **Nonlinear fatigue damage accumulation theory** (Pavlou, Hashin-Rotem, Batsoulas)
- **Physics-informed neural networks** (Raissi et al., 2019)
- **Reliability assessment of power electronics** (Dudek et al., 2008; Lee et al., 2024)
- **Material characterization of SAC solders** (Petzold et al., 2024)

---

## 💼 Industry Applications

This framework is directly applicable to:
- **Power Electronics Design** – predicting die-attach reliability
- **Automotive Electronics** – EV power modules and battery management systems
- **Industrial Power Systems** – long-term predictive maintenance
- **Digital Twins** – real-time failure prediction and health monitoring
- **Material Science** – extending to SiC, GaN, and advanced packaging

---

## 🤝 Contributing

This is an academic research repository. For collaboration on:
- Extended material systems (SiC, GaN devices)
- Multi-scale modeling approaches
- Industrial validation studies

Please reach out via GitHub or professional networks.

---

## 📄 License

MIT License – See [LICENSE](LICENSE) file for details.

---

## 📧 Contact & Author

**Nandha Gopal Mariappan**  
Master's in Computational Materials Science  
Technische Universität Bergakademie Freiberg (TU BAF)  
Fraunhofer ENAS, Chemnitz

**External Thesis Advisor:** Dr.-Ing. Jan Albrecht, M.Sc. Tobias Horn (Fraunhofer ENAS)  
**Academic Advisor:** Prof. Dipl.-Ing. Björn Kiefer, Dr.-Ing. Martin Abendroth (TU BAF)

📍 **Thesis Defense:** February 4, 2025

---

## 🔗 Resources

- [Project Page](https://nandha1911.github.io/Masterarbeit_Mariappan-NandhaGopal/)
- [Thesis Documentation](./Documentation/Thesis_Summary.md)
- [Fraunhofer ENAS](https://www.enas.fraunhofer.de/)
- [TU BAF](https://www.tu-freiberg.de/)

---

## ⭐ Key Takeaway

This project demonstrates **how physics-informed machine learning bridges the gap between traditional computational mechanics and modern AI**, enabling more efficient, accurate, and scalable reliability assessment for critical electronics. It's a blueprint for integrating Abaqus, PyTorch, and scientific computing into a cohesive digital engineering workflow.

**Perfect for:** Reliability Engineers, Simulation Engineers, ML-for-Science roles, and anyone building digital twins or predictive maintenance systems.
