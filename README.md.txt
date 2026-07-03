# EE200 Project: Frequency Forensics & Missing Boundaries

## Project Overview

This project was completed as part of the EE200 (Signals, Systems & Networks) course. It contains two image processing tasks:

### Q1A – Frequency Forensics (The Ghost Signal)

- Loaded a corrupted grayscale image.
- Applied the 2D Fourier Transform (FFT).
- Visualized the frequency spectrum in linear and logarithmic (dB) scales.
- Designed a notch filter to remove periodic noise.
- Reconstructed the image using the Inverse Fourier Transform (IFFT).

### Q1B – Missing Boundaries

- Applied Sobel edge detection.
- Detected object boundaries using image gradients.
- Analyzed the effect of noise on edge detection.

## Technologies Used

- Python
- NumPy
- OpenCV
- Matplotlib

## Repository Structure

```
EE200-Frequency-Forensics
│
├── images/
│   └── results_overview.png
├── Q1A_Frequency_Forensics.ipynb
├── Q1B_Missing_Boundaries.ipynb
├── report.pdf
├── README.md
└── requirements.txt
```

## Results

The figure below shows the complete processing pipeline for the frequency-domain restoration task.

![Project Results](images/results_overview.png)

## Files

- **Q1A_Frequency_Forensics.ipynb** – Frequency-domain image restoration.
- **Q1B_Missing_Boundaries.ipynb** – Sobel edge detection.
- **report.pdf** – Project report.