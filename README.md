# bluefin-help
Example linux yelp-based help documentation, using `yelp-tools` for freedesktop.org compliant linux help.

Mallard is used for documentation markup language.

## Instructions

### Dev Container
Open this project using the given devcontainer specification

### Building

It is recommended to build this in a Distrobox or Toolbx container.

#### Dependencies:
- `make` (for building)
- `yelp-tools`
- `yelp`

Download this repo and extract the archive to a preferrred location.

```bash
cd /path/to/bazzite-help-main/
```

```bash
make
```

Output file will be `index.epub`

### Reading Help File

From the host:

```bash
cd /path/to/bazzite-help-main/docs
```

```bash
yelp .
```

### References Directory

These are translated from the [Discourse documentation](https://universal-blue.discourse.group/docs?category=6) using [html2mallard](https://pypi.org/project/html2mallard/).  Personally, I cherry pick from these reference files.

### Cleaning

```bash
make clean
```
