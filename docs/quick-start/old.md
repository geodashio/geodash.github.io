
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
