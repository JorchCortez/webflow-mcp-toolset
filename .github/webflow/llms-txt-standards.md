# LLMs.txt Standards for Webflow MCP Generation

## Overview

This document establishes standards for generating high-quality `/llms.txt` files using Webflow's Model Context Protocol (MCP). The llms.txt standard (https://llmstxt.org/) provides LLM-friendly website content to improve SEO and AIO (AI Optimization).

## When to Generate llms.txt

Generate an llms.txt file when:
- A user requests SEO optimization that includes AI/LLM discoverability
- A site needs better AI agent integration
- Documentation sites require LLM-friendly content access
- Business sites want to improve AI search engine compatibility
- Personal/portfolio sites need better AI assistant integration

## Required Webflow MCP Data Collection Process

### 1. Site Discovery
```
MUST use: mcp_webflow_sites_get(site_id)
- Get site name, URL, description
- Identify primary domain or webflow.io subdomain
```

### 2. Page Content Analysis
```
MUST use: mcp_webflow_pages_list(site_id)
THEN: mcp_webflow_pages_get_content(page_id) for each important page
- Collect all published pages (skip drafts)
- Extract headings, content, and structure
- Identify key navigation and page hierarchy
```

### 3. CMS Content Discovery
```
MUST use: mcp_webflow_collections_list(site_id)
THEN: mcp_webflow_collections_items_list_items(collection_id) for each collection
- Discover all CMS collections (blogs, portfolios, products, etc.)
- Get sample items from each collection
- Understand content types and relationships
```

### 4. Component Analysis
```
SHOULD use: mcp_webflow_components_list(site_id)
- Identify reusable components
- Understand site structure patterns
```

## llms.txt Format Requirements

### File Structure (MUST follow exactly)

```markdown
# [Site Name]

> [Concise site description with key value proposition and purpose]

[Optional detailed context paragraphs about the site, business, or project]

## [Section Name]

- [Page Title](URL): Brief description of page content

## [Content Type Section]

- [Content Title](URL): Description

## Optional

- [Secondary Resource](URL): Less critical information
- [External Link](URL): Related external resources
```

### Required Sections

1. **H1 Header**: Site/project name (REQUIRED)
2. **Blockquote Summary**: Key information for understanding the site (REQUIRED)
3. **Optional Context**: Detailed information paragraphs (OPTIONAL)
4. **H2 Sections**: Categorized content lists (REQUIRED - at least one)
5. **Optional Section**: Secondary information that can be skipped (OPTIONAL)

## Content Prioritization Strategy

### High Priority (Include in main sections)
- **Homepage**: Always include as primary reference
- **About/Company Pages**: Core business information
- **Services/Products**: Key offerings
- **Documentation**: If technical site
- **Blog/News**: Recent important content (max 10 most recent)
- **Contact**: Business contact information

### Medium Priority (Include if space allows)
- **Team/Staff**: Key personnel information
- **Case Studies**: Success stories
- **FAQ**: Common questions
- **Pricing**: Service/product pricing
- **Careers**: Job opportunities

### Low Priority (Optional section)
- **Policies**: Privacy, terms, legal
- **Archives**: Older blog posts
- **Testimonials**: Customer reviews
- **Press**: Media mentions
- **Technical Docs**: Detailed technical references

## Webflow-Specific Content Handling

### Page Content Extraction
```
From mcp_webflow_pages_get_content():
- Extract H1-H6 headings for page summaries
- Get first 2-3 paragraphs for descriptions
- Identify key call-to-action content
- Note any forms or interactive elements
```

### CMS Content Processing
```
From CMS collections:
- Blog Posts: Include 5-10 most recent with dates
- Products: Include main product categories
- Portfolio: Include recent work samples
- Events: Include upcoming events
- Team: Include key personnel
```

### URL Construction
```
Base URL formats:
- Custom domain: https://example.com/page-slug
- Webflow subdomain: https://sitename.webflow.io/page-slug
- Collection items: https://example.com/collection-slug/item-slug
```

