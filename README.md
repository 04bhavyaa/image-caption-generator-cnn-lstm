# Image Caption Generator (CNN + LSTM)

Small demo and training notebooks for generating captions on Flickr8k images using a CNN feature extractor + LSTM caption model.

## Quickstart (developer)

1. Create and activate a virtual environment (PowerShell):

```powershell
python -m venv .venv;
.\.venv\Scripts\Activate.ps1
```

2. Install the minimal runtime dependencies:

```powershell
python -m pip install --upgrade pip;
pip install -r requirements.txt
```

3. Place trained model artifacts in a `models/` directory at repo root:

```
models/
  ├─ model.keras                 # trained LSTM caption model
  ├─ feature_extractor.keras     # CNN feature extractor
  └─ tokenizer.pkl               # pickled Keras Tokenizer
```

4. Run the Streamlit demo:

```powershell
streamlit run main.py
```

Open the UI in the browser, upload an image and the demo will generate a caption using the saved models.

## Training / Preprocessing

- See `flickr8k-image-captioning-using-cnns-lstms.ipynb` for data cleaning, tokenizer creation, feature extraction, and model training. The notebooks are the authoritative source for reproducing `models/` and items stored under `processed/`.

## Important runtime notes

- `main.py` expects `models/model.keras`, `models/feature_extractor.keras`, and `models/tokenizer.pkl`.
- Default inference parameters: `max_length=34`, `img_size=224`, uses `startseq`/`endseq` tokens.
- Images are normalized by dividing pixel values by `255.0` before feature extraction.
- Tokenizer is loaded via `pickle` — do not load pickles from untrusted sources.

## Recommended improvements (next steps)

- Add a pinned `requirements.txt` (done) and document the exact TensorFlow version used to train the models.
- Add a smoke-test script to validate model loading and inference for CI.
- Consider storing models externally (cloud storage) and providing a download script rather than checking large binaries into the repo.

## Troubleshooting

- If `load_model` fails: verify your installed TensorFlow version matches the version used to save the models.
- If generation stops early or returns empty: check that `tokenizer.index_word` contains expected indices and that `startseq`/`endseq` tokens were used at training time.

## License / Data

- This repo uses the Flickr8k dataset; verify you comply with its license when sharing trained artifacts.
