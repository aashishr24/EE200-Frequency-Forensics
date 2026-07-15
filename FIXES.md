# Fixes applied to this project

## 1. Notch filter left residual periodic noise (`frequency_forensics.ipynb`)

**Before:** the notch filter masked out only the exact pixel of each detected
frequency spike (`mask[spikes] = 0`). In practice, a noise spike's energy
leaks into a few neighboring frequency bins (spectral leakage) rather than
sitting in a single pixel, so masking only the peak pixel left a faint
residual of the periodic pattern in the recovered image.

**Measured impact:** on the real corrupted image in `images/corrupted_image.png`,
comparing pixel counts above a fixed spike threshold outside the DC-safe
zone:

| | Spike pixels remaining |
|---|---|
| Corrupted (before any filtering) | 314 |
| Recovered, original single-pixel mask | 102 |
| Recovered, fixed (dilated mask) | 60 |

**Fix:** dilate the spike mask by a couple of pixels (`scipy.ndimage.binary_dilation`,
2 iterations) before zeroing it out, so the mask also covers each spike's
immediate spectral leakage — at the cost of masking under 1.2% of the total
spectrum, which is negligible for the legitimate low/mid-frequency image
content.

## 2. Notebooks only worked inside Google Colab

**Before:** both notebooks called `from google.colab import files` and
`files.upload()` unconditionally. Running them anywhere else (locally,
in CI, on Binder, or just opening them in plain Jupyter) crashed
immediately with `ModuleNotFoundError`.

**Fix:** wrapped the Colab upload step in a `try/except ImportError`. If
Colab isn't available, both notebooks now fall back to the bundled example
image already shipped in `images/` (`corrupted_image.png` /
`original_image.png`), so they run standalone in any environment. Colab
users see no change in behavior.

Both notebooks have been re-executed end-to-end locally (via
`jupyter nbconvert --execute`) to confirm they run cleanly with this
fallback, and the committed outputs reflect that real run.

## 3. Housekeeping

- Fixed `requirements.txt`: had Windows (`\r\n`) line endings; rewritten
  with Unix line endings, loose version floors, and added `jupyter` so the
  notebooks are actually runnable from a fresh `pip install`.
- Removed a trailing empty code cell in `missing_boundaries.ipynb`.
- Renamed files to drop assignment-part labeling (`Q1A_...` / `Q1B_...`)
  for portfolio presentation: `frequency_forensics.ipynb`,
  `missing_boundaries.ipynb`, `TECHNICAL_REPORT.pdf`, and all images in
  `images/` (e.g. `q1a_recovered_image.png` -> `recovered_image.png`).
- Fixed a stale reference in the README's repository-structure diagram
  (named a report file that no longer matched the actual committed
  filename after an earlier rename).
- Added `LICENSE` (MIT) — README referenced a license that didn't
  actually exist as a file in the repo.
