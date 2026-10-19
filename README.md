# Learning Statistically Accurate Dynamics of Complex Systems

**University of Wisconsin–Madison · MXM Spring 2026**

**Authors:** Daniel Youngberg, Tan Bui, Cody McKenna, and Singer Xing.

[Read the final report](report/final-report.pdf)

This research investigates how learned low-dimensional dynamical models can incorporate statistical observations to represent complex stochastic systems. The framework combines autoencoder representations, LSTM forecasting, and a proposed ensemble Kalman filtering (EnKF) correction stage.

## Research presented

- **Lorenz–96:** autoencoder reconstruction and latent LSTM forecasting with a representation augmented by sparse physical observations.
- **Statistical-observation extension:** a framework for coupling aggregate information, such as moments, with the learned latent representation.
- **FitzHugh–Nagumo:** forecasting experiments incorporating statistical observations, with comparisons of latent dynamics, physical variables, and spiking behavior.

**Implementation status:** Full EnKF implementation remains future work. The included figures show reconstruction and forecasting results; they do not establish completed EnKF correction results.

## Figures

![Framework overview](figures/summary_visual.png)

| Figure | View |
| --- | --- |
| Lorenz–96 autoencoder reconstruction | [Figure](figures/autoencoder-results.png) |
| Lorenz–96 LSTM forecasting | [Figure](figures/lstm-results.png) |
| FitzHugh–Nagumo latent dynamics | [Figure](figures/FHNLatent.png) |
| FitzHugh–Nagumo physical variable u | [Figure](figures/FHNuSlice.png) |
| FitzHugh–Nagumo physical variable v | [Figure](figures/FHNvSlice.png) |
| FitzHugh–Nagumo spike statistics | [Figure](figures/FHNSpikeStats.png) |

The original report and figures are preserved as exported from Overleaf. This repository contains research documents and figures; computational source code is not included. See [source and attribution](SOURCE.md) for the export record.
