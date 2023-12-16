---
title: Contact
date: 2023-12-16

type: landing

sections:
  - block: contact
    content:
      title: Contact
      text: |-
        Leave a message if you have any questions.
      email: jiminliang@gmail.com
      phone: +86-2988202251
      address:
        street: 2 South Taibai Road
        city: Xi'an
        region: Shaanxi
        postcode: '710071'
        country: China
        country_code: CN
      coordinates:
        latitude: '34.14'
        longitude: '108.55'
      directions: Office 234, the administration building.
      office_hours:
        - 'Monday 10:00 to 13:00'
        - 'Wednesday 09:00 to 10:00'
      # appointment_url: 'https://calendly.com'
      #contact_links:
      #  - icon: comments
      #    icon_pack: fas
      #    name: Discuss on Forum
      #    link: 'https://discourse.gohugo.io'
    
      # Automatically link email and phone or display as text?
      autolink: true
    
      # Email form provider
      form:
        provider: netlify
        formspree:
          id:
        netlify:
          # Enable CAPTCHA challenge to reduce spam?
          captcha: false
    design:
      columns: '1'

  - block: markdown
    content:
      title:
      subtitle: ''
      text:
    design:
      columns: '1'
      background:
        image: 
          filename: colormeans.jpg
          filters:
            brightness: 1
          parallax: false
          position: center
          size: cover
          text_color_light: true
      spacing:
        padding: ['20px', '0', '20px', '0']
      css_class: fullscreen
---
