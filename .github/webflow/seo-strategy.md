# Webflow MCP SEO Sweep

## What the agent does

* Enumerates all published pages. Skips drafted pages.
* Reads each page’s visible content and headings.
* Proposes a meta title and description that meet character limits.
* Builds JSON-LD for the site and for each page. Avoids duplicate blocks.
* Generates a keyword strategy at the site level and per page.
* Writes a single machine-friendly markdown plan that you can edit.
* Applies only pages you approve. Re-runs are idempotent.

---

## Inputs the agent should infer or ask once

* `site_name` and `base_url` from the site settings or home page.
* Primary entity: `Organization` or `Person`. Prefer Organization unless clearly a personal brand.
* `sameAs` profiles from header, footer, or existing JSON-LD.
* Presence of on-site search to add `SearchAction`.

If any item cannot be inferred, the agent asks once, records the answer in the `site:` block, and proceeds.

---

## Page selection rules

* Include only pages with `published=true`.
* For CMS templates, prefer dynamic tokens in patterns. If MCP cannot use tokens, the agent generates per-item proposals for top traffic items when feasible.

---

## Meta title and description rules

**Title**

* Format: `<SITE NAME> | <Concise Page Label>`.
* Max 60 characters. If longer, shorten the page label, then abbreviate the site name.
* No duplicates across pages.
* Home page variant allowed: `<SITE NAME> | <Short USP>` if still under 60.

**Description**

* Max 160 characters.
* Clear, specific, benefit-forward.
* One primary keyword included. No stuffing.
* Unique per page.

---

## Schema rules

Always provide:

* `WebSite` with `url`, `name`. Include `SearchAction` when a search route exists.
* Top-level entity: `Organization` or `Person`.
* Per page: `WebPage` with `name`, `url`, `description`, `isPartOf` → `WebSite`, `dateModified`.

Add specialized types when detected:

* Blog post: `BlogPosting` or `Article` with `headline`, `author`, `datePublished`, `image`.
* Product: `Product` with `offers` and `aggregateRating` when present.
* Software product: `SoftwareApplication`.
* Service page: `Service` with `provider`.
* Local business: `LocalBusiness` or subtype with address, geo, phone, hours.
* FAQ section present: `FAQPage` with QAPairs.
* About page: `AboutPage`. Contact page: `ContactPage`. Collection index: `CollectionPage`.
* Event info: `Event` with `location`, `startDate`, `endDate`.

Merge with existing JSON-LD where possible. Prefer a single consolidated `<script type="application/ld+json">` per page. Set `lastReviewed` to current ISO date.

**Schema file generation:**
* Create separate `/webflow/seo/{site_name}/SCHEMAS.md` file containing all schema markup
* Each page schema should include page identifier, URL, and complete JSON-LD
* Keep SEO-PLAN.md focused on titles, descriptions, and keywords only
* Use site name to create dedicated folder for multi-site management

---

## Keyword strategy rules

Method without external APIs:

* Parse H1/H2/H3, first two paragraphs, button text, image alt, nav, breadcrumbs, CMS tags.
* Extract noun phrases and 1 to 3-word terms. Remove brand and stopwords. Normalize plurals.
* Score candidates by frequency, heading prominence, and presence in anchor text.
* Classify search intent: informational, transactional, navigational, local.
* Estimate difficulty and opportunity qualitatively (low, medium, high). If you later add an API, the fields accept real numbers.

Recommendations per page:

* 1 primary keyword.
* 3 to 6 secondary keywords.
* Intent, difficulty, opportunity.
* Internal link targets (hubs) and sources (supporting pages).
* Cannibalization risk if another page targets the same primary.
* Concrete content actions to improve coverage and CTR.

---

## Validations and safeguards

* Enforce character limits: 60 for titles, 160 for descriptions.
* No duplicate titles or descriptions across pages.
* Do not overwrite pages that are not `approved`.
* Idempotent apply step. Re-running does not duplicate JSON-LD.
* Use UTC ISO timestamps for `generated_at`, `lastReviewed`, and `applied_at`.

---

## `/webflow/seo/{site_name}/SEO-PLAN.md` structure

The agent will generate a file `/webflow/seo/{site_name}/SEO-PLAN.md`. Then it will fill fields on first run. User must review and edit. Then you approve and apply.

````markdown
# SEO Plan

> Edit this file, approve items, then run the apply step. The agent only applies pages with `status: approved`.

## Summary

version: "1.1"
generated_at: "YYYY-MM-DDThh:mm:ssZ"
site_url: "https://example.com"
discovery_summary:
  discovered_pages: 0
  skipped_pages: 0
  skipped:
    # - path: "/search"   reason: "system page"
collisions:
  # Records any duplicate title or description proposals the agent found
  # - type: "title" page: "/services" collides_with: "/solutions"


## Site

site:
  name: "<SITE NAME>"
  base_url: "https://example.com"
  entity_type: "Organization"   # or "Person"
  same_as:
    # Add or let the agent infer
    # - "https://linkedin.com/in/<handle>"
    # - "https://github.com/<handle>"
    # - "https://x.com/<handle>"

  global_schema:
    # Edit these fields to customize your site's global schema
    website_name: "<SITE NAME>"
    website_url: "https://example.com"
    has_search: false  # Set to true if site has search functionality
    search_url_pattern: ""  # e.g., "https://example.com/search?q={search_term_string}"
    
    entity_type: "Organization"  # or "Person"
    entity_name: "<SITE NAME>"
    entity_url: "https://example.com"
    entity_logo: ""  # URL to logo image
    entity_description: ""  # Brief description of entity
    
    # For Person entities, add:
    person_job_title: ""
    person_location_city: ""
    person_location_country: ""
    person_image: ""  # URL to profile image
    
    # For Organization entities, add:
    org_logo: ""
    org_address_street: ""
    org_address_city: ""
    org_address_state: ""
    org_address_country: ""
    org_phone: ""
    org_email: ""


