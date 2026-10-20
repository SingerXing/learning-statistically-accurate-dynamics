# Methods walkthrough

*A reader’s guide adapted from the MXM Overleaf materials, without computational source code. This is an explanatory companion, not a verbatim copy of the original walkthrough or a record of independently reproduced experiments.*

**Project:** Learning Statistically Accurate Dynamics of Complex Systems, UW–Madison MXM Spring 2026.  
**Final-report authors:** Daniel Youngberg, Tan Bui, Cody McKenna, and Singer Xing.

## The question behind the method

A complex system may contain many interacting variables, but useful observations may summarize their collective behavior: an average, a correlation, or the fraction exceeding a threshold. Many different system states can share these summaries. The project asks how statistical observations can inform a compact learned dynamical model while retaining a connection to the full physical state.

The proposed cycle has three roles: an **autoencoder** compresses and reconstructs the state; an **LSTM** predicts its evolution in the compact representation; an **ensemble Kalman filter (EnKF)** would correct forecasts using observations. The materials contain reconstruction and forecasting results. Full EnKF implementation is explicitly future work in the poster.

The final report identifies Behnoudfar and collaborators’ model-bridging research as prior work. The team’s Lorenz–96 implementation uses related building blocks as a starting point. The extension concerns statistical observations and their connection to learned coordinates; it is not the invention of autoencoders or LSTMs.

## 1. Establish a Lorenz–96 reconstruction and forecasting workflow

**Generate and prepare data.** Stochastic Lorenz–96 represents a periodic lattice of 40 interacting values. Euler–Maruyama simulation advances the state in small time steps, combining the deterministic change with a random increment. The walkthrough standardizes each coordinate over time, then applies a global rescaling. This puts variables on comparable numerical scales without normalizing every snapshot independently.

**Compress the state.** A one-dimensional convolutional encoder processes nearby lattice values together. Circular padding respects the periodic boundary. Three stride-two blocks reduce the spatial grid from 40 to 20 to 10 to 5; a fully connected projection produces eight learned coordinates, denoted $z=E(x)$.

**Append five selected physical values.** The baseline extracts zero-based state indices `[1, 5, 10, 15, 35]`. These values form $o\in\mathbb{R}^5$, and the decoder receives the combined representation

$$
a=[z;o]\in\mathbb{R}^{13},\qquad \hat{x}=D(a)\in\mathbb{R}^{40}.
$$

The eight encoder outputs are learned features, not eight predefined statistics. The five appended values are individual state components. The decoder reconstructs all 40 variables in their original coordinate order, including variables not directly appended. Those variables still contribute to the encoder input.

**Train for reconstruction and coupling.** Reconstruction loss compares the full decoded state with the original input. A correlation regularizer encourages dependence between the eight learned coordinates and the five appended observations. The intended purpose is to let a later filter transfer information from observed coordinates into learned ones. Such training does not by itself demonstrate a successful assimilation update.

**Forecast in the reduced representation.** After autoencoder training, the fixed encoder produces eight learned coordinates per snapshot; appending the same five observed values produces a 13-dimensional augmented time series. The documented LSTM uses three previous states to predict the next, with two recurrent layers and hidden dimension 32. Predicted states can be decoded for comparison in physical space. Repeatedly feeding forecasts into the next input produces an autoregressive rollout, a more demanding task than a single prediction from a known history.

## 2. Replace individual values with statistical observations

The extension introduces an observation operator $\mathcal M$: a rule that converts a full state into a smaller collection of summaries. During simulated training, these summaries can be computed directly from the reference trajectory. They are distinct from both the learned coordinates and the cross-correlation regularizer.

The Lorenz–96 examples have different observation dimensions:

| Observation | What it contains | Observation dimension |
| --- | --- | --- |
| Baseline pointwise values | Five individual state components | 5 |
| Spatial block averages | Five averages, each over eight adjacent values | 5 |
| Leading Fourier coefficients | Real and imaginary parts of modes 1, 2, and 3 | 6 |

