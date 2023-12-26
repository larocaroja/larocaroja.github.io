---
layout: distill
title: "Microphone Conversion: Mitigating Device Variability in Sound Event Classification"
description: A generative method to tackle domain mismatch problem in sound event classifcation systems
giscus_comments: true
date: 2023-12-25 00:08:00
tags: deep-learning generative-AI research audio-event-classification
categories: research
featured: true

authors:
  - name: Hongseok Oh
    affiliations:
      name: University of Calfironia, San Diego

bibliography: 2023-12-25-first-publication.bib

toc:
  - name: Exploring the World of Sound Recognition
      - name: Sound Event Classification and the Challenge of Device Variability
      - name: Our Innovative Approach to Enhance Reliability
  - name: "The Core of Our Research: Developing a New Technique and Dataset"
      - name: How We Created a Unique Sound Dataset
      - name: Simplifying Our Method for Better Sound Recognition
  - name: "Breaking New Ground: Testing and Results"
      - name: "Comparative Analysis: Our Method vs. Traditional Approaches"
      - name: Implications and Impact of Our Findings
  - name: "The Future of Sound Event Classification"
      - name: Summarizing Our Contributions
      - name: Future Directions and Potential Applications
  - name: The Further Insights and References
      - name: Additional Resources for Enthusiasts and Researchers
---

## Exploring the World of Sound Recognition
### Sound Event Classification and the Challenge of Device Variability
This theme supports rendering beautiful math in inline and display modes using [MathJax 3](https://www.mathjax.org/) engine.
You just need to surround your math expression with `$$`, like `$$ E = mc^2 $$`.
If you leave it inside a paragraph, it will produce an inline expression, just like $$ E = mc^2 $$.

To use display mode, again surround your expression with `$$` and place it as a separate paragraph.
Here is an example:

$$
\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
$$

Note that MathJax 3 is [a major re-write of MathJax](https://docs.mathjax.org/en/latest/upgrading/whats-new-3.0.html) that brought a significant improvement to the loading and rendering speed, which is now [on par with KaTeX](http://www.intmath.com/cg5/katex-mathjax-comparison.php).
### Our Innovative Approach to Enhance Reliability

***

## The Core of Our Research: Developing a New Technique and Dataset
### How We Created a Unique Sound Dataset
Citations are then used in the article body with the `<d-cite>` tag.
The key attribute is a reference to the id provided in the bibliography.
The key attribute can take multiple ids, separated by commas.

The citation is presented inline like this: <d-cite key="gregor2015draw"></d-cite> (a number that displays more information on hover).
If you have an appendix, a bibliography is automatically created and populated in it.

Distill chose a numerical inline citation style to improve readability of citation dense articles and because many of the benefits of longer citations are obviated by displaying more information on hover.
However, we consider it good style to mention author last names if you discuss something at length and it fits into the flow well — the authors are human and it’s nice for them to have the community associate them with their work.
### Simplifying Our Method for Better Sound Recognition

***

## Breaking New Ground: Testing and Results
### Comparative Analysis: Our Method vs. Traditional Approaches
Syntax highlighting is provided within `<d-code>` tags.
An example of inline code snippets: `<d-code language="html">let x = 10;</d-code>`.
For larger blocks of code, add a `block` attribute:

<d-code block language="javascript">
  var x = 25;
  function(x) {
    return x * x;
  }
</d-code>

**Note:** `<d-code>` blocks do not look good in the dark mode.
You can always use the default code-highlight using the `highlight` liquid tag:

{% highlight javascript %}
var x = 25;
function(x) {
  return x * x;
}
{% endhighlight %}
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