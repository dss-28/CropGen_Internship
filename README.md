
# AI Crop Disease Predictor (Hierarchical Pipeline)

**Solo internship project at CropGen** — predicting plant diseases across **100+ crops and 663 diseases (~6,000+ disease–crop pairs)** using a **hierarchical EfficientNet pipeline**.

---

## 📝 Project Overview

This project tackles **real-world agricultural data** to build an AI system that can:

1. Identify the **crop type** from an image
2. Predict **disease affecting the crop**

**Why hierarchical?**
The dataset is large and multi-class — a single flat classifier would struggle with **100+ crops × hundreds of diseases**, so we split the problem:

**Crop Identification → Disease Classification**

This hierarchy is **necessary due to the scale of the data**.

---

## 📊 Dataset

The dataset contains images from:

* **Founder-provided images**
* Images **scraped online**
* Manually **collected images**

**Data cleaning steps:**

* Manual review of mislabeled images
* **Hash-based duplicate removal**
* Organized into **crop → disease directories**

**Example CSV format (sample):**

| Crop     | Disease        | Image Filename          |
| -------- | -------------- | ----------------------- |
| Tomato   | Late Blight    | tomato_lb_001.jpg       |
| Cotton   | Bacterial Spot | cotton_bs_010.jpg       |
| Cucumber | Beetle         | cucumber_beetle_001.jpg |
| Tobacco  | Mosaic Virus   | tobacco_mv_003.jpg      |

---

## 🛠 Model Architecture

### Hierarchical Pipeline

**Broad view (10 crops × 10 diseases per crop):**

```text
                   Input Image
                        │
                        ▼
             ┌────────────────────┐
             │   Crop Classifier   │
             │   (EfficientNet)    │
             └────────────────────┘
                        │
         ┌───────┬───────┬───────┬───────┬───────┐
         ▼       ▼       ▼       ▼       ▼       ▼
      Crop1    Crop2   Crop3   Crop4   Crop5   Crop6 ... Crop10
         │       │       │       │       │       │
   ┌──────┴──────┴──────┴──────┴──────┴──────┐
   ▼      ▼      ▼      ▼      ▼      ▼      ▼ ... ▼
 D1     D2     D3     D4     D5     D6     D7 ... D10
```

**Explanation:**

* **Stage 1 – Crop Classifier:** Identifies which crop the image belongs to (~90% accuracy).
* **Stage 2 – Disease Classifier:** For each crop, a **specific classifier predicts one of 10 diseases** (~70–80% accuracy).

---

## 🎨 Data Augmentation

Applied **standard augmentation** to improve robustness:

* Random flips and rotations
* Color jitter / brightness adjustments
* Careful **train-validation splits** to prevent leakage

---

## ⚡ Key Takeaways

* Real-world AI is messy — **data cleaning is critical**
* Hierarchical models help manage **large multi-class problems**
* Augmentation and proper splits can significantly boost performance

---

## 🔜 Next Steps

The system is **yet to be deployed**. Due to its **hierarchical design**, deployment requires:

* Careful system architecture
* Scalable inference pipeline
* Integration for real-world usage

---

## 📂 Project Structure

```text
AI-Crop-Disease-Predictor/
│
├── data/
│   ├── crop1/
│   │   ├── disease1/
│   │   │   ├── img001.jpg
│   │   │   └── ...
│   │   └── disease2/
│   └── ...
│
├── notebooks/
│   ├── EDA.ipynb
│   └── model_training.ipynb
│
├── models/
│   ├── crop_classifier.pth
│   └── disease_classifier/
│
│
├── README.md
└── requirements.txt
```
Note:This is project structure not repository structure
---

## 📈 Results

* **Crop classifier accuracy:** ~90%
* **Disease classifier accuracy:** ~70–80% (100-class prototype)

---

## 💬 Discussion / Collaboration

I built this **solo during my AI internship at CropGen**. If you are exploring **AI for agriculture**, **multi-class classification**, or **hierarchical pipelines**, I’d love to discuss ideas or potential collaborations!

---

## ⚡ License

*Personal / educational use — company data not shared publicly.*

---
