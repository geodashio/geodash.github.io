GeoDash Website (geodash.github.io)
================

## Description

The main website for GeoDash

## Installation

To create a development virtual machine, use [https://github.com/geodashio/geodash-website-devops](https://github.com/geodashio/geodash-website-devops).

**Extensionless Permalinks**

```
# http://jekyllrb.com/docs/permalinks/#extensionless-permalinks
try_files $uri $uri.html $uri/ =404;
```

Also, see [http://rickharrison.me/how-to-remove-trailing-slashes-from-jekyll-urls-using-nginx](http://rickharrison.me/how-to-remove-trailing-slashes-from-jekyll-urls-using-nginx).

## Usage

Use Jekyll Serve with the following line.  Include `-H 0.0.0.0` so the host machine can access the site.

```
jekyll serve -H 0.0.0.0
```

## Examples

TBD

## Contributing

We are currently accepting pull requests.  Please include a detailed description in the pull request as needed.

```
git push upstream gh-pages
```

## License

TBD
