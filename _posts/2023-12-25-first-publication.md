---
layout: distill
title: "Microphone Conversion: Mitigating Device Variability in Sound Event Classification"
description: "[ICASSP 2024] A generative method to tackle domain mismatch problem in sound event classifcation systems"
giscus_comments: true
date: 2023-12-25 00:08:00
tags: deep-learning generative-AI research audio-event-classification
categories: research
featured: true
# img:m 

authors:
  - name: Hongseok Oh
    affiliations:
      name: University of Calfironia, San Diego

bibliography: 2023-12-25-first-publication.bib

toc:
  - name: Exploring the World of Sound Recognition
      # - name: Sound Event Classification and the Challenge of Device Variability
      # - name: Our Innovative Approach to Enhance Reliability
  - name: "Developing a New Technique and Dataset"
      # - name: How We Created a Unique Sound Dataset
      # - name: Simplifying Our Method for Better Sound Recognition
  - name: "Experiments and Results"
      # - name: "Comparative Analysis: Our Method vs. Traditional Approaches"
      # - name: Implications and Impact of Our Findings
  - name: "The Future of Sound Event Classification"
      # - name: Summarizing Our Contributions
      # - name: Future Directions and Potential Applications
  - name: Further Insights and References
      # - name: Additional Resources for Enthusiasts and Researchers
---

## Exploring the World of Sound Recognition
### Sound Event Classification and the Challenge of Device Variability
Sound Event Classification (SEC) is a fascinating area of technology that aims to identify different types of sounds, like speech, music, and environmental noises, using advanced signal processing and machine learning techniques. Sound Event Classification (SEC) powers popular technologies like Apple’s Sound Recognition, Amazon's Alexa, and Google Home, enabling them to identify sounds from speech to environmental noises. Despite its broad applications, SEC faces challenges, particularly when audio is recorded on different devices, leading to performance issues. These variations, often imperceptible to human ears, can drastically affect the performance of SEC systems.

<div class="fake-img l-body">
  <p>{% include figure.html path="assets/img/apple-sound-recognition.png" %}</p>
</div>
<div class="caption">
  Apple's Sound Recognition <https://www.youtube.com/watch?v=Db9Xsw5Aa5w>
</div>

