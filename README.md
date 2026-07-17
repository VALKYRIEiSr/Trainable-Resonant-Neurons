# Trainable Resonant Neurons (TRNs) for Analog Neural Networks
**Differentiable Frontend Architecture for Edge Hardware**

## Project Overview
An end-to-end differentiable framework implementing Trainable Resonant Neurons (TRNs)--a novel alternative to standard fixed filter banks in Analog Neural Networks (ANNs). This architecture combines parameterized bandpass filters with an envelope detector stage to enable direct optimization of physical circuit features like center frequency (f0) and quality factor (Q) directly from raw signal data.

Traditional analog front-ends rely on a Fixed Filter Bank (FFB) spread statically across a spectrum. A TRN replaces this rigid structure with a completely differentiable signal pipeline:

Input Signal -> [ MFB Filter Stage ] -> [ Full-Wave Rectifier ] -> [ RC Envelope Smoothing ] -> Scalar Feature
                    (Learns f0, Q)                                        

## Technical Research
The underlying mathematical foundations, circuit stages, and benchmark results are fully detailed in the included research document:
* **Research Paper:** `Trainable Resonant Neurons.pdf`

## Technical Specifications
* **Filter Stage:** Uses a Multiple Feedback (MFB) topology to adaptively tune the frequency response entirely in the circuit domain without inductor elements.
* **Rectifier Stage:** Converts the AC output of the filter step into a unipolar signal via full-wave rectification.
* **Envelope Stage:** Implements an RC smoothing circuit to extract stable amplitude envelopes, regulated by a parameterised responsivity-stability (rho, kappa) trade-off.
* **Hardware Simulation:** To make the hardware simulation viable inside deep learning loops, the non-linear absolute values are smoothed via a square-root approximation.

## Repository Structure
* `Trainable Resonant Neurons.pdf`: The underlying research paper detailing the mathematical foundations, circuit stages, and benchmark results.
* `Training_data.ipynb`: Handles the synthetic generation of controlled, multi-tone audio signal datasets used to rigorously test the models (dataset 2).
* `NN.ipynb`: Implements the end-to-end machine learning pipeline, modeling simplified mathematical forms of the circuit responses to minimize computational overhead during neural network training.

## Key Experimental Benchmarks

### Task 1: Linear Spectral Separation (Dataset 1)
* **Condition:** Clean multi-tone inputs evenly spaced across a 500-5,000 Hz band.
* **Result:** Both architectures converged smoothly, approaching a peak classification performance of ~95% Accuracy. Static configurations suffice when boundary conditions are simple.

### Task 2: High Noise and Irregular Spacing (Dataset 2)
* **Condition:** Complex multi-tone signals corrupted by White Gaussian Noise (sigma = 2.0) and subtle, power-invariant frequency shifts.
* **Performance Gap:**
    * Fixed Filter Bank (FFB): Peaked at 78.45% Accuracy.
    * Trainable Resonant Neuron (TRN): Reached 84.69% Accuracy.

*Note: As detailed in the paper, this absolute performance margin of ~6% acts as a lower bound under controlled parameters; the advantage scales dramatically when handling richer, real-world non-stationary data.*

## Usage Summary
1. **Data Generation:** Run `Training_data.ipynb` to construct the perturbed positive and negative signal waveforms.
2. **Model Optimization and Metrics:** Run `NN.ipynb` to execute the neural network pipeline on the generated training datasets and output performance metrics.
