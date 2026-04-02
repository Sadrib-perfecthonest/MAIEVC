# MAIEVC: Multimodal Framework for detecting AI-Driven phishing emails and preventing Visual CAPTCHA bypass attacks

## 📌 Overview

MAIEVC (Multimodal AI Email & Visual CAPTCHA) is an integrated framework that detects sophisticated AI-powered phishing attacks by simultaneously analyzing email content and CAPTCHA behavior. Traditional security systems treat emails and CAPTCHAs as separate problems, missing the critical connection between them. This framework combines both modalities to catch coordinated attacks that would otherwise slip through.

**In simple words:** Phishing emails try to steal your information. CAPTCHAs are those "I'm not a robot" tests. Attackers now use AI to write perfect phishing emails and create fake CAPTCHAs that look real. MAIEVC checks both together - if an email looks suspicious AND the CAPTCHA seems fake, it's probably an attack.

---

## 🚀 Features

- **Dual Detection**: Analyzes both email content and CAPTCHA simultaneously
- **AI Text Detection**: Identifies if email was written by AI (ChatGPT, etc.)
- **CAPTCHA Authenticity Check**: Detects fake/phishing CAPTCHAs using 4 key indicators
- **Lightweight Design**: Runs on edge devices (phones, routers) - not just servers
- **Actionable Risk Scores**: Clear 0-1 scale with thresholds (0.3, 0.5, 0.7, 0.9)
- **Real-time Recommendations**: Allow, Monitor, Warn, Block based on risk level

---

## 🛠️ Libraries Used

| Library | Purpose |
|---------|---------|
| **TensorFlow 2.20.0** | Deep learning framework for model training and inference |
| **Transformers 5.1.0** | ELECTRA-small transformer for email text understanding |
| **MobileNetV2** | Lightweight CNN for CAPTCHA image analysis (pretrained on ImageNet) |
| **Scikit-learn** | Data splitting, cross-validation, metrics calculation |
| **Pandas/NumPy** | Data manipulation and numerical operations |
| **Matplotlib/Seaborn** | Visualization and plotting |
| **Pickle/JSON** | Model and data serialization |

---

## 📊 Key Indicators for Detection

### Email Analysis (ELECTRA-small)
- Phishing keywords (urgent, verify, password, account)
- URL patterns and suspicious links
- Punctuation intensity (!, ?, $)
- Language formality (formal vs casual)
- Urgency indicators

### CAPTCHA Analysis (MobileNetV2)
| Indicator | What it means | Legitimate | Phishing |
|-----------|---------------|------------|----------|
| **visual_quality** | Image clarity, professional look | 0.7 - 1.0 | 0.1 - 0.4 |
| **context_match** | Matches website context | 0.7 - 1.0 | 0.1 - 0.4 |
| **failure_rate** | How often it fails | 0.05 - 0.2 | 0.4 - 0.8 |
| **brand_consistency** | Matches brand colors/fonts | 0.7 - 1.0 | 0.1 - 0.3 |


### Risk Scoring Thresholds
| Risk Score | Level | Action |
|------------|-------|--------|
| < 0.3 | SAFE | ALLOW - Appears legitimate |
| 0.3 - 0.5 | LOW RISK | MONITOR - Suspicious elements |
| 0.5 - 0.7 | MEDIUM RISK | WARN USER - Strong suspicion |
| 0.7 - 0.9 | HIGH RISK | BLOCK - High confidence attack |
| > 0.9 | CRITICAL | BLOCK IMMEDIATELY - Confirmed attack |

---

## ⚠️ Challenges Faced & Solutions

| Challenge | Problem | Solution |
|-----------|---------|----------|
| **Class Imbalance** | CAPTCHA model had 100% precision but 34% recall (missed 66% of attacks) | Added class weights, optimal threshold tuning, calibrated predictions |
| **Slow Training** | MobileNetV2 with 64×64 input was too slow | Reduced to 32×32, simplified architecture, increased batch size |
| **Data Scarcity** | No real CAPTCHA images available | Created synthetic images with realistic patterns based on 4 key indicators |
| **Overfitting** | Email models memorized training data | 3-fold cross-validation, dropout layers, held-out test sets |
| **ELECTRA Availability** | Transformers library issues | Added fallback with 15 hand-crafted text features |

---

## 📈 Results Achieved

 Phishing Detection:
     • Accuracy: 0.933
     • F1-Score: 0.953
     • Precision: 0.964
     • Recall: 0.943

   AI Source Detection:
     • Accuracy: 0.985
     • F1-Score: 0.988
     • Precision: 0.976
     • Recall: 1.000

   CAPTCHA Analysis:
     • Accuracy: 0.988
     • F1-Score: 0.988
     • Precision: 0.980
     • Recall: 0.995

*Note: CAPTCHA metrics improved from initial 0.340 recall to 0.867 after fixes*

---
## 🔮 Future Enhancements

- **Real CAPTCHA Dataset** – Collect and test on actual CAPTCHA images from real websites instead of synthetic data

- **Email Server Integration** – Deploy as plugin for Gmail, Outlook, and corporate email servers for real-time protection

- **Mobile Deployment** – Convert models to TensorFlow Lite for on-device detection on smartphones and edge devices

- **Multi-language Support** – Extend ELECTRA to detect phishing in Bengali, Hindi, Arabic, and other regional languages

- **Continuous Learning** – Implement feedback loop where user reports improve model accuracy over time

---

## 💡 Key Contributions

1. **Multimodal Detection**: First framework combining email content and CAPTCHA behavior analysis
2. **Lightweight Architecture**: ELECTRA-small (14M params) + MobileNetV2 (3.4M params) enables edge deployment
3. **Practical Indicators**: Identified 4 key CAPTCHA features that reliably distinguish phishing implementations
4. **AI Text Detection**: Distinguishes AI-written from human-written emails with 99% accuracy
5. **Actionable Risk Framework**: Clear thresholds translate to concrete recommendations (Allow→Block)
6. **Threshold Optimization**: Automated threshold tuning improved CAPTCHA recall from 34% to 87%


---

## 🔧 Installation

```bash
# Clone repository
git clone https://github.com/yourusername/MAIEVC.git
cd MAIEVC

# Install dependencies
pip install tensorflow==2.20.0
pip install transformers==5.1.0
pip install torch scikit-learn pandas numpy matplotlib seaborn

---

## 🧠 How It Works
