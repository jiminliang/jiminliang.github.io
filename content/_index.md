---
# Leave the homepage title empty to use the site title
title:
date: 2022-10-24
type: landing

sections:
  - block: slider
    content:
      slides:
      - title:  AI for Science and Engineering
        content: We develop and apply novel artificial intelligence methods to see the unseen using optics, electromagnetism and electronics, and to understand what is seen. 
        align: center
        background:
          image:
            filename: image-human-eye-process-scanning.jpg
            filters:
              brightness: 0.7
          position: right
          color: '#666'
        link:
          text: Current Studies
          url: ../research/
      - title: Research in progress
        content: 'Our current research focuses on brain-computer fusion for advanced computer vision, human behaviour analysis, and performance evaluation of AI-based systems, with an emphasis on tackling data limitations using AIGC techniques.'
        align: left
        background:
          image:
            filename: BCI.jpg
            filters:
              brightness: 0.7
          position: center
          color: '#555'
      - title: Previous studies
        content: 'Our previous studies focused on optical tomography for molecular imaging and auroral image analysis.'
        align: left
        background:
          image:
            filename: aurora.jpg
            filters:
              brightness: 0.7
          position: center
          color: '#333'
    design:
      # Slide height is automatic unless you force a specific height (e.g. '400px')
      slide_height: ''
      is_fullscreen: true
      # Automatically transition through slides?
      loop: false
      # Duration of transition between slides (in ms)
      interval: 2000
---
