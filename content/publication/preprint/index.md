---
title: "Unsupervised brain MRI image registration based on hybrid ViT and convolutional U-net"
authors:
- admin
- Feng Liu
- Shu Shi
- Guowei Tao
- Fu Zhou
author_notes:
- ""
- "Corresponding authour"
- ""
- ""
- ""
date: "2023-05-05T23:00:00Z"
doi: ""

# Schedule page publish date (NOT publication's date).
publishDate: "2023-05-05T23:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["3"]

# Publication name and optional abbreviated publication name.
publication: "Scientific Reports"
publication_short: "srep, preprint"

abstract: During a patient’s disease progression, MRIs scaned in different times need to be registered before and after. However, the location and structure of tissue inside the human body may change with the growth of illnesses, interfering with the physician’s ability to quickly diagnose the progression of the disease. To reach this goal, we proposed a hybrid ViT and convolutional U-net for brain MRI image registration, which achieved a higher dice score than ViT-V-Net and VoxelMorph. In the meantime, we have had an idea of a novel loss function for gray image registration called grad-loss, which concentrates on the difference and gradient at each voxel of the MRI image. Quantitative and qualitative comparison results demonstrate that our model outperforms the previous ViT-based and convolution-based networks and achieved a better dice score of 79.7% in OASIS dataset.

# Summary. An optional shortened abstract.
summary: We proposed a hybrid ViT and convolutional U-net for brain MRI image registration, which achieved a higher dice score than ViT-V-Net and VoxelMorph. Quantitative and qualitative comparison results demonstrate that our model outperforms the previous ViT-based and convolution-based networks and achieved a better dice score of 79.7% in OASIS dataset.

tags:
- Source Themes
featured: false

links:
# - name: Custom Link
#   url: http://example.org
url_pdf: ""
url_code: 'https://github.com/wjy-yy/Hybrid-net'
# url_dataset: '#'
# url_poster: '#'
# url_project: ''
# url_slides: ''
# url_source: '#'
# url_video: '#'

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/s9CC2SKySJM)'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
- internal-project

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---

{{% callout note %}}
Create your slides in Markdown - click the *Slides* button to check out the example.
{{% /callout %}}

Supplementary notes can be added here, including [code, math, and images](https://wowchemy.com/docs/writing-markdown-latex/).
