This repository is an end-to-end TensorFlow image classification project (CIFAR-10 by default).


Features:
- tf.data-based pipelines
- Transfer learning (MobileNetV2)
- Training, evaluation, export to SavedModel and TFLite
- FastAPI inference service
- Dockerfile and GitHub Actions CI (smoke test)


## Quickstart


1. Create venv and install

python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt


2. Run smoke training (1 epoch)

python src/train.py --epochs 1 --batch-size 32


3. Run inference server

python src/export.py --model-dir experiments/latest/saved_model
uvicorn app.api:app --port 8000


4. Predict

curl -X POST "http://localhost:8000/predict" -F "image=@test.jpg"

Docker
Build and run:

docker build -t tf-image-classifier .
docker run -p 8000:8000 tf-image-classifier


Tests
pytest -q


Files
src/: core code
app/: FastAPI server
docker/: Dockerfile
ci/: GitHub Actions


License: MIT
---
## requirements.txt


tensorflow>=2.12.0 numpy pillow fastapi uvicorn[standard] scikit-learn pytest
---
## .gitignore


pycache/ .venv/ .experiments/ experiments/ *.pyc *.pkl *.h5 .env
---
## src/configs.py
```python
from dataclasses import dataclass

