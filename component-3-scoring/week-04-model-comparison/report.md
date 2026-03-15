# Model Comparison Report — Week 4
**Name:** Mervin Laforteza
**Date:** 03/14/2026
**Capstone Project:** Threat Intelligence Feed Dashboard
**My Component:** Relevance Scorer

## Test Setup
**Input dataset:** 

1. Unauthorized login from IP 198.51.100.4 traced to Moscow targeting user John Miller at 3:47 AM
2. Routine firewall rule update completed on fw-01 during scheduled maintenance window 
3. Phishing email with spoofed Amazon domain detected targeting finance@acmecorp.com 
4. Multiple failed SSH attempts from Beijing IP on Cloudflare production server — 47 attempts in 5 minutes
5. System resource utilization normal across all monitored hosts — no anomalies detected

**Models tested:** 
1. distilbert-base-uncased-finetuned-sst-2-english (sentiment) 
2. facebook/bart-large-mnli (zero-shot classification) 
3. dslim/bert-large-NER (named entity recognition) 
4. Groq Llama 3 8B (LLM classification)

**Evaluation criteria:** label accuracy, confidence score, speed, ease of integration in n8n

## Results Summary
| Record | Sentiment | Zero-Shot | NER Entities | Groq | 
|--------|-----------|-----------|-------------|------|
| 1 | POSITIVE (0.7481) | possible anomaly | Moscow | Critical      | 
| 2 | POSITIVE (0.7481) | routine activity |        | Info          | 
| 3 | POSITIVE (0.7481) | possible anomaly | Amazon | High          |  
| 4 | POSITIVE (0.7481) | possible anomaly | SS     | Critical      | 
| 5 | POSITIVE (0.7481) | routine activity |        | Informational | 

## Analysis
**Where models agreed:** Alerts 2 and 5
**Where models disagreed:** Alerts 3 and 4 which were labeled High and Critical respectively. May have differences because some models tend to treat attempted attacks as critical threats while others only use it for confirmed system compromise.
**Most accurate model overall:** The Llama 3.1 model utilized by Groq
**Fastest/most practical:** The Llama 3.1 model utilized by Groq would be the fastest and most practical at scale

## Recommended Models for My Capstone Component
**Component:** Relevance Scorer
**Primary model:** Llama 3.1 (Groq) - evaluates whether each threat is relevant to the organization's technology stack by analyzing the alert content and comparing it to technologies in the Airtable.
**Secondary model (if applicable):** Hugging Face NER Model - used to extract entities such as organizations, locations, and other indicators that help identify what systems or infrastructure may be involved in the threat.
**Rejected models and why:** - 
1. Hugging Face Sentiment Analysis model - Only measures emotional tone rather than security risk or relevance
2. NER - only approach - only extracts entities without any context on the actual threat.

## Failure Cases and Limitations
The NER model generated an output of "SS" for Alert 4. It extracted this entity from the word "SSH" in the alert. This demonstrates how this model is not optimized for cybersecurity terminology and may provide incorrect entity extraction. This model would be useful if used in tandem with other models that can provide more context on the entity and its connection to the alert.

## Next Steps
I would use a larger dataset for this system especially in the case of relevance scoring. If possible through n8n, I would connect my n8n workflow to a live stream of data so that alerts are monitored continuously throughout the day.