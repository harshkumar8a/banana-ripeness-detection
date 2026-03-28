# 📷🍌⚙️ **Banana Ripeness Detection with ResNet18**


---

## 🍌📝⚙️ **Project Overview.**
* ***This notebook, developed for the Computer Hardware module, uses a ResNet-18 convolutional network to classify banana ripeness into four categories: unripe, ripe, overripe, and rotten.***
* ***In addition to model training and evaluation, the project benchmarks serial and parallel CPU-based image preprocessing, with model training and inference performed on the GPU.***
* ***Data augmentation was applied to the training set to improve robustness across varied image conditions, reducing overfitting and enhancing generalisation to unseen samples.***

---

## 📂📊🔍 **Dataset Source.**
* ***The dataset used for this project was obtained from the [Banana Ripeness Classification Dataset on Kaggle](https://www.kaggle.com/datasets/shahriar26s/banana-ripeness-classification-dataset).***
* ***It contains labelled images categorised into *overripe*, *ripe*, *rotten*, and *unripe* classes, which served as the basis for model training and evaluation.***

---

## 🔎📈📊 **Results Overview.**

## 🧠📊🔍 **Model Evaluation Summary.**
* ***Final Test Accuracy: 98.04%***
* ***Final Training Accuracy: 96.62%***
* ***Final Validation Accuracy: 97.60%***
* ***Best Training Accuracy: 96.62%***
* ***Best Validation Accuracy: 98.22%***
* ***Macro F1-score: 0.98***
* ***Weighted F1-score: 0.98***
* ***Training Time: 338 seconds***
* ***Total Epochs: 5 (completed all scheduled epochs; early stopping was not triggered)***

---

## 🔍📉🧠 **Misclassification Patterns and Interpretation.**
* ***The most frequent confusion occurred where the true class ‘overripe’ was predicted as ‘ripe’.***
* ***This is plausible given the visual overlap between adjacent ripeness stages (colour transition, bruising cues, and texture changes), particularly under varied lighting and backgrounds.***
* ***Overall, the confusion matrix indicates that most predictions fall on the diagonal, with errors concentrated in a small number of borderline cases.***

---

## ✅📊📋 **Classification Report Table.**

| Class        | Precision | Recall | F1-Score | Support |
| ------------ | --------- | ------ | -------- | ------- |
| Overripe     | 0.97      | 0.96   | 0.96     | 113     |
| Ripe         | 0.96      | 1.00   | 0.98     | 154     |
| Rotten       | 1.00      | 0.97   | 0.98     | 185     |
| Unripe       | 0.99      | 1.00   | 1.00     | 110     |
| Accuracy     | 0.98      | 0.98   | 0.98     | 562     |
| Macro Avg    | 0.98      | 0.98   | 0.98     | 562     |
| Weighted Avg | 0.98      | 0.98   | 0.98     | 562     |

📝🔍 ***Note: “support” is the number of occurrences of each class in `y_true`. When `classification_report` is converted into tabular form, ensure “accuracy” is treated as a scalar summary (not a per-class row). The correct total sample count for this evaluation is `562`.***

---

## 🔍📈🧠 **Interpretation of Results.**

***The classification report below highlights the model’s predictive strengths and limitations across the four banana ripeness classes:***

* 🌕 ***‘Overripe’ shows strong performance overall, but is the most error-prone class due to adjacency effects.***
  * 🚨 ***Most confusion: true class ‘overripe’ misclassified as ‘ripe’ (5 cases).***

* 🍌 ***‘Ripe’ demonstrates perfect recall (1.00), indicating all ripe bananas were correctly identified in the test set.***
  * ✅ ***No ripe bananas were misclassified (0 cases).***

* 🧪 ***‘Rotten’ maintains excellent precision (1.00), with a small number of misses reflected in recall (0.97).***
  * 🔎 ***Observed smaller confusions: rotten → overripe (3), rotten → ripe (2), rotten → unripe (1).***

* 🍃 ***‘Unripe’ achieves perfect recall (1.00), supporting reliable early-stage sorting decisions.***
  * ✅ ***No unripe bananas were misclassified (0 cases).***

---

## 🌍📊🚀 **Global Model Performance Summary.**
* ✅ ***Final Test Accuracy: 98.04%***
* 🧠 ***Macro and Weighted F1-scores: 0.98***

**This outcome reflects:**
* ✅ ***Strong generalisation across all classes, with errors concentrated in a small number of borderline cases.***
* 🧠 ***Stable learning behaviour, with training accuracy (96.62%) and validation accuracy (97.60%) closely aligned.***
* 📊 ***Consistently high class-wise performance, supporting reliable multi-class decision-making in deployment contexts.***
* 🔐 ***Clear class-wise reporting enables transparent monitoring of performance and misclassification patterns in real-world use.***

---

## 🚀💻⚙️ **Device Configuration.**
* ***GPU: Tesla P100-PCIE-16GB***
* ***Total GPU Memory: 17059.55 MB***
* ***CPU: Intel(R) Xeon(R) CPU @ 2.00GHz***
* ***RAM: 33.66 GB (Memory Usage: 5.5%)***

---

## ⏱️🧪⚡ **Serial vs Parallel Processing: Image Preprocessing Benchmark Summary.**

| Category | Images | Serial Time  | Parallel Time | Serial FPS | Parallel FPS | Execution Time Improvement (Factor) |
| -------- | ------ | ------------ | ------------- | ---------- | ------------ | ----------------------------------- |
| Overripe | 113    | 0.22 seconds | 0.64 seconds  | 511.89     | 175.61       | 0.34                                |
| Ripe     | 154    | 0.29 seconds | 0.17 seconds  | 527.97     | 923.78       | 1.75                                |
| Rotten   | 185    | 0.36 seconds | 0.18 seconds  | 508.09     | 1037.65      | 2.04                                |
| Unripe   | 110    | 0.21 seconds | 0.12 seconds  | 533.60     | 884.84       | 1.66                                |

📝🚀⚡ ***Key takeaway: Parallel preprocessing is faster for ripe, rotten, and unripe, whilst overripe is faster in serial due to parallel overhead; overall mean improvement across all categories is 1.45×.***

📝🔍✅ ***Notes (for correctness/definitions): scikit-learn’s classification report macro averages are unweighted means, while weighted averages are support-weighted means. Parallel speedups can be limited by serial portions and coordination overhead (Amdahl-style limits), which explains cases where parallel runs slower for small workloads in practice.***

---

## ⏱️🚀📈 **Execution Time Improvement (Factor) Summary.**
* ***A value above 1.00 means parallel processing outpaced serial processing.***
* ***A value below 1.00 means serial processing was faster than parallel.***
* ***Example: in the ‘ripe’ category, the improvement factor is 1.75, meaning parallel preprocessing ran about 1.75× faster than serial (923.78 FPS vs 527.97 FPS).***
* ***Across all four categories, the average Execution Time Improvement (Factor) was approximately 1.45, indicating an overall advantage for parallel execution.***

> ⚠️ ***For smaller workloads, parallel overhead can reduce or negate speed gains.***

---

## 🔍📝📁 **Exported Artefacts.**
* ***`best_model.pth` — Trained Model Checkpoint.***
* ***`accuracy_loss_curves.pdf` <br>`accuracy_loss_curves.png`***
* ***`confusion_matrix_with_interpretation.pdf` <br> `confusion_matrix_with_interpretation.png`***
* ***`classification_report.pdf` <br> `classification_report.png`***
* ***`fps_comparison_chart.pdf` <br> `fps_comparison_chart.png`***
* ***`preprocessing_benchmark_results.csv` — Benchmark Table.***

📝 ***All files are programmatically generated during notebook execution and packaged into `output_bundle.zip`.***

---

## **📝📂📚 Note on Model Output Availability.**
* ***The trained model is utilised in the notebook [ResNet18 Banana Ripeness CPU Benchmark](https://www.kaggle.com/code/sandhyapalaniappan/resnet18-banana-ripeness-cpu-benchmark).***
* ***Model Access 🌐🔗📍 – The trained ResNet18 model is published and publicly accessible here: [Banana Ripeness Classifier: ResNet18 Model](https://www.kaggle.com/models/sandhyapalaniappan/banana-ripeness-resnet18-v1).***

---

## 🙏💡📝 **Final Note.**
* ***This Computer Hardware Module Project showcases a balanced AI pipeline: a robust model trained on GPU alongside optimised CPU-based image preprocessing workflows.***
* ***This notebook demonstrates how intelligent model design, GPU acceleration, and CPU-level parallelism can be harmonised to achieve strong classification accuracy and system efficiency, essential qualities for scalable AI deployments in agriculture, especially when throughput, latency, and resource utilisation need to remain well-optimised in production.***
