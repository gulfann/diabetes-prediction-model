### Project Report: Diabetes Prediction with SVM
Diabetes prediction with SVM, focusing on class imbalance and recall improvement.
## Dataset Overview

* **Rows:** 1000
* **Features:** 9 (health-related measurements)
* **Target column:** `Diagnosis` (0 = non-diabetic, 1 = diabetic)
* **Imbalance:** 694 (69%) non-diabetic, 306 (31%) diabetic

The imbalance is important because a model can achieve \~69% accuracy just by predicting “non-diabetic” every time.


## Initial Results

* Accuracy \~69% (similar to baseline imbalance).
* The model mostly predicted the majority class (non-diabetic).
* This showed that accuracy was **misleading** — it looked okay, but the model was failing to detect diabetics.

## Addressing Imbalance

* Used `class_weight='balanced'` in SVM.
* This forced the model to give more importance to the minority class (diabetic).

**Results after balancing:**

* Accuracy dropped (\~53%)
* But recall for diabetics increased (model caught more true diabetics)
* Trade-off: fewer false negatives (diabetics correctly predicted) but more false positives (non-diabetics predicted as diabetic).

## Example Case Study

To make the difference clear, I tested the models on this input:

input_data = (3, 95.665270, 54.157100, 23.927648, 
              130.989859, 29.235840, 0.461786, 18.669086)


True label (from dataset): Diabetic
Prediction without class balancing: Non-diabetic (missed the case)

Prediction with class balancing: Diabetic (correct prediction)

## Interpretation
* The first model (no balancing) leaned too heavily toward the majority class (non-diabetic) and failed to detect this case.

* After adding class_weight='balanced', the model gave more weight to the minority class (diabetic) and caught the case correctly.

* This small example highlights why recall is so important for imbalanced medical datasets.

* ⚠️ However, even after balancing, the model overall still struggles. Accuracy dropped to ~53%, and the predictions are inconsistent.


## Conclusion

This project demonstrates the importance of looking beyond accuracy when working with imbalanced datasets.

Even though the model’s predictions were not perfect, the process showed:

1.How imbalance affects performance,

2.Why recall matters more in medical problems,

3.That simply training a model is not enough — critical analysis of results is key,

⚠️ Even with class balancing, the linear SVM is still not reliable for real-world use.

Takeaway: More advanced models (non-linear SVM, Random Forest, XGBoost) and techniques like SMOTE or collecting more data may be necessary to build a system that predicts diabetes more accurately.


