# physical-design-homework2-macro-placement

![GitHub repo size](https://img.shields.io/github/repo-size/ysnanako/physical-design-homework2-macro-placement)
![GitHub last commit](https://img.shields.io/github/last-commit/ysnanako/physical-design-homework2-macro-placement)

This project is part of the **National Cheng Kung University (NCKU) - VLSI/CAD Group** course **"Physical Design for Nanometer IC"**, focusing on **macro placement using Corner Stitching (CS) and Genetic Algorithm (GA)**.

## 📖 Table of Contents

- [Project Overview](#project-overview)
- [Input Format](#input-format)
- [Output Format](#output-format)
- [Project Structure](#project-structure)
- [Parsing & Placement Flow](#parsing--placement-flow)
- [Example Execution](#example-execution)
- [Generated Plots](#generated-plots)
- [Validation & HPWL Calculation](#validation--hpwl-calculation)
- [Contribution Guide](#contribution-guide)
- [Contact Information](#contact-information)

## 📝 Project Overview

This project implements **macro placement** using **Corner Stitching (CS) as the packing-based foundation** while utilizing **Genetic Algorithm (GA) to perturb insertion order**. The goal is to **Half-Perimeter Wire Length (HPWL)** while ensuring legal placement.

### **Key Features:**
1. **Parsing Bookshelf format `.aux` files** and extracting circuit information.
2. **Using Corner Stitching (CS) for efficient whitespace management and placement legality checking.**
3. **Applying Genetic Algorithm (GA) to optimize macro insertion order into CS structure.**
4. **Generating `.pl_out` placement results and `.plt` for visualization.**
5. **Checking legality and calculating HPWL** using `tester.py`. 

## 📄 Input Format

This project follows the **Bookshelf** format and requires the following files:
- **`.aux`** - Main index file pointing to `.nodes`, `.nets`, `.pl`, `.scl`, etc.
- **`.nodes`** - Describes circuit components and their dimensions.
- **`.nets`** - Defines netlist connectivity.
- **`.pl`** - Specifies the placement coordinates.
- **`.scl`** - Defines row placement structure.

📄 **Example `.aux` File**
```
RowBasedPlacement : circuit.nodes circuit.nets circuit.pl circuit.scl
```

## 📄 Output Format
After execution, the program generates **macro placement results**:
- **`.pl_out`** - Output placement file for macros.
- **`.dat` files** - Stores parsed circuit information.
- **`.plt` files** - Gnuplot scripts for visualization.

## 🧰 Project Structure

```
📂 physical-design-homework3-abacus/
│── 📂 src/ # (main.cpp, parser.cpp, abacus.cpp, and headers)
│── 📂 obj/ # (ignored)
│── 📂 plt/ # (ignored in Git, automatically generated)
│── 📂 dat/ # (ignored in Git due to large size, automatically generated)
│── 🖥️ HW2_StudentID # (ignored)
│── 🔧 Makefile
│── 📜 README.md # This file
│── 📜 .gitignore

../📂 benchmarks/ # (located outside the repo)
```

## 🔹 **Parsing & Placement Flow**
This project implements **macro placement** using **Corner Stitching (CS) as the packing-based foundation** while utilizing **Genetic Algorithm (GA) to perturb insertion order**. The workflow is as follows:

### **1. Parsing Bookshelf Format**
- The program first reads the **`.aux`** file, which references the **`.nodes`, `.nets`, `.pl`, `.scl`** files.

### **2. Corner Stitching as Packing-based Foundation**
- **Corner Stitching (CS)** is used as the core **data structure for macro packing**.
- Macros are inserted into empty regions using **CS rules**, ensuring:
  - **No overlaps** between macros.
  - **Efficient whitespace handling**.
  - **Alignment to legal placement sites**.

### **3. Genetic Algorithm for Macro Placement Perturbation**
- The **Genetic Algorithm (GA)** determines the **insertion order of macros** within the **Corner Stitching structure**.
- The GA process follows these steps:
  1. **Initialize Population** - Generate initial macro insertion orders.
  2. **Selection** - Choose the best insertion orders based on **short wirelength**.
  3. **Crossover & Mutation** - Swap macro insertion orders and introduce **small perturbations**.
  4. **Evaluation** - Each new solution is scored based on the resulting **short wirelength** after insertion.
  5. **Iteration** - The process continues until convergence.

### **4. Output Generation**
- The final macro placement is stored in **`.pl_out`**.
- Visualization data is exported as **`.plt`** and **`.dat`** files for `gnuplot`.

### **5. Validation & HPWL Calculation**
- The legality of the placement is checked using **`tester.py`**.
- **HPWL** is computed to evaluate placement quality.

## ⚡ **Example Execution**

```bash
./HW2_StudentID ../benchmarks/adaptec1/adaptec1.aux
```

```bash
gnuplot adaptec1/adaptec1.plt
```

```bash
python3 tester.py --case adaptec1
```

## 🖼️ Generated Plots

Below are the generated plots from the `matlab` and `gnuplot` output:

**adaptec1 pre-placed (matlab)**  
![fixed](https://github.com/user-attachments/assets/a251b908-bfb2-4dae-b5aa-8cb14aca7e85)  
**adaptec1 result (matlab)**  
![GA4](https://github.com/user-attachments/assets/34f0f459-003d-41fd-adc2-b7fe0d21ff26)  
**adaptec1 result (gnuplt)**  
![GA3](https://github.com/user-attachments/assets/356a0f04-9937-4e2f-b2de-4e30a069d21a)  

## ✅ Validation & HPWL Calculation

### **Legality Check & HPWL Calculation**

- Ensures **macros do not overlap**.
- Computes total wirelength to evaluate placement quality.

```bash
python3 tester.py --case adaptec1
len node_info 543
adjust net size = 693
node_net_num_max 81
node_area_max = 3444336
Macro HPWL: 1051995.0
```

If the placement has overlaps or violates any constraints, the script will report errors.

## 🤝 Contribution Guide

1. Fork this repository.
2. Create a new branch (`git checkout -b feature-xyz`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push to the remote branch (`git push origin feature-xyz`).
5. Submit a Pull Request.

## 📬 Contact Information

- 📧 Email: [m16131056@gs.ncku.edu.tw](mailto\:m16131056@gs.ncku.edu.tw)
- 🌎 University: [National Cheng Kung University (NCKU)](https://www.ncku.edu.tw)
- 📖 Course: Physical Design for Nanometer IC, Fall 2024
