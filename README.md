# Emblica officinalis Network Pharmacology

This repository contains a Python-based automated network pharmacology pipeline and transcriptomics analysis for exploring the therapeutic potential of *Emblica officinalis* (Amla).

## 📌 Project Highlights

- Automated data collection from PubChem, BindingDB, BioGRID, NCBI Gene, DisGeNET
- Cytoscape network generation for compound-target-disease relationships
- Transcriptome assembly and annotation using Trinity and BLAST
- Pathway enrichment analysis with KAAS

## 🧪 Tools Used

- Python (RDKit, Pandas, Py4Cytoscape)
- Flask (for web interface)
- Cytoscape
- Trinity, BLASTx, TransDecoder, KAAS

## 📁 Repository Structure

- `pipeline/` – Python scripts and Flask web interface
- `data/` – Input SDF files and disease lists
- `results/` – Output networks and interaction files
- `transcriptomics/` – Transcriptome assembly and annotation results

## 🧬 How to Run

1. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

2. Start the Flask app:
    ```bash
    python pipeline/app.py
    ```

3. Upload your multi-compound `.sdf` file and disease list through the web interface.

4. Download the output ZIP containing:
    - Cytoscape `.cys` file
    - PNG image of the network
    - CSV with interactions

## 📜 License

This project is licensed under the MIT License.
