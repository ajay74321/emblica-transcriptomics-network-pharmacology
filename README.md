# emblica-transcriptomics-network-pharmacology

This repository contains a Python-based automated network pharmacology and transcriptomics pipeline 
for exploring the therapeutic potential of *Emblica officinalis* (Amla).

## 🌟 Project Highlights

- Automated data collection from PubChem, BindingDB, BioGRID, NCBI Gene, and DisGeNET
- Cytoscape-based network generation for compound-target-disease relationships
- Transcriptome assembly and annotation using Trinity and BLASTx
- Pathway enrichment analysis using the KAAS web server

## 🧰 Tools & Technologies

- **Python**: `pandas`, `rdkit`, `requests`, `py4cytoscape`, `igraph`, `os`
- **Web Framework**: Flask
- **Databases**: PubChem, BindingDB, BioGRID, NCBI Gene, DisGeNET
- **Network Visualization**: Cytoscape
- **Transcriptomics**: Trinity, TransDecoder, BLASTx, KAAS

## 📁 Repository Structure

```
emblica-therapeutic-pipeline/
│
├── README.md
├── LICENSE
├── .gitignore
│
├── data/
│   ├── phytochemicals/
│   ├── sdf_files/
│   └── diseases_list.txt
│
├── results/
│   ├── output.csv
│   ├── network.png
│   ├── network.cys
│   └── input.sdf│

```

## 🚀 Getting Started

1. Clone the repository:
    ```bash
    git clone https://github.com/yourusername/emblica-therapeutic-pipeline.git
    cd emblica-therapeutic-pipeline
    ```

2. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3. Run the Flask web app:
    ```bash
    python pipeline/app.py
    ```

4. Upload your SDF file and disease list via the web interface.

## 📦 Output

After execution, a ZIP file is auto-downloaded containing:
- `network.cys` – Cytoscape session file
- `network.png` – Network image
- `output.csv` – Compound-target-disease interactions
- `input.sdf` – Original input file

## 🧬 Transcriptomics Analysis

Includes Trinity-based de novo transcriptome assembly and pathway analysis using KAAS. Refer to the `transcriptomics/` folder for detailed files and annotation outputs.

## 📄 License

This project is licensed under the MIT License.

## ✍️ Acknowledgements

This work was carried out at the **Bioinformatics Centre, Savitribai Phule Pune University** as part of an M.Sc. in Bioinformatics under the guidance of **Dr. Abhijeet Kulkarni**, with co-guides **Dr. Manali Joshi**, **Dr. Payel Ghosh**, and **Mrs. Smita Saxena**.
