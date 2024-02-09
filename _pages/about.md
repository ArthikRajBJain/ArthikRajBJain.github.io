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

Here's a condensed version of the flow of computation in the model: We begin by projecting the input variables from the 720 × 1440 lat-lon grid to a 2D grid of patches (h × w) with a small patch size (e.g., p = 8), where each patch is represented as a d-dimensional token. These patches, along with positional encoding, are then passed through a series of AFNO layers. Each layer takes an input tensor of patches X ∈ Rh×w×d and conducts spatial mixing followed by channel mixing. Spatial mixing occurs in the Fourier domain.

**Step 1.** Transform tokens to the Fourier domain with

<center>z<sub>m,n</sub> = [DFT(X)]<sub>m,n</sub>,</center>
<br>
where m, n index the patch location and DFT denotes a 2D discrete Fourier transform.

**Step 2.** Apply token weighting in the Fourier domain, and promote sparsity with a Soft-Thresholding and Shrinkage operation as

<center>z̃<sub>m,n</sub> = S<sub>λ</sub>(MLP(z<sub>m,n</sub>)),</center>
<br>
where S<sub>λ</sub>(x) = sign(x)max(\|x\| - λ,0) with the sparsity controlling parameter λ, and MLP() is a 2-layer multi-layer perceptron with block-diagonal weight matrices which are shared across all patches.

**Step 3.** Inverse Fourier to transform back to the patch domain and add a residual connection as

<center>y<sub>m,n</sub> = [IDFT(Z̃)]<sub>m,n</sub> + X<sub>m,n</sub>.</center>
<br>
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

FourCastNet's remarkable efficiency, surpassing traditional models by four to five orders of magnitude, represents a significant milestone in weather prediction. This efficiency stems from its ability to rapidly generate large ensembles, providing nuanced insights into uncertainties inherent in weather forecasting. By swiftly assessing uncertainties, FourCastNet facilitates improved early warnings and enables expedited impact assessments in the face of evolving weather conditions.

This efficiency is primarily attributed to FourCastNet's innovative architecture and computational framework. Leveraging advanced parallel processing techniques and optimized algorithms, FourCastNet streamlines the computation process, drastically reducing the time required for generating forecasts compared to conventional models.

Moreover, the model's speed opens new avenues for exploration in weather prediction research. Researchers can now conduct rapid hypothesis testing for weather variability mechanisms, thanks to FourCastNet's swift computational capabilities. This agility allows scientists to iterate through various scenarios and analyze the impact of different variables on weather patterns with unprecedented speed and accuracy.

In essence, FourCastNet's efficiency revolutionizes the landscape of weather prediction, offering not only faster and more accurate forecasts but also empowering researchers with the tools to delve deeper into the intricacies of weather dynamics.

## Practical Applications:

FourCastNet, with its advanced capabilities in weather forecasting, holds immense potential for various practical applications across different sectors. Some of the key practical applications of FourCastNet include:

1. **Early Warning Systems:** FourCastNet can significantly enhance early warning systems for severe weather events such as hurricanes, tornadoes, and flash floods. By providing accurate and timely forecasts, it enables authorities to issue timely warnings, evacuate vulnerable areas, and implement necessary disaster preparedness measures to minimize potential damage and save lives.

2. **Emergency Response Planning:** Emergency response agencies can leverage FourCastNet's forecasts to better plan and allocate resources during extreme weather events. By anticipating the intensity, duration, and trajectory of weather phenomena, responders can mobilize personnel, equipment, and supplies more effectively, ensuring a swift and coordinated response to emergencies.

3. **Agriculture and Farming:** FourCastNet's predictions can benefit agricultural practices by enabling farmers to make informed decisions regarding crop planting, irrigation, and pest management. By forecasting weather conditions such as precipitation, temperature, and humidity, FourCastNet helps farmers optimize their agricultural activities, minimize crop losses, and improve overall productivity.

4. **Energy Management:** Energy companies can use FourCastNet's forecasts to optimize energy production and distribution. By anticipating fluctuations in weather patterns, such as wind speeds and solar radiation, energy providers can adjust power generation schedules, optimize renewable energy production, and mitigate risks associated with extreme weather events, ensuring a reliable and resilient energy supply.

5. **Transportation and Logistics:** FourCastNet's accurate weather forecasts can aid transportation and logistics companies in planning routes, scheduling shipments, and managing inventory. By anticipating adverse weather conditions such as storms, heavy rainfall, or snowfall, companies can minimize disruptions to supply chains, optimize delivery schedules, and improve overall operational efficiency.

6. **Urban Planning and Infrastructure Development:** Urban planners and infrastructure developers can use FourCastNet's forecasts to design resilient infrastructure and mitigate risks associated with climate change. By anticipating future weather patterns and extreme events, planners can incorporate adaptive measures such as improved drainage systems, flood barriers, and green infrastructure to enhance the resilience of cities and communities against natural disasters.

## Future Horizons:

The advancements showcased by FourCastNet in weather forecasting open up promising avenues for future research and innovation in atmospheric science and related fields. Here are some future horizons that could be explored:

1. **Model Refinement:** Continuous refinement and optimization of the FourCastNet model architecture can further enhance its forecasting accuracy, efficiency, and scalability. This includes exploring novel techniques for spatial and temporal resolution enhancement, improving parameterization schemes, and integrating additional data sources for comprehensive weather prediction.

2. **Integration of Observational Data:** Incorporating real-time observational data from ground-based sensors, satellites, and remote sensing platforms into the forecasting pipeline can enrich the information available to FourCastNet and improve the accuracy of its predictions. This entails developing robust data assimilation techniques and fusion algorithms to effectively integrate diverse data sources and leverage their complementary strengths.

3. **Hybrid Modeling Approaches:** Investigating hybrid modeling approaches that combine the strengths of physics-based models and data-driven techniques like FourCastNet can lead to more comprehensive and robust forecasting systems. By synergistically integrating physical principles with empirical insights, hybrid models can overcome limitations associated with individual modeling paradigms and offer more holistic representations of atmospheric dynamics.

4. **Applications Beyond Weather Forecasting:** Exploring applications of FourCastNet beyond traditional weather forecasting domains, such as climate modeling, environmental monitoring, renewable energy management, and disaster risk reduction, can extend its impact and relevance to broader societal challenges. By adapting and customizing FourCastNet's capabilities to diverse problem domains, researchers can address pressing issues related to climate change, sustainability, and resilience.

# Example:
![Illustration of global Total Precipitiation](/images/Example1.png)

# Conclusion:

In conclusion, FourCastNet represents a significant leap forward in the field of weather forecasting, leveraging state-of-the-art machine learning techniques to deliver accurate, high-resolution predictions of atmospheric variables. Its innovative architecture, efficient computational framework, and superior performance pave the way for transformative advancements in weather prediction and related applications.

By harnessing the power of data-driven modeling, FourCastNet enables meteorologists, policymakers, and stakeholders to make informed decisions, mitigate risks, and build resilient communities in the face of increasingly complex and dynamic weather phenomena. As we look towards the future, continued research, collaboration, and innovation will drive further advancements in atmospheric science, ushering in a new era of precision forecasting and proactive risk management.

With its unparalleled capabilities and untapped potential, FourCastNet heralds a new chapter in the quest for accurate, reliable, and actionable weather intelligence, empowering us to better understand, anticipate, and adapt to the ever-changing dynamics of our planet's atmosphere. As we embark on this journey of discovery and innovation, FourCastNet stands poised to shape the future of weather forecasting and usher in a new era of resilience, sustainability, and preparedness for generations to come.