### Our Innovative Approach to Enhance Reliability
Traditional solutions, such as data augmentation, have been limited, often relying on synthetic data which doesn’t fully capture real-world complexities. Furthermore, most initiatives, including those like [the DCASE Challenge](https://dcase.community), have their limitations, primarily due to their reliance on synthetic evaluation data. This limitation raises questions about the thoroughness and real-world applicability of their evaluations. Recognizing these challenges, our research addresses these challenges, aiming to enhance SEC systems for more accurate and reliable use in everyday technologies.

***

## Developing a New Technique and Dataset
### How We Created a Unique Sound Dataset
In our journey to enhance sound event classification, we crafted the 'Deeply Device Dataset,' a diverse collection capturing 75 sound classes. This dataset, a mix of direct recordings and carefully selected samples from [the RWCP Sound Scene Database](https://www.openslr.org/13/), includes a variety of sounds from daily life noises and human interactions to musical instruments. Key to our approach was the use of 18 different recording devices, encompassing a range of smartphones, laptops, and specialized microphones, each adding its unique acoustic signature to the dataset.

The recording process unfolded in an anechoic chamber, an environment meticulously designed to eliminate external noise and echo, ensuring pristine audio capture. This setup allowed us to systematically record each sound class, with devices positioned to optimally capture the emitted sounds. The result is two subsets: a comprehensive one with all sound classes and devices, and a smaller, focused subset. Each sound event in these subsets was aligned and annotated with precision, offering a rich resource for analyzing how different devices impact sound event classification.

<div class="fake-img l-body">
  <p>{% include figure.html path="assets/img/anechoic-chamber.jpg" %}</p>
</div>
<div class="caption">
  The anechoic chamber used for the experiments
</div>

### Simplifying Our Method for Better Sound Recognition
In our pursuit to enhance sound event classification (SEC), we introduced a novel concept called 'Microphone Conversion'. This innovative technique aims to bridge the gap between different recording devices by transforming the spectrograms from one device to mimic those of another. At the heart of this technique is a mapping function, designed to convert the spectrogram data from a source device ($X_A$) into a form that statistically resembles the target device ($X_B$).

To achieve this transformation, we employed CycleGAN<d-cite key="zhu2017unpaired"></d-cite>, a groundbreaking framework in the realm of unsupervised image-to-image translation. CycleGAN is adept at learning mappings between two unpaired data domains, making it ideal for our purpose. Built on Generative Adversarial Networks (GANs), it involves two generators, $F$ and $G$, and two discriminators, $D_A$ and $D_B$. These components work in tandem: while the generators map data bijectively between the domains, the discriminators aim to distinguish real images from the converted ones.

The effectiveness of CycleGAN in our context lies in its dual-loss setup. The adversarial loss pushes the generators to produce outputs that are indistinguishable from the target domain, ensuring authenticity. Meanwhile, the cycle-consistency loss guarantees that the generated images, once reverse-mapped, closely resemble their original forms. This balance ensures that while the style of the spectrograms adapts to the target domain, their content remains intact and accurate.

$$
\mathcal{L}_{adv}(F, D_B, X_A, X_B) = \\
\mathbb{E}_{X_A{\sim}p(x_a)}\left[{\log}(1-D_B(F(X_A)))\right] + \mathbb{E}_{X_B{\sim}p(x_b)}\left[{\log}D_B(X_B)\right]
$$

$$
\mathcal{L}_{cycle}(F, G, X_A, X_B) = 
\mathbb{E}_{X_A{\sim}p(x_a)}[||{G(F(X_A)) - X_A}||_{1}] + \mathbb{E}_{X_B{\sim}p(x_b)}[||{F(G(X_B)) - X_B}||_{1}]
$$

For the network architecture, we adapted the CycleGAN implementation directly from the original author’s code. Our generator network consists of two upsampling and downsampling layers, along with nine residual blocks with instance normalization, with the omission of the hyperbolic tangent layer. The discriminator, a 16x16 PatchGAN with instance normalization, was chosen for its effectiveness in minimizing blurriness and ensuring better convergence in the output.

Through this approach, we were able to effectively 'translate' audio data across devices, preserving the integrity of the sound events while adapting to the unique acoustic characteristics of various recording devices.

***

## Experiments and Results
### Comparative Analysis: Our Method vs. Traditional Approaches
In our research, we demonstrated how our proposed method can benefit SEC systems in the face of device variability. We also conducted a thorough examination of the leading methods from recent DCASE Challenges, which are designed to mitigate device variability in sound event classification (SEC) systems, and compare their results with ours. 

We evaluated techniques like Freq-MixStyle<d-cite key="Schmid2022"></d-cite> and Residual Normalization<d-cite key="Kim2021b"></d-cite>, which leverage frequency-wise statistics for improved generalization. Additionally, we explored an extended version known as Relaxed Instance Frequency-wise Normalization (RFN)<d-cite key="kim22_interspeechw"></d-cite> applied across five bottleneck blocks, and FilterAugment<d-cite key="Nam2021"></d-cite>, which adjusts spectrograms using optimally generated linear filters. Our testing also included standard data augmentations such as Gaussian noise, room impulse response, and pitch shift, along with advanced methods like SpecAugment and MixUp, each applied with a probability of 0.5, except for RFN.

Our evaluation, as detailed in Tables 1 and 2, highlighted significant performance vulnerabilities in SEC systems when dealing with heterogeneous recording devices. A striking example was observed in the case of T3, where there was a dramatic performance drop of up to 73.7% compared to the baseline 'Real' metric. Conversely, models showed better performance on devices like T2 and T5, which share more similarities with the training data, as evidenced by their proximity in the t-SNE feature space, with a more modest performance drop of 26.3% and 29.5%, respectively. Traditional data augmentation methods offered limited improvement.

Among the more specialized recent approaches, Freq-MixStyle emerged as the most effective, achieving an average F1 score of 85.5% and demonstrating consistent performance with a narrow 3.8% confidence interval. However, our Microphone Conversion technique, MC-200-Gen, outshone these methods with an impressive average F1 score of 90.7% and minimal variability (3.5%). In scenarios requiring adaptation, SEC models employing adaptation strategies generally outperformed MC-200-Adapt (p=0.5) on 4 out of 6 target devices, showing a 1.3% gain in overall performance. Remarkably, they nearly matched the 'Real' performance metric when trained on a diverse set of devices.

Our findings underscore the effectiveness of our Microphone Conversion approach, particularly its capability to enhance both generalization and adaptability of SEC systems. The promising results also suggest the potential for further optimization with extended training durations, paving the way for more robust and reliable SEC systems in the face of device variability.

### Implications and Impact of Our Findings
***

## The Future of Sound Event Classification
### Summarizing Our Contributions
You can add interative plots using plotly + iframes :framed_picture:

<div class="l-page">
  <iframe src="{{ '/assets/plotly/demo.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

The plot must be generated separately and saved into an HTML file.
To generate the plot that you see above, you can use the following code snippet:

{% highlight python %}
import pandas as pd
import plotly.express as px
df = pd.read_csv(
  'https://raw.githubusercontent.com/plotly/datasets/master/earthquakes-23k.csv'
)
fig = px.density_mapbox(
  df,
  lat='Latitude',
  lon='Longitude',
  z='Magnitude',
  radius=10,
  center=dict(lat=0, lon=180),
  zoom=0,
  mapbox_style="stamen-terrain",
)
fig.show()
fig.write_html('assets/plotly/demo.html')
{% endhighlight %}
### Future Directions and Potential Applications
***

## Further Insights and References
### Additional Resources for Enthusiasts and Researchers
Details boxes are collapsible boxes which hide additional information from the user. They can be added with the `details` liquid tag:

{% details Click here to know more %}
Additional details, where math $$ 2x - 1 $$ and `code` is rendered correctly.
{% enddetails %}