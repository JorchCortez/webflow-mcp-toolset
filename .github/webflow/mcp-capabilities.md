# MCP Capabilities and Limitations

This document outlines the tools available to GitHub Copilot when working with Webflow's Model Context Protocol (MCP), as well as any important limitations to be aware of.

## Available Tools

- **Site Management**: List, retrieve, and update site metadata, domains, and publishing status.
- **Page Management**: List, retrieve, and update static and CMS pages, including SEO and Open Graph settings, and localized content.
- **CMS Collections**: List, create, update, and delete CMS collections and their fields (static, option, reference, multi-reference).
- **CMS Items**: List, create, update, publish, and delete items within collections, including support for localization and draft/live status.
- **Components**: List, retrieve, and update components and their content/properties, including localization support.
- **Scripts**: Register, list, and delete inline scripts for sites (with character and location restrictions).
- **Publishing**: Publish sites to custom domains and Webflow subdomains.


## Custom Code Capabilities
- Add inline code to site (global only)
- Remove inline code from site (global only)
- List all registered scripts
- List all applied scripts

## Limitations
- Per-page custom code is not supported via MCP. All custom code is applied globally to the entire site. This is explicitly stated in the official [Webflow MCP Server documentation](https://github.com/webflow/mcp-server).

- **Field Types**: Only the following field types are supported for CMS fields:
	- PlainText
	- RichText
	- Number
	- Image
	- MultiImage
	- Video
	- File
	- Link
	- Email
	- Phone
	- DateTime
	- Color
	- Switch
	- Option (with predefined choices)
	- Reference (single and multi-reference to other collections)
	Attempting to use unsupported field types will result in errors.
- **Script Size**: Inline scripts are limited to 2000 characters.
- **Localization**: Some endpoints require locale IDs and may not support all localization features.
- **Bulk Operations**: Some actions (like item creation or update) are limited in batch size (typically 100 items per request).
- **Content Structure**: When updating content (e.g., rich text), you must follow any project-specific guidelines (see `rich-text-docs.md`).
- **Permissions**: Actions are limited by the permissions of the authenticated user and the capabilities of the MCP API.
- **No Visual Editing**: Copilot cannot visually edit or preview the site; all changes are made via API and must be verified in Webflow Designer or on the live site.

Always consult the documentation in `.github/webflow/` for project-specific requirements before making changes.
