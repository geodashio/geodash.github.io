---
layout: example
category: examples
name: "Vector Tiles"
description: "Example of loading and styling vector tiles"
tags:
  - carto
  - "vector tiles"
group: simple
dashboard: /assets/dashboards/vector-tiles.yml
schema: featurelayersmapzen
---
{% raw %}
featurelayers:
  - id: roads
    type: mapzen
    title: "Roads"
    description: "Roads from Mapzen vector tile service"
    source: { name: "Mapzen", attribution: "Mapzen" }
    maxZoom: 15
    mapzen:
      version: "v1"
      layers: ["roads"]
      format: "mvt"
      api_key: "mapzen-KthQho3"
{% endraw %}
