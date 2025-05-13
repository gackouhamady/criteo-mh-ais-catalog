# 🚀 Project Objective

Develop an “AI Catalog Compliance” demonstrator:

* **Compliance layer** to detect, in images and marketing texts, anything that could breach France’s Loi Evin
* **Two ML components**:

  1. **Object Detection** (identify bottles, prohibited labels)
  2. **NLP Classification** (analyze the textual content of a campaign)

You will cover: ingestion, EDA, feature engineering, modeling, lightweight MLOps pipeline, monitoring, documentation—applying Python best practices and planning for a future GCP deployment (Cloud Run / Vertex AI).

---

## 📅 Detailed 5-day working plan (+ 2 days buffer)

|                                                       Day                                                       | Key tasks              |
| :-------------------------------------------------------------------------------------------------------------: | :--------------------- |
|                                                    **Day 1**                                                    | - **Init repo & env**: |
|                                            • `git init` + Python venv                                           |                        |
| • `requirements.txt` (pandas, numpy, scikit-learn, torch, torchvision, transformers, mlflow, fastapi, uvicorn…) |                        |
|                                                  • `.gitignore`                                                 |                        |

* **Dataset**:
  • Gather a small open-source dataset of alcohol bottle images
  • Simulate 100 marketing descriptions (fictitious), 50% “compliant” and 50% “non-compliant” |
  \| **Day 2** | - **Ingestion & EDA** (`src/ingestion.py`):
  • Scripts to read images and text CSVs
  • Basic cleaning (formats, duplicates)
  • Quick notebook to explore: image sizes, text lengths, classes |                                                                                                                                                                                                                                                                                   |
  \| **Day 3** | - **Image modeling** (`src/image_model.py`):
  • Use a pre-trained model (YOLOv5 or torchvision Faster R-CNN)
  • Fine-tune on your 100 annotated images (labels: `bottle` vs `no_bottle`)
  • Metrics: mAP, precision/recall for prohibited-label detection |
  \| **Day 4** | - **Text modeling** (`src/text_model.py`):
  • Transformer (DistilBERT) to classify “compliant” vs “non-compliant”
  • Pipeline: tokenization → training → evaluation (accuracy, F1)

* **Feature engineering**:
  • For images (bounding-box size, aspect ratio)
  • For texts (length, count of regulatory keywords) |
  \| **Day 5** | - **Pipeline & lightweight MLOps** (`src/pipeline.py`):
  • Sequential orchestration: ingestion → image prediction → text prediction → JSON report
  • Log experiments with MLflow (metrics + parameters)

* **API prototype** (`src/app.py`):
  • FastAPI exposing `/predict_image` and `/predict_text` endpoints

* **Monitoring**:
  • Sanity-check script (verify mAP and F1 > 0.75) |
  \| **Day 6** | - **Documentation**:
  • `README.md` detailing installation, execution, and project structure
  • Pipeline diagram (PNG in `docs/`)

* **Unit tests** (`tests/test_*.py`) for each module (ingestion, models, pipeline) |
  \| **Day 7** | - **Packaging & delivery**:
  • Generate final `requirements.txt` (`pip freeze > requirements.txt`)
  • Simple Dockerfile (base `python:3.10`) to package the API
  • Commit & push to GitHub (`main` branch)

* Buffer & refinements based on personal feedback |

---

## ⚙️ Final Git Structure

```bash
criteo-mh-ais-catalog/
├── data/
│   ├── raw/                 # raw images + text CSVs
│   └── processed/           # after cleaning
├── docs/
│   └── pipeline_diagram.png
├── src/
│   ├── ingestion.py         # ingestion + EDA
│   ├── image_model.py       # detection model + metrics
│   ├── text_model.py        # text classification + metrics
│   ├── pipeline.py          # orchestration + MLflow
│   └── app.py               # FastAPI endpoints
├── tests/
│   ├── test_ingestion.py
│   ├── test_image_model.py
│   ├── test_text_model.py
│   └── test_pipeline.py
├── Dockerfile
├── README.md
├── requirements.txt
└── .gitignore
```
