---
layout: example
category: examples
name: "Popups for GeoJSON layer"
description: "Example of feature layer popups for GeoJSON layers"
tags:
  - popups
group: popups
dashboard: /assets/dashboards/popups-geojson.yml
https: false
schema: featurelayerspopup
---
{% raw %}
popup:
  title: "Airport: {{ feature.attributes.namelong }}"
{% endraw %}
