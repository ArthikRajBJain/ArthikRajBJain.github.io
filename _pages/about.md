---
permalink: /
title: "FourCastNet: A Quantum Leap in Weather
Forecasting Unveiled"
excerpt: "About me"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

In the dynamic world of weather forecasting, advancements in technology continually push the boundaries of accuracy and efficiency. One such groundbreaking development is FourCastNet, a global data-driven high-resolution weather forecasting model that promises to revolutionize how we perceive and predict weather events. Weather forecasting plays a pivotal role in our daily lives, from planning outdoor activities to preparing for extreme weather events. Traditional numerical weather prediction (NWP) models have long been the backbone of forecasting systems, but they come with limitations in resolution, speed, and computational efficiency. Enter FourCastNet – a cutting-edge deep learning model designed to address these challenges and redefine the landscape of weather forecasting.

# Diving into FourCastNet: A Symphony of Data-Driven Forecasting

## Overview:

At its core, FourCastNet is a testament to the fusion of innovation and neural networks. Developed on the robust foundations of Fourier Neural Operator (FNO) and Advection-Free Neural Operator (AFNO), this deep learning model has swiftly become a game-changer in the realm of weather prediction. Crafted in less than a year, it represents a departure from traditional numerical weather prediction (NWP) methodologies.
![Weather Change in the globe](/images/Weather.gif)
## Understanding Ensemble Forecasting:

FourCastNet leverages the power of ensemble forecasting, a technique that models multiple possible trajectories of a weather system to capture uncertainty and improve forecast accuracy. By generating large ensemble forecasts using perturbed initial conditions, FourCastNet provides probabilistic forecasts that quantify the likelihood of extreme events, such as hurricanes and atmospheric rivers. This ensemble approach enables forecasters to assess the range of possible outcomes and make more informed decisions.

## Computational Efficiency:

What sets FourCastNet apart is its remarkable computational efficiency. Compared to traditional NWP models like the Integrated Forecasting System (IFS), FourCastNet is orders of magnitude faster and consumes significantly less energy. This efficiency enables the generation of large ensemble forecasts in seconds, facilitating rapid response to weather events and enhanced uncertainty quantification. Moreover, FourCastNet's efficient use of computational resources makes it scalable, allowing it to handle increasingly large datasets and model more complex atmospheric processes.

## Model Description:

Fourier-based neural network forecasting model, to generate global data-driven forecasts of key atmospheric variables at a resolution of 0.25◦, which corresponds to a spatial resolution of roughly 30 km × 30 km near the equator and a global grid size of 720 × 1440 pixels. This allows us, for the first time, to make a direct comparison with the high-resolution Integrated Forecasting System (IFS) model of the European Center for Medium-Range Weather Forecasting (ECMWF).

![Machine Learning Model of FourCastNet](/images/Model.png)
The multi-layer transformer architecture that utilizes the Adaptive Fourier Neural Operator with shared MLP and frequency soft-thresholding for spatial token mixing. The input frame is first divided into a h × w grid of patches, where each patch has a small size p × p × c. Each patch is then embedded in a higher dimensional space with high number of latent channels and position embedding is added to form a sequence of tokens. Tokens are then mixed spatially using AFNO, and subsequently for each token the latent channels are mixed. This process is repeated for L layers, and finally a linear decoder reconstructs the patches for the next frame from the final embedding. The right-hand panels describe the FourCastNet model’s additional training and inference modes: (b) two-step fine-tuning, (c) backbone model that forecasts the 20 variables in Table 1 with secondary precipitation diagnostic model (note that p(k + 1) denotes the 6 hour accumulated total precipitation that falls between k + 1 and k + 2 time steps) (d) forecast model in free-running autoregressive inference mode.

The Adaptive Fourier Neural Operator (AFNO) model represents a groundbreaking approach to high-resolution weather forecasting, incorporating state-of-the-art deep learning techniques tailored for complex atmospheric systems. Developed by Guibas et al. in 2022, AFNO combines the robustness of the Fourier Neural Operator (FNO) learning approach with the efficiency of the Vision Transformer (ViT) architecture, offering unparalleled performance in capturing fine-scale atmospheric dynamics.

### Key Components:

1. Fourier Neural Operator (FNO) Integration:
  - The FNO approach, initially proposed by Li et al. in 2021, has demonstrated remarkable efficacy in modeling complex partial differential equation (PDE) systems, including turbulent Navier-Stokes equations.
  - By leveraging the Fourier domain, FNO efficiently captures spatial and temporal dependencies, making it an ideal candidate for data-driven atmospheric modeling within the AFNO framework.
