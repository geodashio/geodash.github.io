---
title: Quick Start
layout: single
---

### Goal

This quick start guide will help users easily create geospatial dashboards, using the existing GeoDash Viewer, a simple `html` page that will render dashboards from YAML configuration **without having to write any new code**.

### Setup

You can either (1) use the public hosted GeoDash Viewer at [https://viewer.geodash.io](https://viewer.geodash.io) or (2) fork [geodash-viewer](https://github.com/geodashio/geodash-viewer) on GitHub and host the page yourself.  If you'd like to learn more about the internal mechanics of GeoDash, get in contact with <a href="mailto:pjdufour.dev@gmail.com">pjdufour.dev@gmail.com</a>.

**Note on HTTPS**

The public hosted viewer at **viewer.geodash.io** supports http and https.  Depending on the context, you should use http or https.  For example, if visualizing data from a GeoNode that only supports **HTTP** you'll need to use **HTTP** too.  If using the geolocation API, then you'll need to use **HTTPS**.  For the quick start guide, we'll stick with **HTTP**, since we won't be using geolocation.

### The Basics

In GeoDash, dashboards are configured with a single human-readable [YAML](http://yaml.org/) or JSON file.  GeoDash has an initialization routine that will **render** the configuration into a full geospatial dashboard.  GeoDash is agnostic to how the configuration file is created.  It can be created manually, as we'll do now, or computed automatically by a server.

In a location that is on the same domain or accessible to the viewer using [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS), create a `quickstart.yml` file.  If using the public GeoDash Viewer, than I'd suggest creating a [gist](https://gist.github.com/) on GitHub.

All the steps in the quickstart guide are stored in a gist at [https://gist.github.com/pjdufour/7f66ad8889e912ec124527faa9d173a1](https://gist.github.com/pjdufour/7f66ad8889e912ec124527faa9d173a1).  You can either follow along or just use YAML files stored in the public gist.

The entire schema for GeoDash configuration files is accessible at [https://geodash.io/schema](https://geodash.io/schema), which you can consult during and after the quick start guide.  The schema will include additional example snippets.  Consult the [examples](https://geodash.io/examples) page for live examples.

Create the following `quickstart.yml`, and include the following.

### Step 1: OSM

In the first configuration file add the following:

```
---

title: "Quick Start Step 1"
view:
  baselayer: osm
  featurelayers: []
  latitude: 18.7360
  longitude: -72.4178
  maxZoom: 18
  minZoom: 0
  zoom: 7
  controls: []
controls:
  attribution: false
  legend: false
  zoom: false
renderlayers:
  - osm
baselayers:
  - id: osm
    title: OpenStreetMap
    description: OpenStreetMap Basemap, Standard Style
    source:
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>'
      name: OpenStreetMap
      tile:
        url: https://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png
      type: tiles
featurelayers: []
overlays: []
```

To render the dashboard, simply append a link to the YAML configuration file after **?main:config=**, e.g., **http://viewer.geodash.io?main:config=<url of your yaml file>**.  You should now see an OSM map!  You can edit the **view** configuration to change the location of your dashboard.

**Live**

[Step 1 Live](http://viewer.geodash.io/?main:config=https://gist.githubusercontent.com/pjdufour/7f66ad8889e912ec124527faa9d173a1/raw/e6a495fff1ee10f271bbc2ee7351712e6d90ffc4/geodash_quick_start_step_1.yml)

### Step 2: Adding Feature Layers

There are 2 types of layers in GeoDash: base layers and feature layers.  OSM is a **base layer**.  We'll now add one **feature layer** of WFP warehouses.  A baselayer is not interactive.  You can click on and otherwise interact with a feature layer.  A feature layer can pull data from a `wms`, `wfs`, `vector tile`, or other source.  You can see the full range of feature layer options in the [schema](https://geodash.io/schema#featurelayers).

We'll make a few changes.  First, we'll add a new configuration block under **featurelayers:**, which describes how to load the WMS layer.  We'll also need to add the layer to the **view.featurelayers** and **renderlayers:** variables.  The **view** block describes the initial state of the geospatial dashboard on load.  The **renderlayers** block describes how to order the layers.  For example, show a WMS point layer on top of a WMS polygon layer.  In OpenLayers 3, you can layer WMS on top of GeoJSON, so this block exposes that functionality.  In renderlayers, the first/top layer is the highest is the stack.  As such, OSM as the baselayer is last/bottom.

```
---

title: "Quick Start Step 2"
view:
  baselayer: osm
  featurelayers:
    - wld_poi_warehouses_wfp
  latitude: 18.7360
  longitude: -72.4178
  maxZoom: 18
  minZoom: 0
  zoom: 7
  controls: []
controls:
  attribution: false
  legend: false
  zoom: false
renderlayers:
  - wld_poi_warehouses_wfp
  - osm
baselayers:
  - id: osm
    title: OpenStreetMap
    description: OpenStreetMap Basemap, Standard Style
    source:
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>'
      name: OpenStreetMap
      tile:
        url: https://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png
      type: tiles
featurelayers:
  - id: wld_poi_warehouses_wfp
    type: WMS
    title: "Global WFP Warehouses"
    description: "This layer contains locations and additional information of WFP warehouses worldwide."
    source:
      name: "WFP"
      attribution: "WFP GeoNode"
      site: "WFP GeoNode"
    wms:
      version: "1.1.1"
      layers: ["geonode:wld_poi_warehouses_wfp"]
      styles: []
      format: 'image/png'
      transparent: true
      buffer: 256
      url: "http://geonode.wfp.org/cors/geoserver/geonode/wms"
    wfs:
      version: "1.0.0"
      url: "http://geonode.wfp.org/cors/geoserver/wfs"
      geometry: shape
overlays: []
```

Update the link after **?main:config=** as needed.  You should now see a layer of WFP Warehouses on top of your OSM basemap.

**Live**

[Step 2 Live](http://viewer.geodash.io/?main:config=https://gist.githubusercontent.com/pjdufour/7f66ad8889e912ec124527faa9d173a1/raw/e6a495fff1ee10f271bbc2ee7351712e6d90ffc4/geodash_quick_start_step_2.yml)


### Step 3: Adding Popups

We'll now add a simple popup to our WFP Warehouses layer.  You can read more about popups in the schema at [http://geodash.io/schema/#featurelayerspopup](http://geodash.io/schema/#featurelayerspopup).

Add a **popup** block under the feature layer.  In this block you can set the popup title and fields.  You can specify whatever fields are most useful.  Additionally, these fields can be short template snippets.  For example {% raw %}`{{ feature.geometry.lon | number : 4 }}`{% endraw %} to round the longitude to only 4 decimal places.  You can use all the built-in Angular filters and the custom filters at [https://github.com/geodashio/geodash-plugin-filters](https://github.com/geodashio/geodash-plugin-filters) in your popup templates.  In addition to showing feature attribute information, you can also show links to external resources, such as the relevant page on [WFP GeoNode](http://geonode.wfp.org).

```
---

title: "Quick Start Step 3"
view:
  baselayer: osm
  featurelayers:
    - wld_poi_warehouses_wfp
  latitude: 18.7360
  longitude: -72.4178
  maxZoom: 18
  minZoom: 0
  zoom: 7
  controls: []
controls:
  attribution: false
  legend: false
  zoom: false
renderlayers:
  - wld_poi_warehouses_wfp
  - osm
baselayers:
  - id: osm
    title: OpenStreetMap
    description: OpenStreetMap Basemap, Standard Style
    source:
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>'
      name: OpenStreetMap
      tile:
        url: https://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png
      type: tiles
featurelayers:
  - id: wld_poi_warehouses_wfp
    type: WMS
    title: "Global WFP Warehouses"
    description: "This layer contains locations and additional information of WFP warehouses worldwide."
    source:
      name: "WFP"
      attribution: "WFP GeoNode"
      site: "WFP GeoNode"
    wms:
      version: "1.1.1"
      layers: ["geonode:wld_poi_warehouses_wfp"]
      styles: []
      format: 'image/png'
      transparent: true
      buffer: 256
      url: "http://geonode.wfp.org/cors/geoserver/geonode/wms"
    wfs:
      version: "1.0.0"
      url: "http://geonode.wfp.org/cors/geoserver/wfs"
      geometry: shape
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
            - { type: link, label: "WFP GeoNode", value: "{{ layer.title }}", url: "http://geonode.wfp.org/layers/geonode:wld_poi_warehouses_wfp" }
            - type: link
              label: "Logistics Cluster:"
              value: "Hurricane Matthew"
              url: "http://www.logcluster.org/sector/hurrimat16"
            - value: "{{ feature.geometry.lat | number : 4 }}, {{ feature.geometry.lon | number : 4 }}"
              type: link
              label: "OpenStreetMap"
              url: "https://www.openstreetmap.org/#map=15/{{ feature.geometry.lat }}/{{ feature.geometry.lon }}"
overlays: []
```

Update the link after **?main:config=** as needed.  You should now be able to click on the layers and get a popup.  Be sure to be using a **http** verison of the viewer rather than **https**, since the WFP GeoNode WFS only support **http**.

**Live**

[Step 3 Live](http://viewer.geodash.io/?main:config=https://gist.githubusercontent.com/pjdufour/7f66ad8889e912ec124527faa9d173a1/raw/e6a495fff1ee10f271bbc2ee7351712e6d90ffc4/geodash_quick_start_step_3.yml)


### Step 4: Adding Navbars

GeoDash has a fully-customizabel navbars implementation, which can be used for bookmarking locations, a toolbar, or more.  We'll now add 2 simple navbars: (1) a toolbar and (2) location bookmarks.

You can consult the schema at [https://geodash.io/schema/#navbars](https://geodash.io/schema/#navbars) to learn more about navbars.  You can configure the CSS and more, which we won't cover in the quick start guide.

```
---

title: "Quick Start Step 4"
view:
  baselayer: osm
  featurelayers:
    - wld_poi_warehouses_wfp
  latitude: 18.7360
  longitude: -72.4178
  maxZoom: 18
  minZoom: 0
  zoom: 7
  controls: []
controls:
  attribution: false
  legend: false
  zoom: false
renderlayers:
  - wld_poi_warehouses_wfp
  - osm
baselayers:
  - id: osm
    title: OpenStreetMap
    description: OpenStreetMap Basemap, Standard Style
    source:
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>'
      name: OpenStreetMap
      tile:
        url: https://{a-c}.tile.openstreetmap.org/{z}/{x}/{y}.png
      type: tiles
featurelayers:
  - id: wld_poi_warehouses_wfp
    type: WMS
    title: "Global WFP Warehouses"
    description: "This layer contains locations and additional information of WFP warehouses worldwide."
    source:
      name: "WFP"
      attribution: "WFP GeoNode"
      site: "WFP GeoNode"
    wms:
      version: "1.1.1"
      layers: ["geonode:wld_poi_warehouses_wfp"]
      styles: []
      format: 'image/png'
      transparent: true
      buffer: 256
      url: "http://geonode.wfp.org/cors/geoserver/geonode/wms"
    wfs:
      version: "1.0.0"
      url: "http://geonode.wfp.org/cors/geoserver/wfs"
      geometry: shape
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
            - { type: link, label: "WFP GeoNode", value: "{{ layer.title }}", url: "http://geonode.wfp.org/layers/geonode:wld_poi_warehouses_wfp" }
            - type: link
              label: "Logistics Cluster:"
              value: "Hurricane Matthew"
              url: "http://www.logcluster.org/sector/hurrimat16"
            - value: "{{ feature.geometry.lat | number : 4 }}, {{ feature.geometry.lon | number : 4 }}"
              type: link
              label: "OpenStreetMap"
              url: "https://www.openstreetmap.org/#map=15/{{ feature.geometry.lat }}/{{ feature.geometry.lon }}"
overlays: []
navbars:
  - id: toolbar
    placement: top
    tabs:
      - title: "WFP Warehouses"
        value: toggle_wfp_warehouses
        tooltip: { placement: top, content: "Toggle WFP Warehouses" }
        intents:
          - name: toggleFeatureLayer
            properties: [{ name: layer, value: "wld_poi_warehouses_wfp" }]
      - title: "Reset Extent"
        value: reset_extent
        tooltip: { placement: top, content: "Reset Extent" }
        intents:
          - name: flyToExtent
            properties: [{"name": "extent", "value": "initial"}]
  - id: locations
    placement: bottom
    intents:
      - name: stateChanged
        properties: [{ name: location, value: "{{ tab.value }}" }]
      - name: flyToLocation
        properties:
          - { name: lat, value: "{{ tab.lat }}" }
          - { name: lon, value: "{{ tab.lon }}" }
          - { name: zoom, value: "{{ tab.zoom }}" }
          - { name: projection, value: "{{ tab.projection }}" }
    switch: "state.location"
    tabs:
      - title: "Toussaint Louverture International Airport"
        value: airport
        tooltip: { placement: top, content: "Toussaint Louverture International Airport" }
        lat: 18.5802
        lon: -72.2862
        zoom: 15
        projection: "EPSG:4326"
      - title: Carrefour
        value: carrefour
        tooltip: { placement: top, content: "Carrefour, Haiti" }
        lat: 18.5348
        lon: -72.4098
        zoom: 12
        projection: "EPSG:4326"
      - title: Jérémie
        value: jeremie
        tooltip: { placement: top, content: "Jérémie, Haiti" }
        lat: 18.64462
        lon: -74.11377
        zoom: 17
        projection: "EPSG:4326"
```

**Live**

[Step 4 Live](http://viewer.geodash.io/?main:config=https://gist.githubusercontent.com/pjdufour/7f66ad8889e912ec124527faa9d173a1/raw/e6a495fff1ee10f271bbc2ee7351712e6d90ffc4/geodash_quick_start_step_4.yml)

### Step 5: Adding Overlays

TBD

### Step 6:

TBD
