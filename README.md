# Webflow MCP Toolset

A comprehensive set of prompts, documentation, and context files designed to enhance your workflow when using the Webflow Model Context Protocol (MCP) with AI assistants like GitHub Copilot.

## 📋 Overview

This repository provides standardized documentation and guidelines to help AI assistants work more effectively with Webflow sites through the Model Context Protocol.  By maintaining these context files, you ensure consistent and compliant modifications across your Webflow projects. 

## 🗂️ Documentation

All documentation files are located in the `.github/webflow/` directory:

### Core Documentation

- **[mcp-capabilities.md](. github/webflow/mcp-capabilities.md)** - Overview of Webflow MCP capabilities and available operations
- **[rich-text-docs.md](.github/webflow/rich-text-docs.md)** - Guidelines for properly modifying rich text elements in Webflow
- **[seo-strategy.md](.github/webflow/seo-strategy.md)** - SEO strategy guidelines and requirements for Webflow sites
- **[cms-erd.md](.github/webflow/cms-erd.md)** - CMS entity relationship diagrams and data structure documentation
- **[llms-txt-standards.md](.github/webflow/llms-txt-standards.md)** - Standards for LLM-readable text formatting

## 🚀 Usage

### With GitHub Copilot

When using GitHub Copilot with Webflow MCP, Copilot will automatically reference the documentation in `.github/webflow/` before making modifications to your Webflow site.

For example:
- **Rich text modifications** → Consults `rich-text-docs.md`
- **SEO strategy generation** → Follows guidelines in `seo-strategy.md`
- **CMS structure changes** → References `cms-erd.md`

### Adding Copilot Instructions

You can add the following instructions to your Copilot workspace to ensure compliance:

```
Whenever you are using Webflow's Model Context Protocol (MCP) and are about to modify specific things in a site, you must reference the files within the `.github/webflow/` directory. These files may contain important guidelines or requirements that need to be applied to the content you support or modify.

If requested to generate an SEO strategy based on a specific site, FIRST try to find the site using Webflow's MCP, if you find it then ensure you follow the instructions in the `seo-strategy.md` file located in `.github/webflow/`.

Always check for relevant documentation in `.github/webflow/` before making changes to ensure compliance with project-specific standards and practices.
```

## 📁 Repository Structure

```
webflow-mcp-toolset/
├── .github/
│   └── webflow/
│       ├── cms-erd.md
│       ├── llms-txt-standards.md
│       ├── mcp-capabilities.md
│       ├── rich-text-docs.md
│       └── seo-strategy.md
├── . vscode/
└── README.md
```

## 🎯 Benefits

- **Consistency**:  Ensures all AI-assisted modifications follow project standards
- **Compliance**: Maintains adherence to SEO and content guidelines
- **Efficiency**: Reduces back-and-forth by providing clear context upfront
- **Documentation**: Serves as a central knowledge base for Webflow MCP operations

## 🛠️ Customization

You can customize the documentation files in `.github/webflow/` to match your specific: 
- Brand guidelines
- SEO requirements
- CMS structure
- Content formatting rules
- Rich text styling preferences

## 📖 Getting Started

1. Clone this repository or use it as a template
2. Customize the documentation files in `.github/webflow/` to match your project needs
3. Configure your AI assistant to reference these files when working with Webflow MCP
4. Start building and modifying your Webflow sites with consistent, guided AI assistance

## 🤝 Contributing

Feel free to contribute improvements to the documentation templates or add new context files that would benefit Webflow MCP workflows.

## 📄 License

This project is provided as-is for use with Webflow MCP integrations. 

## 🔗 Related Resources

- [Webflow API Documentation](https://developers.webflow.com/)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [GitHub Copilot Documentation](https://docs.github.com/copilot)

---

**Note**: This toolset is designed to work alongside Webflow's MCP and AI assistants that support the Model Context Protocol. 