## Content Guidelines

### Language and Style
- **Concise**: Keep descriptions under 50 words each
- **Clear**: Avoid jargon unless it's a technical site
- **Informative**: Include key benefits/purposes
- **Professional**: Match site's tone
- **Actionable**: Help LLMs understand how to use the content

### Link Descriptions Format
```
- [Page Name](URL): What this page covers and why it's useful
- [Blog Post Title](URL): Key topic and takeaway (Date if relevant)
- [Product Name](URL): What it does and who it's for
```

### Section Organization
```
Recommended section order:
1. Core Pages (About, Services, Products)
2. Content (Blog, News, Resources)  
3. Business Info (Contact, Pricing, Team)
4. Documentation (if applicable)
5. Optional (Policies, Archives)
```

## Quality Assurance Checklist

### Before Generation
- [ ] Collected site metadata and structure
- [ ] Analyzed all published pages
- [ ] Reviewed CMS collections and content
- [ ] Identified site's primary purpose and audience
- [ ] Confirmed custom domain or webflow.io URL

### Content Validation
- [ ] H1 matches site name exactly
- [ ] Blockquote captures core value proposition
- [ ] All URLs are valid and publicly accessible
- [ ] Descriptions are informative and concise
- [ ] Sections are logically organized
- [ ] No duplicate content or URLs

### Format Compliance
- [ ] Follows exact markdown structure
- [ ] Uses proper H1 and H2 headers only
- [ ] Blockquote is properly formatted
- [ ] All links use `[text](url)` format
- [ ] Optional section is appropriately used
- [ ] File size is reasonable (typically under 2KB)

## Example Template

```markdown
# [Site Name from Webflow]

> [Site description combining site purpose, target audience, and key value proposition based on homepage and about page content]

[Optional: Additional context about the business, project scope, or unique aspects discovered from content analysis]

## Core Pages

- [Homepage Title](URL): Main landing page with [key elements found]
- [About Page Title](URL): Company/project background and mission
- [Services/Products Page](URL): [Brief description of offerings]

## Content

- [Recent Blog Post](URL): [Topic and key insights] (Date)
- [Important Resource](URL): [What it provides and audience]
- [Case Study/Portfolio](URL): [What it demonstrates]

## Business Information

- [Contact Page](URL): Contact details and location information
- [Pricing Page](URL): Service costs and packages (if applicable)
- [Team Page](URL): Key personnel and expertise

## Optional

- [Privacy Policy](URL): Data handling and privacy information
- [Terms of Service](URL): Usage terms and conditions
- [Site Archive](URL): Historical content and older posts
```

## Implementation Workflow

1. **Data Collection**: Use Webflow MCP tools to gather comprehensive site data
2. **Content Analysis**: Process and prioritize content based on importance
3. **Structure Planning**: Organize content into logical sections
4. **Draft Generation**: Create initial llms.txt following format requirements
5. **Quality Review**: Validate against checklist and standards
6. **Optimization**: Refine descriptions and organization
7. **Final Validation**: Ensure compliance with llmstxt.org specification

## Success Metrics

A well-generated llms.txt file should:
- Be immediately useful to LLMs for understanding the site
- Provide clear pathways to key information
- Represent the site's full scope and value
- Enable effective AI agent interaction
- Improve discoverability in AI-powered search tools

## Common Pitfalls to Avoid

- **Incomplete data collection**: Skipping CMS content or important pages
- **Generic descriptions**: Using vague language instead of specific value props
- **Wrong URL formats**: Using internal or draft URLs instead of public ones
- **Format violations**: Not following the exact markdown structure
- **Information overload**: Including too many links without prioritization
- **Outdated content**: Referencing old or archived content in main sections

---

*Standards based on llmstxt.org specification v1.0*  
*Created for Webflow MCP integration workflows*  
*Last updated: September 16, 2025*
