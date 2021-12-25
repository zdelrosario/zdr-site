---
authors:
- admin
categories:
- Teaching
date: "2021-12-25:00:00Z"
draft: false
featured: false
image:
  caption: 'Image credit: Zachary del Rosario'
  focal_point: ""
  placement: 2
  preview_only: false
lastmod: "2021-12-25:00:00Z"
projects: []
subtitle: ''
summary: A brief introduction to exploratory model analysis.
tags:
- Data Science
- Exploratory Model Analysis
title: 'Exploratory Model Analysis: A Brief Introduction'
---
# Exploratory Model Analysis: An Introduction



```python
import grama as gr
DF = gr.Intention()
```

Setup



```python
from grama.models import make_cantilever_beam
md_beam = make_cantilever_beam()
md_beam
```




    model: Cantilever Beam
    
      inputs:
        var_det:
          w: [2, 4]
          t: [2, 4]
    
        var_rand:
          H: (+1) norm, {'loc': 500.0, 'scale': 100.0}
          V: (+1) norm, {'loc': 1000.0, 'scale': 100.0}
          E: (+0) norm, {'loc': 29000000.0, 'scale': 1450000.0}
          Y: (-1) norm, {'loc': 40000.0, 'scale': 2000.0}
    
        copula:
          Independence copula
    
      functions:
          cross-sectional area: ['w', 't'] -> ['c_area']
          limit state: stress: ['w', 't', 'H', 'V', 'E', 'Y'] -> ['g_stress']
          limit state: displacement: ['w', 't', 'H', 'V', 'E', 'Y'] -> ['g_disp']



Sinews (ceteris paribus) plot



```python
(
    md_beam
    >> gr.ev_sinews(df_det="nom")
    >> gr.pt_auto()
)
```

    Calling plot_sinew_outputs....



    
![png](/media/ema-intro_files/ema-intro_5_1.png)
    





    <ggplot: (8777835322621)>



# Endnotes

