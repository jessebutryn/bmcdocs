# BMC Tools Documentation

This repository contains documentation for various BMC (Baseboard Management Controller) tools from different vendors.

## 🌐 Live Site

The documentation is live at: **[https://bmcdocs.pages.dev/](https://bmcdocs.pages.dev/)**

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/jessebutryn/bmcdocs.git
   cd bmcdocs
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

   This will install:
   - MkDocs (static site generator)
   - Material theme (for better styling)
   - Awesome Pages plugin (for automatic navigation)

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

## Project Structure

```
bmcdocs/
├── docs/                    # Documentation source files
│   ├── index.md            # Home page
│   ├── dell/               # Dell tools documentation
│   └── supermicro/         # Supermicro tools documentation
├── mkdocs.yml              # MkDocs configuration
├── requirements.txt        # Python dependencies
└── README.md              # This file
```

## Supported Tools

- **Dell RACADM**: Remote Access Controller Admin utility for Dell PowerEdge servers
- **Supermicro SUM**: Supermicro Update Manager for firmware updates
- **Supermicro SAA**: SuperServer Automation Assistant for system management

## Contributing

Add new documentation by creating Markdown files in the `docs/` directory. The navigation is automatically generated using the Awesome Pages plugin.

### Adding New Tool Documentation

1. Create a new directory under `docs/` for the vendor/tool
2. Add Markdown files with documentation
3. The navigation will update automatically

## Features

- 📱 Responsive design with dark/light mode toggle
- 🔍 Full-text search
- 📖 Clean, organized navigation
- 🎨 Material Design theme
- ⚡ Fast static site generation