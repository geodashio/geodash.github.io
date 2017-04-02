---
layout: example
category: examples
name: "Carto / Symbolizer Transform Operations"
description: "Example on using transform operations for carto symbolizers."
tags:
  - carto
  - geojson
group: carto
dashboard: /assets/dashboards/carto-symbolizer-transform-operations.yml
https: false
schema: featurelayerscartostylessymbolizerstransform
---

- id: buffer
  type: polygon
  title: Buffer Symbolizer
  description: Buffer Symbolizer
  static:
    properties:
      fillColor: '#FF8C00'
      fillOpacity: 0.4
      strokeColor: '#444444'
      strokeWidth: 1.0
  transform:
    operations:
      - name: buffer
        properties:
        - name: distance
          value: 1000