2. Vision Transformer (ViT) Backbone:
  - ViT architectures have emerged as the gold standard in computer vision tasks, owing to their ability to capture global interactions between features using multi-head self-attention mechanisms.
  - However, traditional ViT architectures face computational challenges when dealing with high-resolution inputs due to quadratic spatial mixing complexity.
3. Continuous Global Convolution:
  - AFNO introduces a novel approach to spatial token mixing, framing the operation as continuous global convolution implemented efficiently in the Fourier domain using Fast Fourier Transforms (FFTs).
  - This innovative design significantly reduces spatial mixing complexity to O(N log N), where N represents the number of image patches or tokens, enabling scalability to high-resolution datasets.

### Contrasting with Convolutional Architectures:

- Unlike conventional convolutional architectures, which struggle with scalability and memory constraints, AFNO offers practical benefits, particularly at high resolutions.
- For instance, while a 720x1440 resolution FourCastNet model requires approximately 10GB of memory with a batch size of 1, a convolutional network like the 19-layer ResNet would demand around 83GB for the same resolution.
- Moreover, preliminary experiments indicate that convolutional architectures exhibit limitations in capturing small scales over multiple time steps in auto-regressive inference, further emphasizing the superiority of the ViT-based AFNO model.

## Efficient Ensemble Forecasting:

The prowess of FourCastNet becomes apparent in its ability to orchestrate a 100-member ensemble forecast seamlessly on a single 4GPU A100 node. This efficiency, a stark contrast to the resource-intensive demands of conventional models like the Integrated Forecasting System (IFS), propels FourCastNet to the forefront. At a 30km resolution, it operates at a mind-boggling speed—145,000 times faster than its IFS counterpart. The energy efficiency is equally remarkable, consuming a mere 24,000 times less energy.

## Comparison with IFS Model:

In the arena of weather prediction, FourCastNet stands tall against the formidable IFS model. Despite some limitations, such as the absence of physics constraints and a reduced variable set, FourCastNet holds its ground. Its accuracy rivals that of IFS in numerous variables, with notable excellence in precipitation forecasting, outpacing IFS in select scenarios.

## Limited-Purpose Forecasting:

FourCastNet's brilliance truly shines in scenarios demanding precision and efficiency. Imagine a wind farm operator seeking short-term surface wind speed forecasts—FourCastNet emerges as an attractive choice. Its minimal infrastructure requirements redefine the landscape, enabling accurate forecasts with a tabletop computer and a single GPU.

## Comparison with State-of-the-Art DL Weather Prediction:

In a head-to-head clash with the state-of-the-art DLWP model, FourCastNet emerges victorious. Predicting more variables at a significantly higher resolution, it goes beyond the status quo. Visual metrics, including Accuracy (ACC) and Root Mean Square Error (RMSE), underscore FourCastNet's dominance, even when its outputs are downscaled to match DLWP's resolution.

# Implications and Future Trajectories:

## Efficiency and Accessibility:

FourCastNet's efficiency, transcending traditional models by four to five orders of magnitude, unfolds a new chapter in weather prediction. Rapid generation of large ensembles allows for nuanced insights into uncertainties, paving the way for improved early warnings and swift impact assessments. The model's speed also invites exploration, enabling rapid hypothesis testing for weather variability mechanisms.

## Practical Applications:

The precision of FourCastNet in short-range precipitation forecasts extends its influence to disaster mitigation and rapid responses. In the realm of wind energy, its high-resolution wind forecasts become a compass for optimizing layouts and navigating the fluctuations of wind power output.

## Future Horizons:

While FourCastNet is currently without a real-time data assimilation component, future iterations are poised to bridge this gap. The model's potential to predict all variables in NWP hints at a revolution in weather prediction across all atmospheric levels.

# Example:
![Illustration of global Total Precipitiation](/images/Example1.png)

# Conclusion:

FourCastNet is not merely a weather model; it is a revelation in the marriage of deep learning and meteorology. Its speed, efficiency, and accuracy signal a new era in weather forecasting—one that promises benefits in disaster management, energy planning, and scientific exploration. As the journey of advancements continues, FourCastNet stands tall, unraveling the complexities of our atmosphere with the precision of a symphony conductor directing a celestial orchestra.
