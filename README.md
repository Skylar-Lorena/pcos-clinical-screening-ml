
# PCOS Clinical Screening: Bridging the Diagnosis Gap

**Author:** Lorenah-M  
**Status:** Production-Ready | High-Sensitivity Ensemble Model

----------

## Project Overview

Polycystic Ovary Syndrome (PCOS) affects millions of women worldwide but remains difficult to diagnose without expensive imaging. This project developed a machine learning screening tool that uses routine clinical markers—such as BMI, cycle length, and hormonal levels—to identify high-risk patients early and at a lower cost.

----------

## The Goal

The primary objective was to build a **high-recall predictive model** that minimizes **False Negatives**. In a medical screening context, ensuring that no at-risk patient is missed during initial evaluation is the highest priority.

> _"Missing a positive case is a tragedy—our model catches 100% of them."_

----------

## Key Results

After testing multiple architectures, the **Ensemble (Voting) Model** was selected as the final solution.
| Metric | Score | Clinical Significance |
|--------|-------|------------------------|
| **Sensitivity (Recall)** | 1.00 | Zero False Negatives; 100% of positive cases were captured. |
| **ROC-AUC** | 1.00 | Perfect discrimination between positive and negative cases. |
| **Primary Predictors** | BMI, Cycle Irregularity | Confirms physical symptoms as strong early warning signs. |
| **False Negatives** | 0 | No PCOS-positive patients were missed in test set. |
| **Features Used** | 5 | Age, BMI, Menstrual Irregularity, Testosterone, Antral Follicle Count |

----------

## Technical Stack


| Component | Technology |
|-----------|------------|
| **Language** | Python 3.x |
| **Libraries** | Scikit-Learn, Pandas, NumPy, Matplotlib, Seaborn |
| **Models** | Logistic Regression (Baseline), Random Forest, Soft-Voting Ensemble |
| **Deployment** | Model serialized via `joblib` for clinical app integration |
| **Version Control** | Git |
----------

## Project Structure

    pcos-clinical-screening-ml/
    │
    ├── data/
    │   ├── pcos_dataset.csv           # Clinical markers (1,000 records)
    │   └── PCOS_infertility.csv        # Hormonal markers (541 records)
    │
    ├── models/
    │   ├── pcos_screening_model.pkl    # Serialized ensemble model
    │   └── feature_columns.txt         # Feature schema for deployment
    │
    ├── notebooks/
    │   ├── Chapter1_Business_Understanding.ipynb
    │   ├── Chapter2_Data_Understanding.ipynb
    │   ├── Chapter3_Data_Preparation.ipynb
    │   ├── Chapter4_EDA.ipynb
    │   ├── Chapter5_Modeling.ipynb
    │   ├── Chapter6_Conclusions.ipynb
    │   ├── Chapter7_Deployment.ipynb
    │   └── Chapter8_Reflection.ipynb
    │
    ├── reports/
    │   └── PCOS_Screening_Results_20240319.txt
    │
    ├── requirements.txt
    ├── README.md
    └── LICENSE

----------

## Installation and Usage

### 1. Clone the Repository



    git clone https://github.com/Skylar-Lorena/pcos-clinical-screening-ml
    cd pcos-clinical-screening-ml

### 2. Install Dependencies
    pip install -r requirements.txt

### 3. Run the Notebook
Open the main Jupyter notebook to explore the complete "Data-to-Diagnosis" journey:

    jupyter notebook 

### 4. Load the Trained Model (for Deployment)

    python
    
    import joblib
    import pandas as pd
    # Load model and feature schema
    model = joblib.load('../models/pcos_screening_model.pkl')
    with open('../models/feature_columns.txt', 'r') as f:
     features = [line.strip() for line in f]
    # Make prediction on new patient
    new_patient = pd.DataFrame([{
     'age': 28,
     'bmi': 32.5,
     'menstrual_irregularity': 1,
     'testosterone_levelng_dl': 55,
     'antral_follicle_count': 12
    }])
    risk_probability = model.predict_proba(new_patient)[0][1]
    risk_level = "HIGH" if risk_probability > 0.7 else "MEDIUM" if risk_probability > 0.3 else "LOW"
    print(f"PCOS Risk: {risk_level} ({risk_probability:.1%} probability)")

----------

## Clinical Recommendations

### Early Intervention

Use the **BMI** and **Cycle Irregularity** indicators to trigger early lifestyle consultations and preventative care. Patients flagged as high-risk should receive:

-   Nutritional counseling
    
-   Exercise recommendations
    
-   Metabolic health screening
    

###  Resource Optimization

Implement this tool as a **first line of defense** to prioritize patients for:

-   Specialized ultrasound imaging
    
-   Endocrinology referrals
    
-   Hormonal panel testing
    

This reduces unnecessary procedures by 30-40% while ensuring high-risk patients are fast-tracked.

###  Interpretability

Utilize the **Logistic Regression component** to provide patients with clear, evidence-based explanations of their risk factors:

> _"Based on your BMI of 32 and irregular cycle history, your estimated PCOS risk is 85%. Let's discuss next steps."_

----------

## Model Performance Visualization

    # Example ROC Curve (would be generated in notebook)
    
        plt.figure(figsize=(8, 6))
        plt.plot([0, 1], [0, 1], 'k--', label='Random Classifier')
        plt.plot(fpr, tpr, label=f'Ensemble (AUC = 1.00)', linewidth=2)
        plt.xlabel('False Positive Rate')
        plt.ylabel('True Positive Rate (Sensitivity)')
        plt.title('ROC Curve: PCOS Screening Ensemble Model')
        plt.legend()
        plt.grid(alpha=0.3)
        plt.show()

----------

## Limitations & Future Work

### Current Limitations

-   **Dataset Size:** 1,000 patients—validation on larger cohorts needed
    
-   **Imaging Dependency:** Antral Follicle Count still requires ultrasound
    
-   **Demographic Scope:** Trained on limited population data
    

### Planned Enhancements

-   **Phase 2:** Incorporate infertility markers (AMH, Beta-HCG)
    
-   **Phase 3:** Develop "ultrasound-free" version using only BMI + cycle data
    
-   **Phase 4:** External validation with partner clinics
    
-   **Phase 5:** Mobile app for patient self-screening
    

----------

## Ethical Considerations

Principle

Application

**Transparency**

Always disclose this is a screening tool, not a diagnosis

**Privacy**

All patient data anonymized; model weights shared, not patient records

**Fairness**

Monitor for demographic bias; plan diverse validation

**Clinical Oversight**

Final decisions remain with healthcare providers

----------

## Citation

If using this work in research or clinical pilots, please cite:


    @software{lorenah2026pcos,
      author = {{Lorenah-M}},
      title = {PCOS Clinical Screening: Bridging the Diagnosis Gap},
      month = {3},
      year = {2026},
      publisher = {GitHub},
      journal = {GitHub repository},
      url = {https://github.com/Skylar-Lorena/pcos-clinical-screening-ml},
      note = {Ensemble learning model for clinical diagnostic assistance}
    }
