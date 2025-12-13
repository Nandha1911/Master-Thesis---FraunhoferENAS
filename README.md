# Comparison and Evaluation of Algorithms and Models of Non-Linear Damage Development  
## Reliability Assessment of Electronic Components

---


### Overview
This repository documents the work carried out for an **external Master’s thesis completed at Fraunhofer-Institut für Elektronische Nanosysteme ENAS, Chemnitz**.  
The study focuses on the **comparison and evaluation of linear and non-linear damage accumulation models** for the reliability assessment of power electronic components, with particular emphasis on **delamination in the SAC (Sn-Ag-Cu) die attach layer** under thermal cycling.

Finite Element simulations are performed using **Abaqus**, and the numerical results are combined with analytical damage models to predict damage progression without relying solely on experimental testing.

---

### Objectives
- Model and simulate a power electronic component subjected to thermal cycling
- Evaluate damage evolution in the die attach layer
- Compare linear and non-linear damage accumulation models
- Correlate simulation-based damage predictions with experimental observations
- Reduce experimental effort through validated numerical prediction methods

---

### Experimental Background
- **Material:** SAC (Sn-Ag-Cu) solder used as die attach material
- **Damage Evaluation Methods:**
  - Scanning Acoustic Microscopy (SAM)
  - Pulsed Infrared Thermography (PIRT)
- **Loading Condition:** Passive thermal cycling
- Experimental data provide reference values for delamination percentage over increasing thermal cycles

---

### Numerical Modeling (Abaqus)
- 3D finite element model of the electronic component
- Local mesh refinement in critical regions (corners, interfaces)
- Mesh convergence study to ensure numerical accuracy
- Thermo-mechanical boundary conditions with symmetry constraints
- Creep-dominated material behavior in the die attach layer

**Key Output Variable:**
- **CEEQ (Equivalent Creep Strain)** – identified as the most suitable damage indicator

---

### Damage Modeling Approach
- Extraction of strain increments (Δε) from Abaqus results
- Application of the **Coffin–Manson equation** to estimate cycles to failure
- Implementation of:
  - Linear damage accumulation models
  - Non-linear damage accumulation models
- Iterative simulation strategy:
  - Identification of damaged elements
  - Deactivation of failed elements
  - Restart and continuation of simulations for progressive damage evolution

---

### Programming and Automation
- Implemented in **Python (object-oriented design)**
- Abstract base class for damage models
- Modular and extensible architecture
- Automated post-processing and lifetime prediction
- Seamless integration with Abaqus simulation results

---

### Key Results
- Successful prediction of delamination growth over multiple thermal cycles
- Non-linear damage models show improved agreement with experimental data
- **HRSu damage model** demonstrated the highest accuracy
- Improved reliability assessment and lifetime prediction capability

---

### Tools and Software
- **Abaqus**
- **Python 3.x**
- **Git**

---

### Scope and Usage
This repository is intended for:
- Academic research
- Reliability assessment studies
- Methodological extension to other electronic packaging problems
