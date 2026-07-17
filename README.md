# Trainable Resonant Neurons (TRNs) for Analog Neural Networks
**Differentiable Frontend Architecture for Edge Hardware**[cite: 1]

## Project Overview
An end-to-end differentiable framework implementing Trainable Resonant Neurons (TRNs)--a novel alternative to standard fixed filter banks in Analog Neural Networks (ANNs)[cite: 1]. This architecture combines parameterized bandpass filters with an envelope detector stage to enable direct optimization of physical circuit features like center frequency (f0) and quality factor (Q) directly from raw signal data[cite: 1].

Traditional analog front-ends rely on a Fixed Filter Bank (FFB) spread statically across a spectrum[cite: 1]. A TRN replaces this rigid structure with a completely differentiable signal pipeline[cite: 1]:

Input Signal -> [ MFB Filter Stage ] -> [ Full-Wave Rectifier ] -> [ RC Envelope Smoothing ] -> Scalar Feature
                    (Learns f0, Q)                                        

## Technical Research
The underlying mathematical foundations, circuit stages, and benchmark results are fully detailed in the included research document[cite: 1]:
* **Research Paper:** `Trainable Resonant Neurons.pdf`[cite: 1]

## Technical Specifications
* **Filter Stage:** Uses a Multiple Feedback (MFB) topology to adaptively tune the frequency response entirely in the circuit domain without inductor elements[cite: 1].
* **Rectifier Stage:** Converts the AC output of the filter step into a unipolar signal via full-wave rectification[cite: 1].
* **Envelope Stage:** Implements an RC smoothing circuit to extract stable amplitude envelopes, regulated by a parameterised responsivity-stability (rho, kappa) trade-off[cite: 1].
* **Hardware Simulation:** To make the hardware simulation viable inside deep learning loops, the non-linear absolute values are smoothed via a square-root approximation[cite: 1].

## Repository Structure
* `Trainable Resonant Neurons.pdf`: The underlying research paper detailing the mathematical foundations, circuit stages, and benchmark results[cite: 1].
* `Training_data.ipynb`: Handles the synthetic generation of controlled, multi-tone audio signal datasets used to rigorously test the models (dataset 2)[cite: 1].
* `NN.ipynb`: Implements the end-to-end machine learning pipeline, modeling simplified mathematical forms of the circuit responses to minimize computational overhead during neural network training[cite: 1].

## Key Experimental Benchmarks

### Task 1: Linear Spectral Separation (Dataset 1)
* **Condition:** Clean multi-tone inputs evenly spaced across a 500-5,000 Hz band[cite: 1].
* **Result:** Both architectures converged smoothly, approaching a peak classification performance of ~95% Accuracy[cite: 1]. Static configurations suffice when boundary conditions are simple[cite: 1].

### Task 2: High Noise and Irregular Spacing (Dataset 2)
* **Condition:** Complex multi-tone signals corrupted by White Gaussian Noise (sigma = 2.0) and subtle, power-invariant frequency shifts[cite: 1].
* **Performance Gap:**
    * Fixed Filter Bank (FFB): Peaked at 78.45% Accuracy[cite: 1].
    * Trainable Resonant Neuron (TRN): Reached 84.69% Accuracy[cite: 1].

*Note: As detailed in the paper, this absolute performance margin of ~6% acts as a lower bound under controlled parameters; the advantage scales dramatically when handling richer, real-world non-stationary data[cite: 1].*

## Usage Summary
1. **Data Generation:** Run `Training_data.ipynb` to construct the perturbed positive and negative signal waveforms[cite: 1].
2. **Model Optimization and Metrics:** Run `NN.ipynb` to execute the neural network pipeline on the generated training datasets and output performance metrics[cite: 1].