Block averages retain coarse regional information. Fourier coefficients describe large-scale spatial patterns; these six numbers are not six moments of the same type. The walkthrough also discusses means, variances, higher moments, energy-related summaries, and spatial correlations as possible operators.

These instantaneous spatial summaries should not be confused with averages over many independent trajectories or long time windows. The operator determines what “statistical observation” means in each experiment. Temporal or lagged statistics require a history, not just one snapshot.

## 3. Two ways to connect statistics to the latent state

### Statistical augmentation

The first approach replaces the five pointwise values with $m=\mathcal M(x)$ and retains the augmented construction $a=[E(x);m]$. Reconstruction and correlation-based training aim to preserve physical information and couple the learned coordinates to the statistical ones.

With eight learned coordinates, five block averages give a **13-dimensional** representation; six Fourier values would give **14 dimensions**. In the proposed filter, a selector reads the appended statistical coordinates. Forecast cross-covariance would determine how their correction affects the learned coordinates.

### A learned observation map

The second approach keeps only $z=E(x)$ as the reduced state and trains an auxiliary network $h$ to predict statistics. Its intended relationship is

$$
h(z)\approx\mathcal M(D(z)).
$$

The walkthrough separates three objectives: reconstruct the physical state, preserve its target statistics after decoding, and make $h(z)$ agree with the statistics of that decoded state. This decoder consistency matters: predicting the right statistics from $z$ alone would not guarantee that the reconstructed physical field has those statistics.

The reduced state can remain eight-dimensional, but the observation map is now nonlinear. The report says alternatives were tested; the included figures do not provide a separate quantitative comparison demonstrating which approach performs better.

## 4. What the FitzHugh–Nagumo results add

FitzHugh–Nagumo uses two fields, a fast activator $u$ and a slower recovery variable $v$, to represent excitable dynamics and spiking. With 40 sites per field, the physical state has 80 values. The poster describes an eight-dimensional encoder representation augmented by **four statistical observations** for LSTM training.

The final report includes latent forecasts, decoded $u$ and $v$ time series, and a comparison of the fraction of sites above a spike threshold. These are evidence of forecasting work involving statistical observations beyond the Lorenz–96 pointwise baseline. They are not evidence of completed EnKF corrections or a proven improvement in the invariant distribution.

## 5. Proposed correction stage

The proposed EnKF would maintain several possible reduced states, forecast each with the LSTM, and compare predicted observations with available observations. An update based on ensemble cross-covariance would adjust each forecast before decoding and continuing the cycle. Statistical augmentation uses a coordinate selector; the second approach uses the nonlinear map $h$.

The walkthrough supplies formulas and implementation sketches for this stage. These sketches do not establish that the complete cycle was executed or that filtering improved the results.

## Evidence and source notes

The poster explicitly lists full EnKF implementation as a next step. The repository therefore distinguishes **reported reconstruction/forecasting results**, **extension designs**, and **future filtering work**. The observation dimensions above describe specific configurations; neither five nor six is a fixed dimension of the overall framework.

Some source details remain inconsistent. The walkthrough’s Lorenz–96 example uses forcing 5 while the report states 8. Its correlation-loss equation and displayed training calculation are different objectives. The report and poster both describe four FHN statistical inputs but differ on their exact composition. This guide does not resolve those differences by guessing; exact experimental settings require confirmation from the corresponding experiment record.

## Sources

- `Lorenz_Autoencoder_Walkthrough.tex`: “Data Generation,” “The CNN Autoencoder,” “Training the Autoencoder,” “The Latent Dynamics LSTM,” “Extending the Framework to Moment-Based Observations,” and “Latent-Space EnKF with Moment Observations.”
- `main.tex`: “Previous Work,” “Motivation of Extension,” “Methodology,” “Results,” and “Discussion”; available as the [final report](../report/final-report.pdf).
- `Poster/main_poster.tex`: “Discussion” and “Conclusion and Future Work,” used to distinguish reported forecasts from planned assimilation; available as the [research poster](../poster/research-poster.pdf).

Original project materials remain unchanged. This guide summarizes the team’s documentation and does not assign individual ownership of the walkthrough or of particular experiments.
