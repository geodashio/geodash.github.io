---
layout: example
category: examples
name: "Popups for WMS/WFS"
description: "Example of feature layer popups for WMS/WFS layers"
tags:
  - popups
group: popups
dashboard: /assets/dashboards/popups-wms.yml
https: false
schema: featurelayerspopup
---
{% raw %}
popup:
  title: "WFP Warehouse: {{ feature.attributes.whlocation }}"
  panes:
    - id: popup_overview
      tab: {label: Overview }
      fields:
        - { "attribute": whlocation, "label": "Location", "value": "{{ feature.attributes.whlocation }}" }
        - { "attribute": owner, "label": "Owner", "value": "{{ feature.attributes.ownerorg }}" }
        - { "attribute": status, "label": "Status", "value": "{{ feature.attributes.status }}" }
        - { "attribute": locprecision, "label": "Location Precision", "value": "{{ feature.attributes.locprecision }}" }
    - id: "popup_links"
      tab: { label: "Links" }
      fields:
        - { type: link, label: "WFP GeoNode", value: Home, url: "http://geonode.wfp.org/" }
        - { type: link, label: "WFP GeoNode", value: "{{ layer.title }}", url: "http://geonode.wfp.org/layers/geonode:wld_poi_warehouses_wfp" }
        - type: link
          label: "Logistics Cluster:"
          value: "Hurricane Matthew"
          url: "http://www.logcluster.org/sector/hurrimat16"
        - value: "{{ feature.geometry.lat | number : 4 }}, {{ feature.geometry.lon | number : 4 }}"
          type: link
          label: "OpenStreetMap"
          url: "https://www.openstreetmap.org/#map=15/{{ feature.geometry.lat }}/{{ feature.geometry.lon }}"
{% endraw %}
