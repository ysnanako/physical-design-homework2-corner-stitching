# physical-design-homework2-corner-stitching

![GitHub repo size](https://img.shields.io/github/repo-size/ysnanako/physical-design-homework2-corner-stitching)
![GitHub last commit](https://img.shields.io/github/last-commit/ysnanako/physical-design-homework2-corner-stitching)

This project is part of the **National Cheng Kung University (NCKU) - VLSI/CAD Group** course **"Physical Design for Nanometer IC"**, focusing on **macro placement using Corner Stitching and Genetic Algorithm (GA)**.

## 📖 Table of Contents

- [Project Overview](#project-overview)
- [Input Format](#input-format)
- [Output Format](#output-format)
- [Project Structure](#project-structure)
- [Parsing & Placement Flow](#parsing--placement-flow)
- [Example Execution](#example-execution)
- [Validation & HPWL Calculation](#validation--hpwl-calculation)
- [Contribution Guide](#contribution-guide)
- [Contact Information](#contact-information)

## 📝 Project Overview

This project implements **macro placement** using **Corner Stitching (CS) as the packing-based foundation** while utilizing **Genetic Algorithm (GA) to perturb insertion order**. The goal is to **minimize Short Wire Length (SWL) and Half-Perimeter Wire Length (HPWL)** while ensuring legal placement.

### **Key Features:**
1. **Parsing Bookshelf format `.aux` files** and extracting circuit information.
2. **Using Corner Stitching (CS) for efficient whitespace management and placement legality checking.**
3. **Applying Genetic Algorithm (GA) to optimize macro insertion order into CS structure.**
4. **Generating `.pl_out` placement results and `.pl_out` for visualization.**
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

../📂 benchmarks/ # Directory containing Bookshelf benchmark test cases (located outside the repo)
```

## 🔹 **Parsing & Placement Flow**
This project implements **macro placement** using **Corner Stitching (CS) as the packing-based foundation** while utilizing **Genetic Algorithm (GA) to perturb insertion order**. The workflow is as follows:

### **1. Parsing Bookshelf Format**
- The program first reads the **`.aux`** file, which references the **`.nodes`, `.nets`, `.pl`, `.scl`** files.
- The **`.nodes`** file provides information about **macros and standard cells**.
- The **`.nets`** file describes net connections between cells.
- The **`.pl`** file provides initial placement data.
- The **`.scl`** file contains row structure information for standard cell placement.

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
- The legalized placement result is stored in **`.legal.pl`**.
- Visualization data is exported as **`.plt`** files for `gnuplot`.

### **5. Validation & HPWL Calculation**
- The legality of the placement is checked using **`tester.py`**.
- **HPWL and short wirelength** are computed to evaluate placement quality.
- If the result is not optimal, **GA parameters should be adjusted and re-run**.

## ⚡ **Example Execution**

```bash
./HW2_StudentID ../benchmarks/adaptec1/adaptec1.aux
```

```bash
gnuplot adaptec1/adaptec1.plt
```

## 🖼️ Generated Plots

Below are the generated plots from the `gnuplot` output:

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

# physical-design-homework2-corner-stitching

This project is part of the **National Cheng Kung University (NCKU) - VLSI/CAD Group** course **"Physical Design for Nanometer IC"**, focusing on **macro placement using Corner Stitching and Genetic Algorithm (GA)**.

## 📖 Table of Contents
- [Project Overview](#project-overview)
- [Requirements](#requirements)
- [Installation & Execution](#installation--execution)
- [Input Format](#input-format)
- [Output Format](#output-format)
- [Project Structure](#project-structure)
- [Parsing & Placement Flow](#parsing--placement-flow)
- [Example Execution](#example-execution)
- [Validation & SWL & HPWL Calculation](#validation--swl--hpwl-calculation)
- [Contribution Guide](#contribution-guide)
- [Contact Information](#contact-information)

## 📝 Project Overview
This project implements **macro placement** using **Corner Stitching (CS) as the packing-based foundation** while utilizing **Genetic Algorithm (GA) to perturb insertion order**. The goal is to **minimize Short Wire Length (SWL) and Half-Perimeter Wire Length (HPWL)** while ensuring legal placement.

### **Key Features:**
1. **Parsing Bookshelf format `.aux` files** and extracting circuit information.
2. **Using Corner Stitching (CS) for efficient whitespace management and placement legality checking.**
3. **Applying Genetic Algorithm (GA) to optimize macro insertion order into CS structure.**
4. **Generating `.plout` placement results and validating with legality checks.**
5. **Calculating SWL & HPWL to assess placement quality.**

## 🖥️ Requirements
This project is developed on **Linux (Ubuntu 20.04+)** and requires:
- `g++ 6.3.0+`
- `make`
- `gnuplot`
- `python3`
- `iccad2013_check_legality` (legality checker)
- `iccad2013_get_hpwl` (HPWL calculation)

## 🚀 Installation & Execution
Follow these steps to install and run the project:

1. **Clone the Repository**
   ```bash
   git clone https://github.com/ysnanako/physical-design-homework2-corner-stitching.git
   cd physical-design-homework2-corner-stitching
   ```

2. **Compile the Code**
   ```bash
   make
   ```

3. **Run the Program**
   ```bash
   ./HW2_StudentID <circuit.aux>
   ```

4. **Check Legality & HPWL Calculation**
   ```bash
   ./iccad2013_check_legality superblue1.aux superblue1.legal.pl
   ./iccad2013_get_hpwl superblue1.aux superblue1.legal.pl
   ```

5. **Validate with SWL Checker**
   ```bash
   python3 tester.py --case superblue1
   ```

6. **Visualize the Output**
   ```bash
   gnuplot <circuit>/<circuit.plt>
   ```

## 📂 Input Format
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
- **`.plout`** - Output placement file for macros.
- **`.legal.pl`** - Legalized placement file.
- **`.plt`** - Gnuplot scripts for visualization.

## 🏗️ Project Structure
```
📂 physical-design-homework2-corner-stitching/
│── 📂 src/ # Source code directory (main.cpp, parser.cpp, datatype.cpp, and headers)
│── 📂 obj/ # Compiled object files (ignored in Git)
│── 📂 plt/ # Gnuplot scripts for visualization (ignored in Git, automatically generated)
│── 📂 dat/ # Stores generated placement data (ignored in Git due to large size)
│── 🚀 HW2_StudentID # Main executable file (ignored in Git)
│── 📜 .gitignore # Specifies files to ignore in version control
│── 📜 README.md # This file
│── 🏗️ Makefile # Defines build instructions for compiling the project

../📂 benchmarks/ # Directory containing Bookshelf benchmark test cases (located outside the repo)
```

## 🔹 **Parsing & Placement Flow**
1. **Corner Stitching (CS) as Packing-based Foundation**
   - CS is used for **macro placement and whitespace management**.
   - Ensures **no overlaps** and **efficient whitespace usage**.
2. **Genetic Algorithm (GA) for Macro Placement Optimization**
   - GA perturbs **macro insertion order** into CS structure.
   - Uses **Selection, Crossover, Mutation, and Evaluation** to optimize **Short Wire Length (SWL)**.
3. **Short Wire Length (SWL) Calculation**
   - SWL is computed **after placement** to measure connection efficiency.
4. **Output Generation**
   - `.plout` (Macro placement output).
   - `.legal.pl` (Legalized placement output).
   - `.plt` (Visualization scripts).
5. **Validation & HPWL Calculation**
   - Legality verified with `tester.py`.
   - **HPWL & Total Wirelength** computed for quality assessment.

## ✅ Validation & Wirelength & HPWL Calculation
To validate correctness, **legality and quality metrics** are computed using:

### **Legality & Wirelength Check**
```bash
python3 tester.py --case superblue1
python3 tester.py --case superblue5
python3 tester.py --case superblue19
```
- Ensures **macros do not overlap**.
- Computes total wirelength to evaluate placement quality..

### **HPWL Calculation**
```bash
./iccad2013_get_hpwl superblue1.aux superblue1.legal.pl
./iccad2013_get_hpwl superblue5.aux superblue5.legal.pl
./iccad2013_get_hpwl superblue19.aux superblue19.legal.pl
```
A **lower HPWL and SWL** indicate a **better placement solution**.

## 🤝 Contribution Guide
1. Fork this repository.
2. Create a new branch (`git checkout -b feature-xyz`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push to the remote branch (`git push origin feature-xyz`).
5. Submit a Pull Request.

## 📬 Contact Information
- 📧 Email: [m16131056@gs.ncku.edu.tw](mailto:m16131056@gs.ncku.edu.tw)
- 🌎 University: [National Cheng Kung University (NCKU)](https://www.ncku.edu.tw)
- 📖 Course: Physical Design for Nanometer IC, Fall 2024

