# BMC Tools Documentation

This repository contains documentation for various BMC (Baseboard Management Controller) tools from different vendors.

## Setup

1. Install MkDocs:
   ```bash
   pip install mkdocs
   ```

2. Install Material theme (optional, for better styling):
   ```bash
   pip install mkdocs-material
   ```

## Building the Site

To build the static site:
```bash
mkdocs build
```

## Serving Locally

To serve the site locally for development:
```bash
mkdocs serve
```

The site will be available at `http://localhost:8000`

## Contributing

Add new documentation by creating Markdown files in the `docs/` directory and updating the navigation in `mkdocs.yml`.

## Supported Tools

- Dell RACADM
- Supermicro SUM
- Supermicro SAA

More tools can be added as needed.