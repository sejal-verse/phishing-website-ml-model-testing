# 🛡️ PhishGuard — Phishing Website Detection using Machine Learning

PhishGuard is a machine-learning project that classifies websites as **phishing or legitimate** using website-related characteristics from the UCI Phishing Websites dataset.

The project goes beyond simply training a model. It investigates model performance, prediction errors, robustness, feature importance, model improvement, and final evaluation before integrating the trained model into an interactive Streamlit application.

---

## 🎯 Project Objective

The objective of this project is to:

* Build a machine-learning system for phishing website classification.
* Explore and preprocess the phishing website dataset.
* Establish a baseline Decision Tree model.
* Compare multiple machine-learning algorithms.
* Analyze incorrect predictions.
* Test model robustness.
* Investigate feature importance.
* Tune the Decision Tree model.
* Perform a final multi-metric evaluation.
* Deploy the trained model through an interactive Streamlit interface.

### Project workflow

```text
Dataset
   ↓
EDA
   ↓
Preprocessing
   ↓
Baseline Model
   ↓
Model Comparison
   ↓
Error Analysis
   ↓
Robustness Testing
   ↓
Feature Importance
   ↓
Model Improvement
   ↓
Final Evaluation
   ↓
Streamlit Application
```

---

## 📊 Dataset

The project uses the **UCI Phishing Websites dataset**.

Dataset characteristics:

* **11,055 instances**
* **30 input features**
* Binary classification task
* Target labels:

  * `-1` → Phishing
  * `+1` → Legitimate

The dataset contains encoded characteristics related to URLs, domains, links, webpage behavior, and other website properties.

Dataset source:

**UCI Machine Learning Repository — Phishing Websites**

---

## 🤖 Machine Learning Approach

The project uses a Decision Tree as the main model and compares it with additional machine-learning algorithms during the model comparison stage.

The project includes:

### Baseline Model

A Decision Tree classifier is trained as the baseline.

### Model Comparison

The project compares:

* Decision Tree
* Logistic Regression
* Random Forest
* K-Nearest Neighbors

### Error Analysis

Incorrect predictions are investigated to understand:

* False positives
* False negatives
* Patterns in model mistakes

For this project:

```text
False Positive = Legitimate website predicted as phishing
False Negative = Phishing website predicted as legitimate
```

### Robustness Testing

The model is tested under a controlled feature perturbation to investigate prediction stability.

### Feature Importance

Decision Tree feature importance is analyzed to identify which website characteristics contributed most strongly to model decisions.

### Model Improvement

Decision Tree hyperparameters are investigated to evaluate whether tuning can improve model behavior.

---

## 📈 Final Model Evaluation

The final evaluation compares the baseline and tuned Decision Tree models using:

* Accuracy
* Precision
* Recall
* F1 Score
* ROC-AUC

Current evaluation results:

| Model                  | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
| ---------------------- | -------: | --------: | -----: | -------: | ------: |
| Baseline Decision Tree |   97.11% |    97.22% | 96.22% |   96.72% |  98.05% |
| Improved Decision Tree |   94.80% |    93.64% | 94.69% |   94.17% |  98.65% |

An important observation is that the tuned model does **not** outperform the baseline across every metric. While it achieves a higher ROC-AUC, the baseline model performs better on accuracy, precision, recall, and F1 score on the evaluated holdout set.

This result is retained rather than presenting the tuning process as successful simply because it was expected to improve the model.

---

## 📊 Confusion Matrix

The final evaluation also includes a confusion matrix for the improved Decision Tree.

The matrix helps examine:

* Correctly identified phishing websites
* Phishing websites classified as legitimate
* Legitimate websites classified as phishing
* Correctly identified legitimate websites

The visualization is available in:

```text
reports/figures/final_confusion_matrix.png
```

---

## 🔍 Feature Importance

Feature importance analysis is included to investigate which website characteristics have the greatest influence on the Decision Tree.

Results are available in:

```text
reports/feature_importance.csv
reports/figures/feature_importance.png
```

Feature importance should be interpreted as the contribution of a feature within the trained model, rather than proof that the feature independently causes a website to be phishing.

---

## 🌐 Streamlit Application

The project includes an interactive Streamlit application called **PhishGuard**.

The application allows users to:

* Enter encoded website characteristics.
* Analyze the supplied characteristics.
* View the predicted class.
* View phishing and legitimate probabilities.
* View model performance.
* View the confusion matrix.
* Explore feature importance.
* Understand the overall machine-learning workflow.

### Run the application

First activate the virtual environment.

Then from the project root:

```powershell
streamlit run app/app.py
```

The application will open in your browser.

---

## 📁 Project Structure

```text
phishing-website-ml-model/
│
├── app/
│   └── app.py
│
├── data/
│   └── raw/
│       └── phishing.arff
│
├── models/
│   ├── phishing_model.pkl
│   └── feature_columns.pkl
│
├── reports/
│   ├── figures/
│   │   ├── feature_importance.png
│   │   └── final_confusion_matrix.png
│   │
│   ├── error_analysis.csv
│   ├── robustness_results.csv
│   ├── feature_importance.csv
│   └── final_results.csv
│
├── src/
│   ├── 01_environment_test.py
│   ├── 02_load_dataset.py
│   ├── 03_eda.py
│   ├── 04_visualize_data.py
│   ├── 05_preprocess.py
│   ├── 06_baseline_model.py
│   ├── 07_model_evaluate.py
│   ├── 08_model_comparison.py
│   ├── 09_error_analysis.py
│   ├── 10_robustness_testing.py
│   ├── 11_feature_importance.py
│   ├── 12_model_improvement.py
│   ├── 13_final_evaluation.py
│   └── 14_save_model.py
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## ⚙️ Installation

Clone the repository:

```powershell
git clone https://github.com/sejal-verse/phishing-website-ml-model.git
```

Move into the project directory:

```powershell
cd phishing-website-ml-model
```

Create a virtual environment:

```powershell
py -3.13 -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
pip install -r requirements.txt
```

---

## ▶️ Running the Project

### Run individual ML pipeline stages

For example:

```powershell
python src/03_eda.py
```

```powershell
python src/13_final_evaluation.py
```

Save the trained model:

```powershell
python src/14_save_model.py
```

Launch the application:

```powershell
streamlit run app/app.py
```

---

## ⚠️ Important Limitation

PhishGuard currently **does not accept a live website URL and automatically scan it**.

The application works with the 30 encoded website characteristics used by the trained model.

Therefore, entering a URL such as:

```text
https://example.com
```

does not currently cause the application to visit or inspect that website.

A future version could implement a feature-extraction pipeline that converts a URL/webpage into the same 30 model features before making a prediction.

---

## 🚀 Future Improvements

Possible future improvements include:

* Automatic feature extraction from URLs.
* Live URL analysis.
* Additional machine-learning models.
* Cross-validation-based model evaluation.
* More systematic hyperparameter optimization.
* Improved robustness testing.
* Explainable AI techniques such as SHAP.
* More detailed EDA visualizations.
* Improved Streamlit UI.
* Deployment as a public web application.
* Automated model testing and monitoring.

---

## 🧰 Technologies Used

* Python
* Pandas
* NumPy
* SciPy
* Scikit-learn
* XGBoost
* Matplotlib
* Seaborn
* Joblib
* Streamlit
* Jupyter

---

## 📌 Disclaimer

This project is an educational machine-learning demonstration.

A prediction from this model should not be treated as a definitive security verdict for a real-world website. The application is based on patterns learned from the training dataset and does not currently perform live website inspection.
