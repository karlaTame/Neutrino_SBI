# Neutrino_SBI

# Simulation-Based Inference for Neutrino Interaction Model Tuning

This repository contains the code used for the paper **“Simulation-Based Inference for Neutrino Interaction Model Parameter Tuning”**, submitted to the **NeurIPS 2025 Workshop on Machine Learning and the Physical Sciences (ML4PS)**.

## Overview

This project demonstrates, for the first time, the application of **simulation-based inference (SBI)** techniques to tune **neutrino–nucleus interaction models**. Using a mock dataset based on the **MicroBooNE** tuning of the **GENIE** event generator, our approach employs a **Neural Posterior Estimator (NPE)** with **Masked Autoregressive Flows (MAF)** to infer the posterior distributions of key GENIE parameters directly from simulated histograms.

The workflow provides a scalable and amortized framework for performing likelihood-free inference in high-dimensional parameter spaces, offering a pathway to more efficient and uncertainty-aware model tuning for next-generation neutrino experiments such as **DUNE** and **SBND**.

## Data and Methods

* **Simulation Framework:**

  * Neutrino–nucleus interactions are generated with **GENIE** and processed through **NUISANCE** to produce histograms comparable to experimental data (T2K dataset).
  * Four GENIE model parameters are varied:

    * `MaCCQE`
    * `NormCCMEC`
    * `XSecShape_CCMEC`
    * `RPA_CCQE`

* **Training Setup:**

  * 200,000 simulated configurations for training
  * 1,000 independent configurations for validation and testing
  * Histogram dimensionality reduced from 58 → 24 via an embedding network
  * Neural Posterior Estimator (NPE) with **Masked Autoregressive Flow (6 layers, 55 hidden units per block)**
  * Training performed on CPU (≈10 min per run)

* **Software Dependencies:**

  * `Python >=3.10`
  * `sbi`, `torch`, `numpy`, `pandas`, `matplotlib`
  * `GENIE` and `NUISANCE` (for event generation)

## Results Summary

The trained SBI model successfully recovers the correct underlying parameter values when evaluated on mock data generated with the MicroBooNE tune. Posterior coverage tests confirm that the model produces well-calibrated uncertainty estimates, with slight underconfidence in some parameters and minor overconfidence in one.

This work establishes a validated proof-of-principle for applying SBI to neutrino interaction modeling, paving the way for more complex and realistic tuning campaigns using experimental data.

## Citation

If you use this code or its results, please cite:

**K. Tame-Narvaez et al., “Simulation-Based Inference for Neutrino Interaction Model Parameter Tuning,” NeurIPS 2025 ML4PS Workshop.**

## Acknowledgments

This work was performed under the **FermiForward Discovery Group, LLC**, Contract No. 89243024CSC000002 with the U.S. Department of Energy, Office of Science, Office of High Energy Physics.
K. Tame-Narvaez acknowledges support from DOE Grant KA2401045.
