# Advandex Click-Through Rate (CTR) Prediction Model

## 📋 Project Overview
Development of a machine learning model for predicting click-through probability for the Advandex advertising platform. The project aims to create a tool that enables precise CTR estimation, which is essential for optimizing ad delivery, improving user experience, and maximizing advertiser ROI.

Research relevance is driven by the competitive digital advertising landscape where accurate CTR prediction directly impacts platform revenue and advertiser satisfaction. Precise CTR estimation allows for smarter bidding, better ad placement, and improved targeting efficiency.

## 🔍 Machine Learning Problem Statement

### **Task Type**
**Binary Classification** — predicting whether an ad impression belongs to one of two classes: "no click" (0) or "click" (1).

### **Learning Type**
**Supervised Learning** — based on labeled historical data of ad impressions and corresponding click events.

### **Target Variable**
`click` — binary feature:
- `0`: ad impression did not result in a click
- `1`: user clicked on the ad

### **Success Criteria**
The model must achieve balance between:
- **High Ranking Quality** — effectively separate ads with high click potential from low-click ones
- **Excellent Calibration** — predicted probabilities must reliably reflect actual click frequency
- **Stability** — consistency on new data (minimal difference in key metrics between train/valid/test splits)

## 📊 Quality Metrics

### **Primary Metrics:**
**PR-AUC** (Precision-Recall Area Under Curve) — primary metric for classification quality. Most informative with strong class imbalance (clicks are rare events), as it focuses on correct prediction of the target class (clicks) while ignoring correct predictions of the abundant "no click" class.

**Log Loss** (Logistic Loss) — key metric for evaluating the accuracy of predicted probabilities. Heavily penalizes the model for both classification errors and excessive "confidence" in incorrect predictions. Minimizing Log Loss directly improves calibration.

**Brier Score** — combined metric measuring both calibration accuracy and resolution of predictions. A perfectly calibrated model has a Brier Score close to 0. This provides a direct integrated assessment of probabilistic forecast reliability.

## 📈 Model Performance Results

### **Model Improvement vs. Baseline**
Yes, quality has significantly improved compared to the DummyClassifier baseline:
- **PR-AUC improved**: 0.1725 → 0.3395
- **Log Loss reduced**: 10.1955 → 0.5177
- **Brier Score improved**: 0.2829 → 0.1322

### **Most Influential Features on Click Probability**
Analysis of model coefficients revealed the top 5 most significant features:
1. `device_conn_type_5` (coefficient +2.88) — connection type
2. `C1_grouped_1005` (coefficient +2.50) — contextual category feature
3. `C1_grouped_1010` (coefficient +2.23) — another contextual category
4. `device_type_1` (coefficient +2.12) — device type
5. `banner_pos_grouped_1` (coefficient +1.74) — banner position

Technical parameters (connection, device) and contextual factors (category, position) have the greatest influence on CTR.

### **Model Calibration Quality**
The model demonstrates good calibration:
- **Brier Score**: 0.1312 (acceptable for imbalanced data)
- **ECE**: 0.1119 after calibration ("good" level according to industry standards)

## 🚀 Production Readiness Assessment

The model is conditionally ready for production use, with some caveats:

### **Strengths:**
- Stable quality on validation and test sets
- Good probability calibration
- Interpretable results
- Identification of business-significant patterns

### **Areas for Consideration:**
- PR-AUC of 0.3395 indicates room for improvement in classification quality
- Continuous monitoring required for concept drift in ad patterns
- Potential need for retraining frequency optimization based on data dynamics
