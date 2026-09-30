<<<<<<< HEAD
[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/tniubn-f)
# HW1-Markdown-Creation-and-Rendering-Practice-Template
=======
# 🐷 PigView: Edge-AI Pig Weight Estimation System

![Edge SoC](https://img.shields.io/badge/Edge_SoC-GPA7750A-blue?style=flat-square)
![Memory Constraint](https://img.shields.io/badge/Memory-64MB-red?style=flat-square)
![Core Model](https://img.shields.io/badge/Model-MobileNetV2_YOLOv3_Lite-green?style=flat-square)
![Methodology](https://img.shields.io/badge/Methodology-MBB_%2B_ROI-orange?style=flat-square)
![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen?style=flat-square)

## 1. Project Overview
This project is the technical specification and system architecture white paper for "PigView: Automated Pig Weight Estimation System". This system is deeply optimized for extremely resource-constrained edge computing devices (Edge SoC GPA7750A, with only 64MB RAM). In terms of architectural design, this project **completely abandons high-computational-overhead keypoint and skeleton recognition technologies**, and instead adopts **Minimum Bounding Box (MBB) area mapping** paired with **ROI physical spatial constraints**, achieving a commercially viable application that balances high precision with stable 15 FPS inference.

To maximize the readability and cross-platform compatibility of the technical documents, and to perfectly demonstrate the spirit of decoupling Markdown content from rendering, this project has established a **"Quad-Engine Rendering Pipeline"**. Through automated scripts, the native `content.md` is translated into four industry-standard formats: HTML, static website, PDF, and technical presentation slides.

## 2. Prerequisites
Please ensure the execution environment meets the following conditions to guarantee compatibility between the automated rendering pipeline and the Sandbox environment:
* **Operating System**: Linux or macOS is recommended (requires a Bash script execution environment).
* **Core Dependencies**:
  * `Node.js / npm` (v18+): Responsible for invoking npx to execute PDF and Marp presentation rendering.
  * `Python` (v3.8+): Responsible for building the MkDocs static documentation website.
  * `Quarto CLI`: Responsible for basic academic HTML rendering.

## 3. Installation
If executing in a clean Sandbox environment (e.g., bare-metal Ubuntu), please run the following commands in order to configure the complete build environment:

**A. Install underlying system dependencies (Node.js, npm, Python pip)**:
```bash
sudo apt-get update
sudo apt-get install -y nodejs npm python3-pip wget
```

**B. Install Quarto CLI**:
```bash
wget [https://github.com/quarto-dev/quarto-cli/releases/download/v1.4.551/quarto-1.4.551-linux-amd64.deb](https://github.com/quarto-dev/quarto-cli/releases/download/v1.4.551/quarto-1.4.551-linux-amd64.deb)
sudo dpkg -i quarto-1.4.551-linux-amd64.deb
```

**C. Install Python dependencies (MkDocs)**:
```bash
pip3 install -r requirements.txt
```

## 4. Build Pipeline
Please execute the following Bash automated script in the project root directory. This pipeline will safely initialize the `output/` directory, sequentially drive the four major rendering engines, and finally clean up temporary build files:

```bash
# Ensure the output directory exists (complies with CI basic standards)
mkdir -p output

# ---------------------------------------------------------
# Engine 1: Quarto Compilation (HTML interactive academic white paper)
# ---------------------------------------------------------
quarto render content.md --to html -M theme:flatly -M toc:true -M embed-resources:true
mv content.html output/Quarto_Report.html

# ---------------------------------------------------------
# Engine 2: Material for MkDocs Compilation (Dark mode static website)
# ---------------------------------------------------------
mkdir -p docs
cp content.md docs/index.md
cp -r assets docs/ 2>/dev/null || :
# 直接使用目錄下已存在的 mkdocs.yml 進行編譯 (不要寫 echo 去覆蓋它)
mkdocs build -d output/MkDocs_Site
rm -rf docs

# ---------------------------------------------------------
# Engine 3: md-to-pdf Compilation (High-precision print-grade PDF specification)
# ---------------------------------------------------------
npx md-to-pdf content.md
mv content.pdf output/Technical_Spec.pdf

# ---------------------------------------------------------
# Engine 4: Marp CLI Compilation (Technical presentation slides)
# ---------------------------------------------------------
npx @marp-team/marp-cli@latest content.md -o output/Presentation_Slides.html
```

## 5. Expected Outputs
After the pipeline execution is complete, the `output/` directory will precisely generate the following four publishing formats, comprehensively covering academic review and commercial presentation needs:
1. **`Quarto_Report.html`**: A single-file HTML report featuring a floating navigation bar and complete academic formatting.
2. **`MkDocs_Site/`**: A modern documentation website directory with powerful search capabilities and dark mode (please open the internal `index.html`).
3. **`Technical_Spec.pdf`**: A PDF document that retains all HTML centered formatting and mathematical formula parsing.
4. **`Presentation_Slides.html`**: A slide file that can be presented in full screen directly within a browser.

## 6. References
* [Quarto Official Documentation](https://quarto.org/)
* [Material for MkDocs Documentation](https://squidfunk.github.io/mkdocs-material/)
* [md-to-pdf (Node.js)](https://github.com/simonhaenisch/md-to-pdf)
* [Marp: Markdown Presentation Ecosystem](https://marp.app/)
>>>>>>> acb9985 (PigView documentation & 4 rendering tools)
