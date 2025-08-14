# Hybrid Thermal Modeling of an FSPM Motor for Predictive Maintenance

![DOI](https://img.shields.io/badge/DOI-10.1016/j.csite.2024.105286-blue)
![Framework](https://img.shields.io/badge/Framework-MATLAB%20%26%20Simulink-orange)

This repository contains the simulation models and data for the research paper:

> **Heat Transfer Study on a Stator-Permanent Magnet Electric Motor: A Hybrid Estimation Model for Real-Time Temperature Monitoring and Predictive Maintenance**

Published in *Case Studies in Thermal Engineering*. You can access the full paper here:  
➡️ **https://doi.org/10.1016/j.csite.2024.105286**

---

## Overview

The core of this research is a novel **hybrid temperature estimation model** designed for real-time, sensor-less thermal monitoring of a Flux-Switching Permanent Magnet (FSPM) motor. This approach is crucial for motors operating under natural convection, where there's a higher risk of thermal breakdown. The model combines a Lumped Parameter Thermal Network (LPTN) with a Feed-Forward Neural Network (FNN) to accurately predict the temperature of critical components like the windings and permanent magnets (PMs).

The ultimate goal is to enable **predictive maintenance** and intelligent **operation management**, preventing failures before they occur by analyzing the motor's thermal state in real-time.

![Model Architecture](figures/FVM-1.png)
> *3D Finite Element Model (FEM) used for numerical thermal validation.*

---

## Model Architecture

The monitoring system is built on two primary stages: **Power Loss Estimation** and **Hybrid Temperature Estimation**. It uses readily available signals from the motor's drive unit, such as current and speed, eliminating the need for physical temperature sensors.

### 1. Power Loss Estimation

A deep neural network estimates the core losses and PM eddy current losses, which are the primary sources of heat. This model was trained on data generated from a verified finite element electromagnetic study.

| Core Loss Contour | PM Loss Contour |
| :-----------------: | :---------------: |
| ![Core Loss Contour](figures/CorelossContour-1.png) | ![PM Loss Contour](figures/PMlossContour-1.png) |
> *Distribution of core loss and PM eddy current loss as calculated by the FEA model.*

### 2. Hybrid Temperature Estimation

The estimated power losses, along with environmental conditions (ambient temperature and Heat Transfer Coefficient - HTC), are fed into the hybrid temperature estimation unit.

![Hybrid Estimation Unit](https://i.imgur.com/uR1uQ4K.png)
> *The proposed hybrid estimation unit, combining an LPTN and an FNN.*

This unit first calculates the motor's casing temperature using a fast and efficient 2-node LPTN model. This temperature, along with the motor's operating point, is then used by a highly accurate FNN to predict the dynamic temperature profiles of the windings and PMs.

| Winding Temperature | PM Temperature |
| :-----------------: | :--------------: |
| ![Winding Temperature Profile](figures/Winding.png) | ![PM Temperature Profile](figures/PM.png) |
> *Transient thermal simulation results for the volume average temperature of the winding and PMs, which the hybrid model is trained to replicate.*

---

## Key Results & Capabilities

The final model can accurately track the motor's temperature with a peak error below **7.5%** when compared to experimental measurements.

### Predictive Maintenance

The model can predict when a component's temperature will exceed its safety limit, allowing the control system to take preventive action. For instance, under a simulated short-circuit fault, the model predicts that the winding insulation limit of 105°C will be breached in just **970 seconds**.

![Fault Prediction](https://i.imgur.com/83pLhXq.png)
> *Temperature profiles showing a nominal run (a) vs. a short-circuit fault (b), where the model predicts rapid temperature violation.*

### Duty Cycle Management

The system can also be used to safely manage the motor's duty cycle during overload conditions by guiding the use of a forced convection cooling system (e.g., a fan).

---

## Repository Contents

This repository is organized as follows:

* **/Electromagnetic simulation:** Contains the zipped files for the electromagnetic FEA study used to generate data for the power loss model.
* **/Figures:** Contains key figures and images used in the paper and this README.
* **/Steady-State Thermal Simulation:** Contains the zipped files for the steady-state numerical thermal analysis.
* **/Transient Thermal Simulation:** Contains the zipped files for the transient thermal analysis used for model validation.
* **README.md:** This file.

> **Please note:** The `.zip` files containing the simulation models are password-protected. To request access, please contact the author at **hamidsharifi32@gmail.com**.

---

## Getting Started

1.  Clone this repository to your local machine.
2.  Request the password for the `.zip` files via the email above.
3.  Unzip the folder corresponding to the simulation you wish to examine.
4.  All models were developed and tested using **MATLAB & Simulink**.
5.  All simulations are conducted in Ansys.

---

## Explanation of Key Figures

This section provides a brief explanation for each of the key figures included in the `/figures` directory.

| Figure Thumbnail | Description |
| :---: | :--- |
| ![Core Loss Contour](figures/CorelossContour-1.png) | **Core Loss Distribution (Fig. 18 in the paper)** <br> This figure shows the distribution of core losses in the stator and rotor at four different time steps during operation. The FEA model calculates these losses by considering the magnetic flux density and saturation in the steel core, providing a crucial heat source input for the thermal simulation. |
| ![Finite Element Model](figures/FVM-1.png) | **Finite Element Thermal Simulation Results (Fig. 8 in the paper)** <br> This shows the steady-state temperature field distribution across all major components of the motor, as calculated by the 3-D Finite Element Analysis (FEA). It accurately identifies the hotspot location in the end winding section, which reaches a maximum temperature of 62.79°C under nominal conditions. |
| ![PM Temperature Profile](figures/PM.png) | **Transient Temperature of Permanent Magnets (Fig. 9b in the paper)** <br> This plot shows the simulated volume-average temperature of the Permanent Magnets (PMs) over time during the heating phase. The profile is calculated from the transient numerical model and was found to be in acceptable agreement with the experimental test data. |
| ![PM Loss Contour](figures/PMlossContour-1.png) | **PM Eddy Current Loss Distribution (Fig. 19 in the paper)** <br> This illustrates the distribution of eddy current losses generated directly within the permanent magnets at four different time steps. While smaller than core losses, these are a direct heat source within the thermally sensitive PMs and are critical for accurate temperature prediction. |
| ![Temperature vs HTC](figures/TemperatureVSh3-1.png) | **Effect of Heat Transfer Coefficient on Temperature (Fig. 10 in the paper)** <br> This graph demonstrates the effect of the convective Heat Transfer Coefficient (HTC) on the steady-state temperature of the winding, PM, stator, and casing. It shows that increasing the cooling performance (a higher HTC) nonlinearly reduces the motor's temperature, with the effect diminishing significantly after an HTC of 30 W/m²°C. |
| ![Winding Temperature Profile](figures/Winding.png) | **Transient Temperature of Winding (Fig. 9a in the paper)** <br> This plot shows the simulated volume-average temperature of the winding over time. As the primary source of copper losses, the winding temperature is a critical indicator of the motor's thermal state. The dynamic profile shows a thermal time constant (${\tau_h}$) of 4200 seconds, which closely matches the experimental value. |

---

## How to Cite This Work

If you use the models or findings from this project in your research, please cite the original paper.

**Plain Text:**
> Sharifi, T., Eikani, A., & Mirsalim, M. (2024). Heat transfer study on a stator-permanent magnet electric motor: A hybrid estimation model for real-time temperature monitoring and predictive maintenance. *Case Studies in Thermal Engineering*, *63*, 105286.

**BibTeX:**
```bibtex
@article{Sharifi2024,
  title   = {Heat transfer study on a stator-permanent magnet electric motor: A hybrid estimation model for real-time temperature monitoring and predictive maintenance},
  author  = {Sharifi, Tohid and Eikani, Alireza and Mirsalim, Mojtaba},
  journal = {Case Studies in Thermal Engineering},
  volume  = {63},
  pages   = {105286},
  year    = {2024},
  doi     = {10.1016/j.csite.2024.105286}
}
