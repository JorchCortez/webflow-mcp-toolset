# Webflow Rich Text Field Structure

## Overview

This document describes the complete structure and formatting options available in Webflow's Rich Text fields, based on analysis of the "MCP test Article" which contains all available block types.

## Field Information

- **Field Type**: `RichText`

## Rich Text Block Types

### 1. Headings

All heading levels are supported from H1 to H6 and must be implemented accordingly:

```html
<h1 id="">Article title</h1>
<h2 id="">Article title</h2>
<h3 id="">Article title</h3>
<h4 id="">Article title</h4>
<h5 id="">Article title</h5>
<h6 id="">Article title</h6>
```

**Notes:**
- Each heading includes an empty `id` attribute for anchor linking
- Best practice: Use H2 and smaller for internal article content (per field help text), Always verify with user if there is an H1 in the site outside of the article content and if so bring the titles down to H2 or smaller to ensure we maintain the proper semantic structure of the page.

### 2. Text Blocks

#### Paragraph
```html
<p>lorem ipsum dolor sit amet</p>
```

#### Blockquote
```html
<blockquote>this is a quote!</blockquote>
```

### 3. Lists

#### Ordered List
```html
<ol>
    <li>list no 1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ol>
```

#### Unordered List
```html
<ul>
    <li>bullet lists now</li>
    <li>another</li>
    <li>final</li>
</ul>
```

### 4. Media Elements

#### Image Figure
```html
<figure class="w-richtext-figure-type-image w-richtext-align-center" 
        data-rt-type="image" 
        data-rt-align="center">
    <div>
        <img src="{image_url}" 
            loading="lazy" 
            alt="__wf_reserved_inherit">
    </div>
    <figcaption>footnote for the image</figcaption>
</figure>
```

**Image Attributes:**
- `class`: `w-richtext-figure-type-image w-richtext-align-center`
- `data-rt-type`: `"image"`
- `data-rt-align`: `"center"` (can be left, center, right)
- `loading`: `"lazy"`
- `alt`: Usually `"__wf_reserved_inherit"` or custom alt text
- `figcaption`: Optional caption text

#### Video Figure (YouTube Embed)
```html
<figure class="w-richtext-figure-type-video w-richtext-align-center" 
        style="padding-bottom:33.723653395784545%" 
        data-rt-type="video" 
        data-rt-align="center" 
        data-rt-max-width="" 
        data-rt-max-height="33.723653395784545%" 
        data-rt-dimensions="854:480" 
        data-page-url="{video_url}">
    <div>
        <iframe allowfullscreen="true" 
                frameborder="0" 
                scrolling="no" 
                src="{video_embed_url}" 
                title="Manage Your Entire Webflow Site With AI (MCP First Look)">
        </iframe>
    </div>
</figure>
```

**Video Attributes:**
- `class`: `w-richtext-figure-type-video w-richtext-align-center`
- `style`: Responsive padding-bottom percentage based on aspect ratio
- `data-rt-type`: `"video"`
- `data-rt-align`: `"center"` (can be left, center, right)
- `data-rt-dimensions`: Original video dimensions (width:height)
- `data-page-url`: Original video URL
- `data-rt-max-width`: Maximum width constraint
- `data-rt-max-height`: Maximum height percentage

### 5. Code Block

```html
<pre></pre>
```

**Notes:**
- Empty `<pre>` tags for code blocks
- Content can be added between the tags

### 6. Custom Embed

```html
<div data-rt-embed-type='true'>The info here is inside of a custom embed section</div>
```

**Attributes:**
- `data-rt-embed-type`: `'true'` (indicates custom embed)
- Content can include custom HTML, scripts, or other embeddable content

## Alignment Options

Most block types support alignment via data attributes:
- `data-rt-align="left"`
- `data-rt-align="center"`
- `data-rt-align="right"`

## CSS Classes

Webflow automatically applies specific CSS classes:
- `w-richtext-figure-type-image`: For image figures
- `w-richtext-figure-type-video`: For video figures
- `w-richtext-align-center`: For center alignment
- `w-richtext-align-left`: For left alignment (implied)
- `w-richtext-align-right`: For right alignment

## MCP Usage Guidelines

When creating or updating rich text content via MCP:

1. **Always include proper HTML structure** with opening and closing tags
2. **Use semantic HTML elements** (h1-h6, p, blockquote, etc.)
3. **Include required data attributes** for figures and embeds
4. **Maintain Webflow's CSS class conventions** for proper styling
5. **Use proper image URLs** from Webflow's CDN for images
6. **Include captions** in `<figcaption>` tags when needed
7. **Set appropriate aspect ratios** for video embeds

## Example Complete Rich Text Content

```html
<h2 id="">Introduction</h2>
<p>This is a paragraph with some introductory text.</p>

<blockquote>This is an important quote to highlight.</blockquote>

<h3 id="">Key Points</h3>
<ul>
    <li>First important point</li>
    <li>Second important point</li>
    <li>Third important point</li>
</ul>

<figure class="w-richtext-figure-type-image w-richtext-align-center" 
        data-rt-type="image" 
        data-rt-align="center">
    <div>
        <img src="https://cdn.prod.website-files.com/SITE_ID/IMAGE_ID_filename.jpg" 
             loading="lazy" 
             alt="Descriptive alt text">
    </div>
    <figcaption>Image caption explaining the visual</figcaption>
</figure>

<h3 id="">Technical Details</h3>
<pre>
// Code example
function example() {
    return "Hello World";
}
</pre>

<div data-rt-embed-type='true'>
    <!-- Custom HTML embed content -->
</div>
```

## Important Notes

1. **Image URLs**: Should use Webflow's CDN format: `https://cdn.prod.website-files.com/SITE_ID/FILE_ID_filename.ext` any other format may not render correctly or could lead to broken images.
2. **Video Embeds**: Calculate proper aspect ratios for responsive design
3. **Empty IDs**: Heading IDs are typically empty but can be populated for anchor links
4. **Alt Text**: Use `"__wf_reserved_inherit"` for Webflow's automatic alt text or provide custom alt text
5. **Nested Elements**: Some elements like figures contain nested divs and other elements
6. **Data Attributes**: Critical for Webflow's visual editor and styling system
