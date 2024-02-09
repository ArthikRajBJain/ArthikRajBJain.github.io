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

![Weather Change in the globe](/images/Weather2.gif)

## Understanding Ensemble Forecasting:

FourCastNet leverages the power of ensemble forecasting, a technique that models multiple possible trajectories of a weather system to capture uncertainty and improve forecast accuracy. By generating large ensemble forecasts using perturbed initial conditions, FourCastNet provides probabilistic forecasts that quantify the likelihood of extreme events, such as hurricanes and atmospheric rivers. This ensemble approach enables forecasters to assess the range of possible outcomes and make more informed decisions.

## Computational Efficiency:

What sets FourCastNet apart is its remarkable computational efficiency. Compared to traditional NWP models like the Integrated Forecasting System (IFS), FourCastNet is orders of magnitude faster and consumes significantly less energy. This efficiency enables the generation of large ensemble forecasts in seconds, facilitating rapid response to weather events and enhanced uncertainty quantification. Moreover, FourCastNet's efficient use of computational resources makes it scalable, allowing it to handle increasingly large datasets and model more complex atmospheric processes.

## Model Description:

Fourier-based neural network forecasting model, to generate global data-driven forecasts of key atmospheric variables at a resolution of 0.25◦, which corresponds to a spatial resolution of roughly 30 km × 30 km near the equator and a global grid size of 720 × 1440 pixels. This allows us, for the first time, to make a direct comparison with the high-resolution Integrated Forecasting System (IFS) model of the European Center for Medium-Range Weather Forecasting (ECMWF).

![Machine Learning Model of FourCastNet](/images/Model.png)

(a) The multi-layer transformer design employs the Adaptive Fourier Neural Operator (AFNO) alongside shared MLP and frequency soft-thresholding for spatial token mixing. Initially, the input frame is partitioned into h × w patches, each sized p × p × c. These patches undergo embedding into a higher-dimensional space with numerous latent channels, followed by the addition of positional embedding to create a token sequence. Spatial mixing via AFNO and subsequent channel mixing occur for each token across L layers. Finally, a linear decoder reconstructs patches for the next frame from the final embedding. The right-hand panels illustrate additional training and inference modes of the FourCastNet model: (b) two-step fine-tuning, (c) backbone model forecasting 20 variables (where p(k + 1) indicates 6-hour accumulated total precipitation between k + 1 and k + 2 time steps), and (d) free-running autoregressive inference mode.

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

![Efficient Ensemble](/images/Ensemble.png)

The FourCastNet model demonstrates remarkable accuracy in forecasting fine-scale, rapidly changing variables crucial for hurricane predictions. Using Hurricane Michael as a case study, Panel (a) displays the mean position of the Mean Sea Level Pressure (indicating the hurricane's eye) forecasted by a 100-member ensemble using FourCastNet (red circles) compared to ERA5 reanalysis ground truth (blue squares) over 108 hours starting from October 7, 2018, at 00:00 UTC. Ensemble forecasts were generated by perturbing the initial condition with Gaussian noise, producing 100 trajectories. Shaded ellipses represent the 90th percentile spread of the hurricane eye's longitudinal and latitudinal positions in the FourCastNet ensemble. Panel (b) illustrates the minimum MSLP forecasted by FourCastNet (red filled circles) and the corresponding true minimum from ERA5 reanalysis (blue filled circles), with the red shaded region indicating the 90 percent confidence region in the 100-member ensemble forecast. Panels (c) and (d) depict surface wind speed and 850hPa wind speed predictions at lead times of 18, 36, 54, and 72 hours generated by FourCastNet alongside true wind speeds. The leftmost column shows surface wind speed and 850hPa speed in the initial condition (Oct. 7, 2018, 00:00 UTC) used to initialize the forecast. These forecasts collectively trace Hurricane Michael's formation, intensification, and path from a tropical depression to a category 5 hurricane, culminating in landfall on Florida's west coast.

## Comparison with IFS Model:

In the arena of weather prediction, FourCastNet stands tall against the formidable IFS model. Despite some limitations, such as the absence of physics constraints and a reduced variable set, FourCastNet holds its ground. Its accuracy rivals that of IFS in numerous variables, with notable excellence in precipitation forecasting, outpacing IFS in select scenarios.

![Comparision With IFS](/images/ComparisionIFS.png)

The comparison between ERA5, FourCastNet, and IFS examines extreme percentiles. In the left panel, the highest percentiles of TP and U<sub>10</sub> distribution are depicted at a 24-hour forecast time, selected from a randomly sampled initial condition. The right panel displays the TP and U<sub>10</sub> relative quantile error (RQE, explained in the text) across forecast time, averaged over N<sub>f</sub> initial conditions in 2018 (the filled region covers the 1st and 3rd quartiles). On average, both models exhibit a slightly negative RQE trend, indicating an under-prediction of the most extreme values, particularly for TP.

## Limited-Purpose Forecasting:

FourCastNet's brilliance truly shines in scenarios demanding precision and efficiency. Imagine a wind farm operator seeking short-term surface wind speed forecasts—FourCastNet emerges as an attractive choice. Its minimal infrastructure requirements redefine the landscape, enabling accurate forecasts with a tabletop computer and a single GPU.

## Comparison with State-of-the-Art DL Weather Prediction:

In a head-to-head clash with the state-of-the-art DLWP model, FourCastNet emerges victorious. Predicting more variables at a significantly higher resolution, it goes beyond the status quo. Visual metrics, including Accuracy (ACC) and Root Mean Square Error (RMSE), underscore FourCastNet's dominance, even when its outputs are downscaled to match DLWP's resolution.

![Comparision With Other DL Algorithms](/images/Comparision_DL.png)

Comparing ACC and RMSE metrics among (downsampled) FourCastNet predictions, (downsampled) IFS, and the baseline state-of-the-art DLWP model [Weyn et al., 2020] for (a) Z500 and (b) T2m, FourCastNet predictions exhibit substantial enhancement over the baseline model. Additionally, FourCastNet produces predictions with eight times higher resolution, enabling the resolution of numerous crucial small-scale features compared to the DLWP model.

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
