# 🚀 Objectif du projet
Développer un démonstrateur “AI Catalog Compliance” :

- **Couche “Conformité”** pour détecter sur images et sur textes marketing tout ce qui pourrait contrevenir à la Loi Evin
- **Deux briques ML** :
  1. **Object Detection** (reconnaître bouteilles, étiquettes prohibées)
  2. **NLP Classification** (analyser le contenu textuel d’une campagne)

Vous couvrirez : ingestions, EDA, feature engineering, modélisation, pipeline MLOps léger, monitoring, documentation, tout en appliquant les bonnes pratiques de dev Python et en anticipant un futur déploiement GCP (Cloud Run / Vertex AI).

---

## 📅 Planning détaillé sur 5 jours ouvrés (+ 2 jours de buffer)

| Jour   | Tâches clés                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|:------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Jour 1 | - **Init repo & env** :<br>  • `git init` + venv Python<br>  • `requirements.txt` (pandas, numpy, scikit-learn, torch, torchvision, transformers, mlflow, fastapi, uvicorn…)<br>  • `.gitignore`<br><br>- **Jeu de données** :<br>  • Rassembler un petit dataset d’images de bouteilles d’alcool (open-source)<br>  • Simuler 100 descriptions marketing (fictives) avec 50 % “compliantes” et 50 % “non-compliantes” |
| Jour 2 | - **Ingestion & EDA** (`src/ingestion.py`) :<br>  • Scripts pour lire images et CSV textes<br>  • Nettoyage basique (formats, doublons)<br>  • Notebook rapide pour explorer : tailles images, longueur textes, classes                                                                                                                                                |
| Jour 3 | - **Modélisation Image** (`src/image_model.py`) :<br>  • Utiliser un modèle pré-entraîné (YOLOv5 ou torchvision Faster R-CNN)<br>  • Fine-tuning sur vos 100 images annotées (label `bottles` vs `no_bottle`)<br>  • Metrics : mAP, precision/recall pour détection d’étiquettes interdites                                             |
| Jour 4 | - **Modélisation Texte** (`src/text_model.py`) :<br>  • Transformer (DistilBERT) pour classifier “compliant” vs “non-compliant”<br>  • Pipeline tokenization → training → évaluation (accuracy, F1)<br><br>- **Feature Engineering** :<br>  • Pour images (taille boîte englobante, ratio)<br>  • Pour textes (longueur, count de mots-clés réglementaires)     |
| Jour 5 | - **Pipeline & MLOps léger** (`src/pipeline.py`) :<br>  • Orchestration séquentielle : ingestion → prédiction image → prédiction texte → rapport JSON<br>  • Enregistrement d’expériences avec MLflow (metrics + paramètres)<br><br>- **Prototype d’API** (`src/app.py`) :<br>  • FastAPI exposant deux endpoints `/predict_image` et `/predict_text`<br><br>- **Monitoring** :<br>  • Script de sanity checks (vérifier que mAP et F1 > seuil de 0.75) |
| Jour 6 | - **Documentation** :<br>  • `README.md` détaillant l’installation, l’exécution et la structure du projet<br>  • Diagramme du pipeline (PNG dans `docs/`)<br><br>- **Tests unitaires** (`tests/test_*.py`) pour chaque module (ingestion, modèles, pipeline)                                                                                                  |
| Jour 7 | - **Packaging & livraison** :<br>  • Générer `requirements.txt` final (`pip freeze > requirements.txt`)<br>  • Dockerfile simple (base `python:3.10`) pour embarquer l’API<br>  • Commit & push sur GitHub (branche `main`)<br><br>- Buffer & correctifs selon retours personnels                                                                                 |

---

## ⚙️ Structure Git finale

```bash
criteo-mh-ais-catalog/
├── data/
│   ├── raw/                 # images brutes + CSV textes
│   └── processed/           # after cleaning
├── docs/
│   └── pipeline_diagram.png
├── src/
│   ├── ingestion.py         # ingestion + EDA
│   ├── image_model.py       # détection modèle + metrics
│   ├── text_model.py        # classification texte + metrics
│   ├── pipeline.py          # orchestration MLflow
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
