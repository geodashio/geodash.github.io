---
layout: example
category: examples
name: "Carto / Simple"
description: "Simple Example of styling a GeoJSON layer client-side"
tags:
  - carto
  - geojson
group: carto
dashboard: /assets/dashboards/carto-simple.yml
https: false
schema: featurelayerscarto
---

carto:
  styles:
    - id: default
      title: Default Style
      description: Default Style
      symbolizers:
        - id: default
          title: Default Symbolizer
          description: Default Symbolizer
          type: point
          static:
            properties:
              fillColor: "#AA0000"
              fillOpacity: 0.6
              strokeWidth: 1.0
              strokeColor: "#330000"
