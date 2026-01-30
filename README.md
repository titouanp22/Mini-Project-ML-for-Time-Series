# BIRD — Multi-scale Time–Frequency Denoising

**Authors**: Maxime Muhlethaler, Titouan Pottier

## Overview
This project implements **BIRD** and **S-BIRD**, two greedy denoising algorithms for time-series signals based on a **multi-scale MDCT time–frequency representation**.  
The methods are evaluated on **neurophysiological (MEG) signals** with added noise.

---

## Key Idea
The signal is reconstructed using a **sparse approximation** over a **multi-scale MDCT dictionary**:

- Several MDCT window sizes are used to capture structures at different time scales.
- At each iteration, the most relevant atom is greedily selected.
- A **theoretical stopping criterion** allows denoising **without knowing the noise level**.

- **BIRD**: mono-channel version  
- **S-BIRD**: structured multi-channel extension exploiting inter-channel coherence

---

## Method

### Multi-scale MDCT Representation
- 50% overlapping frames
- Multiple window sizes
- Implicit normalized MDCT dictionary

### BIRD Algorithm
Iterative procedure:
1. MDCT analysis of the residual (all scales)
2. Selection of the maximum coefficient
3. Reconstruction of the corresponding atom
4. Residual update
5. Automatic stopping using a theoretical threshold

Multiple random runs are averaged to improve stability.

### S-BIRD (Multi-channel)
- MDCT analysis per channel
- Structured atom selection across channels
- Joint stopping criterion
- `p_active` controls the number of active channels

---

## Baselines
BIRD and S-BIRD are compared with standard denoising baselines using:
- Mean Squared Error (MSE)
- Time-domain reconstruction quality
- Visual inspection of signal peaks

---

## Experiments

### Data
- Real **MEG data** (Somato dataset, MNE)
- 10 neighboring gradiometers
- 1-second temporal window
- Band-pass filtering: 1–40 Hz
- Additive Gaussian noise (SNR = 5 dB)

### Evaluation
- Baselines vs BIRD vs S-BIRD
- Influence of `p_active`
- Time-domain plots and zoom on signal events

---

## Results
- **BIRD** performs effective denoising without explicit noise estimation
- **S-BIRD** significantly improves performance by leveraging spatial structure
- Particularly suited for structured, noisy neurophysiological signals

---

## Dependencies
- Python ≥ 3.9
- NumPy
- SciPy
- Matplotlib
- MNE

---

## Usage
Run the main notebook:
```bash
jupyter notebook ml_for_ts.ipynb