## Keyword Strategy

keyword_strategy:
  methodology: "Headings + first paragraphs + anchors + alt text. Noun-phrase extraction. Deduped. Intent classification. Difficulty and opportunity estimated qualitatively."
  topic_clusters:
    - cluster: "Core Services"
      hub: "/services"
      rationale: "Commercial pages that drive conversions"
      pages: ["/services", "/pricing", "/contact"]
    - cluster: "Education"
      hub: "/blog"
      rationale: "Informational content that supports service pages"
      pages: ["/blog", "/blog/how-to-example", "/blog/category/example"]
  guardrails:
    - "One primary keyword per page"
    - "Avoid duplicate primaries across pages"
    - "Use hubs for internal links from informational posts to commercial pages"

## Pages

> Edit each page block. Flip `status` to `approved` to allow applying. Leave `applied_at` empty; the agent will fill it.

pages:
  - path: "/"
    webflow_id: "<id-or-empty>"
    detected_type: "HomePage"   # WebPage, AboutPage, ContactPage, BlogPosting, Product, Service, FAQPage, etc.
    h1: "<Detected or preferred H1>"

    keywords:
      primary: "<primary keyword>"
      secondary: ["<secondary 1>", "<secondary 2>", "<secondary 3>"]
      intent: "transactional"   # informational | transactional | navigational | local
      difficulty: "medium"      # low | medium | high (qualitative)
      opportunity: "high"       # low | medium | high (qualitative)
      internal_links_to: ["/services", "/pricing", "/contact"]
      internal_links_from: ["/blog/what-is-<topic>", "/blog/best-practices-<topic>"]
      cannibalization_risk: "low"
      content_actions:
        - "Tighten value prop in first 100 words"
        - "Add 3 benefit bullets above the fold"
        - "Include FAQ block for common objections"

    proposed:
      title: "<SITE NAME> | <USP or Core Service>"
      title_char_count: 0
      description: "Short, specific, benefit-forward. Under 160 chars."
      description_char_count: 0

    status: "proposed"          # proposed | approved | applied
    notes: "Rationale for the chosen primary keyword"
    applied_at: ""              # Filled by agent on apply

  - path: "/about"
    webflow_id: "<id-or-empty>"
    detected_type: "AboutPage"
    h1: "About <SITE NAME>"

    keywords:
      primary: "about <brand>"
      secondary: ["our team", "mission", "values"]
      intent: "informational"
      difficulty: "low"
      opportunity: "medium"
      internal_links_to: ["/contact", "/careers"]
      internal_links_from: ["/", "/blog/*"]
      cannibalization_risk: "low"
      content_actions:
        - "Add leadership section with concise bios"
        - "Add Organization schema fields if missing"

    proposed:
      title: "<SITE NAME> | About"
      title_char_count: 0
      description: "Clear summary of who you are and why it matters. Under 160 chars."
      description_char_count: 0

    status: "proposed"
    notes: ""
    applied_at: ""

## Page Block Template (copy this for new pages)

# --- PAGE BLOCK TEMPLATE ---
- path: "/<slug>"
  webflow_id: "<id-or-empty>"
  detected_type: "WebPage"
  h1: "<Detected or preferred H1>"

  keywords:
    primary: "<primary keyword>"
    secondary: ["<secondary 1>", "<secondary 2>", "<secondary 3>", "<secondary 4>"]
    intent: "informational"
    difficulty: "medium"
    opportunity: "medium"
    internal_links_to: []
    internal_links_from: []
    cannibalization_risk: "low"
    content_actions: []

  proposed:
    title: "<SITE NAME> | <Concise Page Label>"
    title_char_count: 0
    description: "<under 160 chars>"
    description_char_count: 0

  //Please set to approved when done
  status: "proposed"
# --- END TEMPLATE ---

## Guidelines the agent must follow
validations:
    enforce_title_limit: 60
    enforce_description_limit: 160
    unique_titles: true
    unique_descriptions: true
    approved_only: true
    idempotent_apply: true
    single_jsonld_block_per_page: true
    set_lastReviewed_iso: true
    exclusions:
    skip_drafts: true
    skip_system_pages: ["404", "search", "password", "rss"]
## Apply and verify steps

**Apply**
1. Re-read `/webflow/seo/{site_name}/SEO-PLAN.md` and `/webflow/seo/{site_name}/SCHEMAS.md`.
2. For each page with `status: approved`:
   - Update Webflow SEO title and description. 
   - Mark the page `status: applied` and set `applied_at` timestamp.
   - Mark the schemas from updated pages from SCHEMAS.md for the user to add on each page (this is not currently an operation that the mcp can perform)

**Schema Generation**
1. Generate `/webflow/seo/{site_name}/SCHEMAS.md` with format:
   ```
   # Page Schemas
   
   ## Global Schemas
   
   ### Website Schema
   ```json
   {global website schema}
   ```
   
   ### Entity Schema  
   ```json
   {organization or person schema}
   ```
   
   ## Page Schemas
   
   ### Homepage
   - **Page**: Homepage
   - **URL**: /
   - **Schema**:
   ```json
   {page schema here}
   ```
   
   ### About Page
   - **Page**: About
   - **URL**: /about  
   - **Schema**:
   ```json
   {page schema here}
   ```
   ```
- Mark the page `status: applied` and set `applied_at` timestamp.


**Verify**
1. Fetch each updated page.
2. Confirm that title and meta description match the plan.
3. Validate JSON-LD parses cleanly and contains required types.
4. List success and any errors in a short report.

---