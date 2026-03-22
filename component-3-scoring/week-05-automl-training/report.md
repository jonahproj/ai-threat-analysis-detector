# Week 5 Report: AutoML Training & Fine-Tuned Model Evaluation
**Name:** Mervin Laforteza
**Date:** 03/22/2026
**Capstone Project:** Threat Intelligence Feed Dashboard
**My Component:** Relevance Scorer

### Training Setup 
- **Task:** Phishing vs Legitimate email screenshot classification
- **Training images per class:** 25
- **Test images per class:** 5 
- **Total training time:** 31 seconds

### Test Results
| # | Actual Class | Predicted Class | Confidence | Correct? | 
|---|--------------|-----------------|------------|----------| 
| 1 | Phishing     | Phishing        | 100%       |    Yes   |
| 2 | Phishing     | Phishing        | 100%       |    Yes   |
| 3 | Phishing     | Phishing        | 88%        |    Yes   |
| 4 | Phishing     | Phishing        | 90%        |    Yes   |
| 5 | Phishing     | Phishing        | 100%       |    Yes   |
| 6 | Legitimate   | Legitimate      | 51%        |    Yes   |
| 7 | Legitimate   | Legitimate      | 100%       |    Yes   |
| 8 | Legitimate   | Phishing        | 99%        |    No    |
| 9 | Legitimate   | Phishing        | 100%       |    No    |
| 10 | Legitimate  | Legitimate      | 99 %       |    Yes   |

### Confusion Matrix
| | Predicted: [Class 1] | Predicted: [Class 2] 
| |---|---|---|
| **Actual: [Class 1]** | TP = 5 | FN = 2 | 
| **Actual: [Class 2]** | FP = 0 | TN = 3 |

### Calculated Metrics 
- **Accuracy:** 80% 
- **Precision:** 100% 
- **Recall:** 71.4%
- **F1 Score:** 83%

### Interpretation 
[2-3 sentences: Is your model better at precision or recall? Which errors did it make? What would improve it?]

My model is better at precision. It made errors when looking at legitimate email and marking them as phishing. This model can be improved by adding more data points and more varying types of data. For instance, training it to recognize emails with images as either phishing or legitimate.

## Part B: Generic vs Fine-Tuned Model Comparison

### Models Tested 

1. **Generic:** distilbert-base-uncased-finetuned-sst-2-english (sentiment) 
2. **Fine-Tuned A:** valhalla/distilbart-mnli-12-3 - A transformer model fine-tuned on the MultiNLI dataset for zero-shot classification, used to determine how relevant a cybersecurity threat is to a given technology stack without requiring additional training.
3. **Fine-Tuned B:** dbmdz/bert-large-cased-finetuned-conll03-english -  A BERT-based model fine-tuned on the CoNLL-2003 dataset for named entity recognition (NER), used to extract key entities such as software, systems, and organizations from threat intelligence data.

### Results

| Input | Generic Label (Score) | Fine-Tuned A Label (Score) | Fine-Tuned B Label (Score) | Best Model |
|-------|-----------------------|-----------------------------|--------------------------|------------|
| Record 1 | NEGATIVE (0.9961)  | MODERATELY RELEVANT (0.5315)|                          | FINE-TUNED A| 
| Record 2 | NEGATIVE (0.9986)  | MODERATELY RELEVANT (0.6333)| SS (0.6194)              | FINE-TUNED A| 
| Record 3 | NEGATIVE (0.9959)  | HIGHLY RELEVANT (0.4810)    | AMAZON (0.9957)          | FINE-TUNED A|
| Record 4 | NEGATIVE (0.9996)  | MODERATELY RELEVANT (0.6558)|                          | FINE-TUNED A|
| Record 5 | NEGATIVE (0.9979)  | MODERATELY RELEVANT (0.5475)| MOSCOW (0.9998)          | FINE-TUNED A|

### Analysis

**Generic model strengths:** Good at assessing negative tone or suspicious wording

**Generic model weaknesses:** Labeled everything as negative. Doesn't distinguish between real threats and normal activity

**Fine-tuned model advantage:** 

- Fine-Tuned A (Zero-Shot) - Actually interprets severity and context
- Fine-Tuned B (NER) - Able to extract meaningful entities  

**Biggest surprise:** = Generic model produced really high confidence scores for all outputs even when the alert is a system activity

### Recommended Model for My Capstone Component

**Component:** Relevance Scorer

**Primary model:** valhalla/distilbart-mnli-12-3 - Provides context-aware classification and works with dynamic labels

**Confidence threshold:** 60% since this is what my data has shown. Any higher would miss some threats

**Priority metric:** Precision - so that false positives are avoided

## Limitations & Next Steps
Future work will focus on domain-specific fine-tuning, hybrid model integration, and incorporating structured threat intelligence data to improve both precision and contextual relevance