# Architecture

Please take a look at the following post on Medium to understand the perspective informing the design philosophy.

https://medium.com/@pjdufour.dev/introducing-geodash-18f1d68bd6f5#.tg7ieg569

## Design Philosophy

At it's core, GeoDash is built to be extremely extensible.  This has important impacts on how it is constructed within 2 facets: `runtime` and `source`.

During `runtime` in the browser, the top-level component is a `dashboard`.  Everything flows from dashboards.  JSON/YAML configuration is `attached` to dashboards.  Within dashboards, you'll find the maps, charts, tables, etc.

During `source`, the code is distributed into `projects` and within projects are `plugins`.  In most cases, a `project` represents the top-level application level.  This is similiar to the Django construct of `projects` and `apps`.  Plugins can reside locally within a project's codebase or can be referenced by uri (`file:///` or `http://`).  Within plugins, you'll find the actual executable code, including `controllers`, `directives, ``templates`, etc.  This flexibility allows the developer to distribute or consolidate code in whatever way is easiest to maintain and enhance.  There are no artifical requirements for consolidation or distribution for that matter.

You can design your application or platform as needed.

## Key Terms

### Dashboard

A dashboard is the top level `runtime` object of a GeoDash application.  Within a dashboard are all the maps, charts, etc.

### Base Layer

A base layer is a layer on a map that covers the entirety of the map extent.  Base layers cannot be queried.

### Feature Layer

A feature layer is similar to a base layer, but there are two key differences.  First, a feature layer need not cover the entirety of the map extent.  Second, a feature layer is queryable, stylable, and other wise can be interacted with via popups, etc.

### Scope

`Scope` refers to an [AngularJS scope](https://docs.angularjs.org/guide/scope).  Scopes are used for managing application state and for passing messages between components.

### Project

A project is the top level `source code` construct of a GeoDash appliation.  A project is made up of a list of `plugins`

### Plugin

A plugin is the second level `source code` construct of a GeoDash application.  A project is made up of a list of `plugins`

### Controller

A controller is an [AngularJS controller](https://docs.angularjs.org/guide/controller).

### Directive

A directive is an [AngularJS directive](https://docs.angularjs.org/guide/directive).
