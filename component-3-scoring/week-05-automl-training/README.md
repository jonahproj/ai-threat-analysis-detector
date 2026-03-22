# Week 5: AutoML & No-Code Model Training

Trained a custom image classifier with Google Teachable Machine and compared generic vs fine-tuned Hugging Face models for the Relevance Scorer component of our Threat Intelligence Feed Dashboard.

## Custom Model Training 
- Built a [Phishing/Legitimate] image classifier with Teachable Machine 
- Achieved 80% accuracy on 10 held-out test images
- Precision: 100% | Recall: 71.42% | F1: 83.33%

## Fine-Tuned Model Comparison Compared 3 models (1 generic + 2 fine-tuned) on 5 test inputs: 

- Generic: distilbert-sst-2 (sentiment)
- Fine-Tuned A: valhalla/distilbart-mnli-12-3
- Fine-Tuned B: dbmdz/bert-large-cased-finetuned-conll03-english 

## Finding 
Recommended distilbart-mnli-12-3 for Relevance Scorer because it was able to provided contextual and actionable data from the input. Fine-tuned models showed higher performance with more relevant labels.

See `report.md` for full analysis
