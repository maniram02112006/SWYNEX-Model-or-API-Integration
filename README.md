# SWYNEX Task 2 - Model Integration: Graphic Design Style Classifier

A small Streamlit web app that integrates the trained Keras model from
[Task 1](https://github.com/maniram02112006/SWYNEX-AI-Graphic-Design-Classifier)
into a working prototype. Upload a poster or graphic design image and the app
predicts its design style.

**Internship:** SWYNEX Technologies - Task 2: Model or API Integration

## What it does

1. Accepts a JPG or PNG image (up to 10 MB).
2. Validates the file (real image, readable, at least 32 x 32 pixels).
3. Preprocesses it exactly like the Task 1 training script.
4. Loads the saved Keras model and predicts one of five styles.
5. Shows the predicted style, the model confidence, and the probability of every style.
6. Shows clear error messages for invalid files.

**Classes (same order as the Task 1 code):** cinematic, minimalist, typography, sports, vintage

## Model details (read from the Task 1 code and the saved model file)

| Item | Value |
|---|---|
| Architecture | MobileNetV2 (ImageNet weights, frozen) + GlobalAveragePooling2D + Dropout(0.2) + Dense(5, softmax) |
| Input | 160 x 160 x 3 RGB image, raw pixel values 0-255 |
| Preprocessing | MobileNetV2 scaling is built into the saved model, so the app does not divide by 255 |
| Output | 5 softmax probabilities, mapped to the class list above |
| Model file | `model/graphic_design_classifier.keras` (about 9.7 MB) |

## Project structure

```text
SWYNEX-Model-or-API-Integration/
|-- app.py                  Streamlit application
|-- requirements.txt        Python packages
|-- README.md               This file
|-- .gitignore
|-- model/
|   `-- graphic_design_classifier.keras   Trained model from Task 1
`-- examples/
    |-- cinematic_01.jpg, minimalist_02.jpg, typography_01.jpg, vintage_01.jpg
    `-- example_outputs.md  Example inputs and the outputs the app produced
```

## How to run (Windows, VS Code terminal)

```powershell
python -m venv venv
venv\Scripts\activate
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

Your browser opens at `http://localhost:8501`. If PowerShell blocks the
activate script, run `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`
once and try again. If `pip install` cannot find TensorFlow, your Python
version is probably too new for it; install Python 3.11 or 3.12 from python.org and repeat the steps.

## Example inputs and outputs

See [`examples/example_outputs.md`](examples/example_outputs.md). Try the four
images in the `examples/` folder.

## Limitations (please read)

- The Task 1 model was trained on **20 AI-generated illustrative sample images
  (4 per class)**. The dataset's own README says this is not enough for reliable
  training or an honest performance evaluation.
- **No accuracy figure is reported here**, because no proper held-out evaluation exists.
- The example images are from that same sample set, so correct predictions on
  them do **not** show how the model performs on new designs.
- The confidence is a softmax score. It is not a calibrated probability and can
  be high for wrong answers.
- The model always chooses one of the five styles, even for images that are not
  posters or that mix styles.

## Future improvements

- Collect a larger, properly licensed and labelled dataset and evaluate on a held-out test set.
- Add data augmentation and fine-tuning.
- Add an "uncertain / not a poster" option.

## Security

No API keys, passwords, or tokens are used or stored in this project. The model
runs locally.
