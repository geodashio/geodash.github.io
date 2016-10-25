---
title: Quick Start
layout: single
---

### The Basics

In GeoDash dashboards are configured with a single human-readable [YAML](http://yaml.org/).  We'll first create the yaml file and then the html page it goes in.

At runtime, GeoDash will assume many sensible defaults when no configuraiton is given.  For example, when no `base layer` is given, GeoDash will load `OSM`.

Please create a new directory called `quickstart` to contain [quickstart.yml]({{ site.baseurl }}/docs/quick-start/quickstart.yml) and [quickstart.html]({{ site.baseurl }}/docs/quick-start/quickstart.html).

Create the following `quickstart.yml`, and include the following.

```
view:
  latitude: 12
  longitude: 12
  minZoom: 0
  maxZoom: 18
  zoom: 6
  baselayer: osm
  featurelayers:
    - roads
    - buildings

```

Create the following `quickstart.html` in the same directory.

```
<head>
  <title>GeoDash Quick Start</title>
  <script src="http:///static/geodashserver/build/js/geodashserver.full.min.js?v=0.0.8"></script>
</head>
<body>
  <div
    id="main"
    class="geodash-main"
    data-geodash-dashboard-url="quickstart.yml">
  </div>
</body>
```

Now load `quickstart.html` in your browser.  A map should now appear with OSM!  Change the yaml and refresh to adjust the location.

### State

We've created a basic configuration, but sometimes you'll want to adjust the `state` of the application based on users, groups, time of day, etc.  Within runtime, `state` refers to the location of the viewport, which layers are visible, etc.  You can configure an initial state, which will adjust the map on load.  That way you can have one configuration file for multiple scenarios, when only the center point is changing, etc.

```
data-geodash-dashboard-initial-state-url="quickstart-state.yml"
```

For more robust applications, you can provide an initial state via API or render directly to the page using templates.

### Adding Feature Layers

Now we'll add some queryable layers for roads and buildings to the dashboard.  Queryable layers are considered `feature layers` within GeoDash.  Feature Layers can also be styled, have popups, events, etc.

### Popups

You can add customizable popups to layers in GeoDash.  GeoDash provides a high degree of customizability above most standard GIS implementations

Specifically, GeoDash allows dashboard owners to use Angular filters.  Therefore, not all popups are the same small hard to read boxes.

With this flexibility, you can also create small to show a human readable field name (rather than the internal name or cut-off shapefile version).

```

featurelayer
  - id: buildings
    ...
    popup:
      title: Building {{ attributes.name }}
```


All together, GeoDash provides the ability to delivered tailored content for popups, maintaining a high-degree of value-add.
