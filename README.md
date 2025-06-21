# 🚑 Accelerating Dengue Drug Discovery Using AI & ChemBERTa

This repository presents a machine learning pipeline that leverages **transformer-based models** and **chemical similarity scoring** to accelerate the early-stage discovery of novel drug candidates for dengue.

---

## 🧪 Project Objective

To develop an AI-driven system that:
- Analyzes known dengue drugs and predicts side effect severity.
- Generates novel molecular structures (SMILES) using chemical transformations.
- Uses **ChemBERTa** to predict toxicity.
- Applies **cosine similarity** to infer side effects of unknown compounds.

---

## 📂 Dataset

- **Source**: 38 dengue-related compounds curated from PubChem, ChEMBL, DrugBank, and PubMed.
- **Columns**:
  - `Drug Name`
  - `Chemical Compound`
  - `Usage`
  - `Dosage`
  - `Side Effects`
  - `Manufacturer`
  - `SMILES` (chemical structure)
  
- **Preprocessing**:
  - Binary labels created based on `"severe"` keyword in side effects.
  - Rows without SMILES were dropped.
  - Dataset split 80/20 for training and testing.

---

## 🧠 Model Architecture

### ⚙️ ChemBERTa (ZINC-based)

- **Model**: `seyonec/ChemBERTa-zinc-base-v1`
- **Tokenizer**: SMILES-specific BPE tokenizer
- **Training**:
  - 5 Epochs
  - Batch size: 8
  - Loss function: Cross Entropy
  - Final Test Accuracy: **97.81%**

---

## 🔍 Cosine Similarity Engine

After classification, ChemBERTa embeddings are extracted for each compound.  
These embeddings are compared using **cosine similarity** to find the most structurally similar known drug.

- **Thresholding**:
  - If similarity > 0.9 → Inherit side effects from known drug.
  - Used as a sanity-check to validate model predictions.

---

## 📊 Visualizations

- **Heatmap**: Top 20 most common side effects
- **Bar Chart**: Class distribution (Severe vs Non-Severe)
- **Histogram**: Severity score distribution across 2000+ generated compounds

---

## 🧬 Novel Molecule Generation

- ~2000 new SMILES strings created using **RDKit**
- Chemical operations used:
  - Ring substitutions
  - Functional group replacements
- Ensures **drug-likeness** and **chemical diversity**

---

## 🧰 Technologies Used

- Python
- RDKit
- PyTorch
- HuggingFace Transformers
- scikit-learn
- pandas, seaborn, matplotlib

---

## 🧾 Output Example

| SMILES                            | Predicted Severity | Most Similar Drug | Similarity Score | Inferred Side Effects                     |
|----------------------------------|--------------------|-------------------|------------------|-------------------------------------------|
| CC(C)CC1=CC=C(C=C1)C(C)C(=O)O     | 1 (Severe)         | Ibuprofen         | 0.95             | Stomach irritation, bleeding              |
| CCOC1=CC=CC=C1C(=O)O              | 0 (Not Severe)     | Acetaminophen     | 0.89             | Mild rash, nausea                         |

---

## 🧪 Conclusion

This project demonstrates how **AI and transformers** can be effectively applied to biomedical challenges, offering:
- Faster identification of drug risks
- Scalable and reusable frameworks
- Interpretable predictions with structural context

---

## 💡 Future Work

- Docking simulations for shortlisted candidates
- Extension to multi-class side effect prediction
- Application to other viral diseases like Zika or Malaria

---
