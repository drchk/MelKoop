# MelKoop: Real-Time Speech Enhancement via Parsimonious Koopman Embeddings

This repository page summarizes the current MelKoop model used in the manuscript. The main training code is not released in this repository yet. This page is intended to provide transparent model-size, computational-cost, and benchmark-positioning information.

## Model summary

MelKoop is a compact causal speech-enhancement front end operating in the complex STFT domain. It combines:

- a lightweight subband encoder,
- GraphFreq message passing over compressed frequency bands,
- a hybrid FIR--Koopman temporal core,
- a small Mel-envelope correction branch,
- and a complex-mask decoder.

## Complexity summary

The model-complexity report was generated with `ptflops` using input shape `[1, 257, 63, 2]`, corresponding to approximately one second of 16 kHz audio with `NFFT=512` and hop length `256`.

| Quantity | Value |
|---|---:|
| Trainable parameters | **23,371** |
| Trainable parameters | **23.37 K** |
| Trainable parameters | **0.023371 M** |
| Counted MACs | **41.78 MMAC/s** |
| Counted MACs | **0.041784 GMAC/s** |
| All parameters, including frozen Mel projection matrices | 25.42 K |

**Counting note.** MACs are counted for recognized PyTorch modules such as `Conv1d`, `ConvTranspose1d`, `Linear`, normalization, activation, and related modules under the `ptflops` convention. STFT/iSTFT, some elementwise operations, custom tensor operations, and some graph/batched-matrix operations may not be fully counted. Therefore, the number should be read as a module-level counted MAC estimate rather than a hardware latency measurement.

## Component-level size overview

| Component | Modules | Parameters | Counted MACs |
|---|---|---:|---:|
| Encoder input conv + subband encoder | conv1, conv2, conv3, conv1x1 | ~7.25K | ~15.26MMAC |
| Temporal TDCN++ core | temporal | ~3.34K | ~2.94MMAC |
| GraphFreq message passing | graphfreq | ~1.30K trainable including adjacency/gate | ~0.56MMAC counted |
| Mel-envelope Koopman branch | melkoop | ~2.11K trainable | ~0.26MMAC counted |
| FIR--Koopman hybrid time-core | time_core | ~1.07K trainable | ~2.16MMAC counted |
| Post S4-like depthwise/pointwise block | s4_post | 272 params + gate | ~0.55MMAC counted |
| Decoder | deconv1, deconv2, deconv3 | ~6.30K | ~15.39MMAC |

The full layer-by-layer parameter and MAC report is available here:

[`reports/melkoop_full_layer_param_mac_report.txt`](reports/melkoop_full_layer_param_mac_report.txt)

## VoiceBank+DEMAND comparison

Published objective results on the standard VoiceBank+DEMAND test set. `--` denotes that the source does not report the value. This table is used for quality--efficiency positioning rather than as a fully controlled loss-matched comparison, because training data, objective functions, causality/look-ahead, and reporting conventions differ across papers.

| Model | Year | Params [M] | MACs [G] | Causal | PESQ | CSIG | CBAK | COVL | STOI |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Noisy | -- | -- | -- | -- | 1.97 | 3.34 | 2.44 | 2.63 | 0.921 |
| FullSubNet+ | 2021 | 8.67 | 30.06 | Not specified | 2.88 | 3.86 | 3.42 | 3.57 | 0.940 |
| MP-SENet | 2023 | 2.05 | -- | Not specified | 3.50 | 4.73 | 3.95 | 4.22 | 0.960 |
| Spiking-S4 | 2024 | 0.53 | 0.75 | No | 3.39 | 4.92 | 2.64 | 4.31 | -- |
| SEMamba | 2024 | 2.25 | -- | No | 3.55 | 4.77 | 3.95 | 4.29 | 0.960 |
| Mamba-SEUNet | 2025 | 6.28 | 9.085 | No | 3.59 | 4.80 | 4.02 | 4.32 | 0.960 |
| xLSTM-SENet | 2025 | 2.20 | -- | No | 3.48 | 4.74 | 3.93 | 4.22 | 0.960 |
| RNNoise | 2018 | 0.06 | 0.04 | Yes | 2.33 | 3.40 | 2.51 | 2.84 | 0.922 |
| DCCRN | 2020 | 3.70 | 14.36 | Not specified | 2.54 | 3.74 | 3.13 | 2.75 | 0.938 |
| FRCRN | 2022 | 10.27 | 12.30 | Yes | 3.21 | 4.23 | 3.64 | 3.73 | 0.942 |
| DeepFilterNet2 | 2022 | 2.31 | 0.36 | Yes | 3.08 | 4.30 | 3.40 | 3.70 | 0.943 |
| Dual-S4D | 2024 | 10.8 | 18.43 | Not specified | 2.55 | 3.94 | 3.00 | 3.23 | 0.934 |
| CCFNet+ | 2023 | 0.62 | 1.47 | Yes | 3.03 | 4.27 | 3.55 | 3.61 | 0.950 |
| FSPEN | 2024 | 0.079 | 0.089 | Yes | 2.97 | -- | -- | -- | 0.942 |
| CAGCRN | 2025 | 0.07 | 0.06 | Yes | 2.86 | -- | -- | -- | 0.939 |
| AFAGC-GinNet | 2025 | 1.32 | 1.03 | Yes | 3.25 | 4.35 | 3.62 | 3.75 | 0.955 |
| LiSenNet | 2025 | 0.037 | 0.06 | Yes | 3.07 | -- | -- | -- | 0.939 |
| ****MelKoop**** | **2026** | **0.023** | **0.041** | **Yes** | **3.56** | **4.17** | **3.22** | **3.80** | **0.936** |

**Note.** Causality/look-ahead labels are source-grounded: `Yes` or `No` is used only when the source makes this clear; otherwise the entry is marked `Not specified`. Metric precision follows the source-reported values for external baselines; MelKoop point estimates are rounded to the same display convention. Since confidence intervals and metric-aware training losses are not consistently reported for external baselines, small cross-paper score differences should not be read as formal significance claims. Component-level conclusions are based on the internal ablation and temporal-core comparison reported in the manuscript.

## Code release status

The main training and inference code is not included in this repository at this stage. Code, model configuration files, inference/evaluation scripts, and representative audio examples are planned for public release after acceptance, subject to dataset and third-party licensing constraints.
