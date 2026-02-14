# Copilot Instructions: Learn2 Blog Extension

## Project Overview

This is a **Grav CMS theme extension** that adds full blog functionality to the Learn2 documentation theme. It's NOT a standalone theme but extends an existing theme by adding templates, blueprints, and styles.

**Key Architecture Decision**: Files are designed to be copied INTO `user/themes/learn2/` directory of an existing Grav installation, not used as a separate theme. This means templates extend Learn2's base structure.

## Template System (Twig)

### Template Hierarchy
```
partials/base.html.twig (from Learn2)
├── blog.html.twig (blog listing)
└── blog-item.html.twig (single post)
```

### Critical Patterns

**Always extend Learn2's base:**
```twig
{% extends 'partials/base.html.twig' %}
```

**Override specific blocks, not whole templates:**
- `{% block content %}` - main content area
- `{% block navigation %}` - prev/next links
- Never override `head`, `sidebar`, or `body` blocks (breaks Learn2 integration)

**Grav Collections** (NOT simple loops):
```twig
{# CORRECT: Use Grav's collection system #}
{% for child in page.collection().order('date', 'desc') %}

{# WRONG: Don't iterate page.children directly #}
{% for child in page.children %}
```

**Featured Images** (Grav-specific):
```twig
{# Access via page.media[] with header key #}
{% if page.header.featured_image %}
    <img src="{{ page.media[page.header.featured_image].url }}">
{% endif %}

{# Can also use first image #}
{% set blog_image = page.media.images|first %}
```

**Plugin detection** (always check if enabled):
```twig
{% if config.plugins.pagination.enabled and page.collection().params.pagination %}
    {% include 'partials/pagination.html.twig' %}
{% endif %}
```

## Blueprints (Admin Panel Config)

Located in `blueprints/*.yaml`, these define admin UI fields. Key pattern:

```yaml
'@extends':
    type: default
    context: blueprints://pages  # Inherit Grav's base page blueprint

form:
  fields:
    tabs:
      fields:
        content:
          type: tab
          fields:
            header.my_field:  # Prefix with 'header.' to store in page frontmatter
              type: text
```

**Critical**: Field names like `header.subtitle` map directly to frontmatter YAML `subtitle:` in markdown files.

## CSS Architecture

**Naming Convention**: BEM-inspired with component prefixes
- `.blog-*` - Blog-wide styles
- `.list-blog-*` - Blog listing specific
- `.post-*` - Single post specific

**Mobile-first responsive**:
```css
/* Base styles for mobile */
.blog-list-item article { display: block; }

/* Desktop overrides */
@media (min-width: 768px) {
    .blog-list-item article { display: flex; }
}
```

**Integration point**: CSS must be manually added to `user/themes/learn2/templates/partials/base.html.twig`:
```twig
{% do assets.addCss('theme://css/blog.css',100) %}
```

## Frontmatter Conventions

Blog overview page (`blog.md`):
```yaml
template: blog
content:
    items: '@self.children'  # Grav collection syntax
    order:
        by: date
        dir: desc
```

Blog post (`blog-item.md`):
```yaml
template: blog-item
author: Name
date: 14.02.2026
featured_image: header.jpg  # Filename in same folder
taxonomy:
    category: [Tech, Tutorial]
    tag: [grav, cms]
```

## Development Workflow

**No build process**: Direct Twig/CSS editing. After changes:
```bash
bin/grav clear-cache  # ALWAYS clear cache after template/blueprint changes
```

**Testing checklist**:
1. Test WITH pagination plugin enabled/disabled
2. Test WITH comments plugin enabled/disabled
3. Test WITH breadcrumbs plugin enabled/disabled
4. Test responsive breakpoints (768px, 1024px)
5. Test with/without featured images

## Common Pitfalls

❌ **DON'T** create new base template - extends Learn2's base
❌ **DON'T** use WordPress/Jekyll patterns - this is Grav
❌ **DON'T** forget `|raw` filter for `page.content` (Markdown → HTML)
❌ **DON'T** hardcode URLs - use `{{ page.url }}` and `{{ base_url }}`
❌ **DON'T** add npm/build tools - keep it simple file-based

✅ **DO** check plugin existence before including partials
✅ **DO** use Grav's media system for images (`page.media[]`)
✅ **DO** clear cache frequently during development
✅ **DO** test both admin panel AND file-based workflows

## Integration Points

- **Learn2 Theme**: Templates extend `partials/base.html.twig`
- **FontAwesome**: Already loaded by Learn2 (use `<i class="fa fa-*">`)
- **Pagination Plugin**: Optional, detected via `config.plugins.pagination.enabled`
- **Comments Plugin**: Optional, detected via `config.plugins.comments.enabled`
- **Breadcrumbs Plugin**: Optional, detected via `config.plugins.breadcrumbs.enabled`

## File Locations

When developing/testing in actual Grav installation:
- Templates → `user/themes/learn2/templates/`
- Blueprints → `user/themes/learn2/blueprints/`
- CSS → `user/themes/learn2/css/`
- Content → `user/pages/blog/` (example blog pages)

## Documentation Structure

For context on features:
- `README.md` - User-facing features and quick setup
- `DOCUMENTATION.md` - Technical architecture (THIS file's companion)
- `CONTRIBUTING.md` - Code style and PR conventions
- `INSTALL.md` - Detailed installation steps

When adding features, update all relevant docs, especially CHANGELOG.md following semver conventions.
