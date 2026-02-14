# Projekt-Struktur und Dokumentation

## Übersicht der Projektdateien

```
grav-theme-learn2-blog/
├── .github/                          # GitHub-spezifische Konfiguration
│   ├── ISSUE_TEMPLATE/               # Issue-Templates
│   │   ├── bug_report.md             # Template für Bug-Reports
│   │   ├── feature_request.md        # Template für Feature-Requests
│   │   ├── question.md               # Template für Fragen
│   │   └── config.yml                # Issue-Konfiguration
│   └── PULL_REQUEST_TEMPLATE.md      # Template für Pull Requests
│
├── blueprints/                       # Admin-Panel Konfiguration
│   ├── blog.yaml                     # Blueprint für Blog-Übersicht
│   └── blog-item.yaml                # Blueprint für Blog-Posts
│
├── css/                              # Stylesheets
│   └── blog.css                      # Blog-spezifisches CSS
│
├── templates/                        # Twig-Templates
│   ├── blog.html.twig                # Blog-Übersichtsseite
│   ├── blog-item.html.twig           # Einzelner Blog-Post
│   └── partials/                     # Wiederverwendbare Template-Teile
│       └── blog-item.html.twig       # Blog-Post-Vorschau
│
├── .gitignore                        # Git ignorierte Dateien
├── BLOG_README.md                    # Detaillierte Blog-Nutzung
├── CHANGELOG.md                      # Versionshistorie
├── CONTRIBUTING.md                   # Beitrags-Richtlinien
├── INSTALL.md                        # Installationsanleitung
├── LICENSE                           # MIT Lizenz
├── README.md                         # Haupt-Dokumentation
└── SECURITY.md                       # Sicherheitsrichtlinien
```

## Dokumentations-Hierarchie

### Für neue Nutzer

1. **[README.md](README.md)** - Starte hier
   - Schneller Überblick
   - Features
   - Basis-Installation
   - Erste Schritte

2. **[INSTALL.md](INSTALL.md)** - Detaillierte Installation
   - Schritt-für-Schritt-Anleitung
   - Verschiedene Installationsmethoden
   - Konfiguration
   - Fehlerbehebung

3. **[BLOG_README.md](BLOG_README.md)** - Nutzung im Detail
   - Alle Features erklärt
   - Konfigurationsoptionen
   - Anpassungen
   - Best Practices

### Für Contributors

1. **[CONTRIBUTING.md](CONTRIBUTING.md)** - Wie beitragen
   - Code-Style
   - PR-Prozess
   - Testing
   - Richtlinien

2. **[CHANGELOG.md](CHANGELOG.md)** - Was ist neu
   - Versionshistorie
   - Breaking Changes
   - Upgrade-Hinweise

### Für Security

1. **[SECURITY.md](SECURITY.md)** - Sicherheit
   - Sicherheitslücken melden
   - Best Practices
   - Checklisten

## Template-Architektur

### Template-Hierarchie

```
base.html.twig (Learn2 Theme)
├── blog.html.twig (Blog-Übersicht)
│   └── partials/blog-item.html.twig (Post-Vorschau)
└── blog-item.html.twig (Einzelner Post)
```

### Template-Blöcke

Alle Templates erweitern `partials/base.html.twig` des Learn2 Themes:

**Verfügbare Blöcke:**

- `head` - HTML Head-Bereich
- `stylesheets` - CSS-Dateien
- `javascripts` - JavaScript-Dateien
- `sidebar` - Seitenleiste
- `body` - Body-Wrapper
- `topbar` - Top-Navigation
- `content` - Hauptinhalt
- `navigation` - Vor/Zurück-Navigation
- `footer` - Footer-Bereich

### Blueprint-Struktur

Blueprints definieren die Admin-Panel-Oberfläche:

```yaml
title: Template Name
'@extends':
    type: default
    context: blueprints://pages

form:
  fields:
    tabs:              # Tab-Organisation
      fields:
        content:       # Content-Tab
          fields:
            # Felder hier
        options:       # Options-Tab
          fields:
            # Felder hier
```

## CSS-Architektur

### Struktur

```css
/* 1. Blog-Liste */
#blog-listing { }
.blog-list-item { }
.list-blog-image { }
.list-blog-content { }
.list-blog-meta { }
.list-blog-summary { }

/* 2. Einzelner Post */
.blog-post { }
.post-meta { }
.featured-image { }
.post-content { }

/* 3. Responsive */
@media (max-width: 768px) { }
```

### Naming Convention

- **BEM-ähnlich**: `.blog-list-item`, `.list-blog-content`
- **Semantisch**: Beschreibende Klassennamen
- **Spezifisch**: Prefix `blog-` oder `list-blog-` oder `post-`

### Responsive Breakpoints

```css
/* Mobile First */
/* Base: Mobile (< 768px) */

@media (min-width: 768px) {
    /* Tablet */
}

@media (min-width: 1024px) {
    /* Desktop */
}

@media (min-width: 1200px) {
    /* Large Desktop */
}
```

## Entwicklungs-Workflow

### Lokale Entwicklung

1. **Setup:**

```bash
cd /pfad/zu/grav
bin/gpm install learn2
# Blog Extension installieren
```

1. **Entwicklungs-Server:**

```bash
php -S localhost:8000 system/router.php
```

1. **Twig-Debug aktivieren:**

```yaml
# user/config/system.yaml
twig:
  debug: true
  auto_reload: true
```

1. **CSS-Änderungen testen:**

```bash
# Cache nach CSS-Änderungen leeren
bin/grav clear-cache
```

### Git-Workflow

1. **Feature-Branch:**

```bash
git checkout -b feature/mein-feature
```

1. **Entwicklung:**

```bash
# Änderungen machen
git add .
git commit -m "Add: Feature-Beschreibung"
```

1. **Testing:**

- Teste in verschiedenen Browsern
- Teste responsive Design
- Teste mit/ohne Plugins

1. **Push und PR:**

```bash
git push origin feature/mein-feature
# Pull Request auf GitHub erstellen
```

### Testing-Checkliste

- [ ] Funktionalität in Chrome
- [ ] Funktionalität in Firefox
- [ ] Funktionalität in Safari (wenn möglich)
- [ ] Mobile Ansicht (Chrome DevTools)
- [ ] Tablet Ansicht
- [ ] Mit Pagination Plugin
- [ ] Ohne Pagination Plugin
- [ ] Mit Comments Plugin
- [ ] Ohne Comments Plugin
- [ ] Verschiedene Bildgrößen
- [ ] Posts mit/ohne Featured Images
- [ ] Posts mit/ohne Tags
- [ ] Cache aktiviert
- [ ] Cache deaktiviert
- [ ] Grav 1.6
- [ ] Grav 1.7+

## Datenfluss

### Blog-Übersicht

```
blog.md (Frontmatter)
    ↓
blog.html.twig
    ↓
page.collection() → Posts sammeln
    ↓
for-loop → partials/blog-item.html.twig
    ↓
HTML Output
```

### Einzelner Post

```
blog-item.md (Frontmatter)
    ↓
blog-item.html.twig
    ↓
page.header.* → Metadaten
page.content → Inhalt
page.media → Bilder
    ↓
HTML Output
```

## Erweiterungs-Punkte

### Neue Features hinzufügen

1. **Custom Fields:**

```yaml
# In blueprints/blog-item.yaml
header.reading_time:
  type: number
  label: Lesezeit (Minuten)
```

1. **Template anpassen:**

```twig
{# In templates/blog-item.html.twig #}
{% if page.header.reading_time %}
<span class="reading-time">
    <i class="fa fa-clock"></i> {{ page.header.reading_time }} Min. Lesezeit
</span>
{% endif %}
```

1. **Styling hinzufügen:**

```css
/* In css/blog.css */
.reading-time {
    color: #666;
    font-size: 0.9rem;
}
```

### Plugin-Integration

Beispiel: Related Posts Plugin

```twig
{# In templates/blog-item.html.twig nach content #}
{% if config.plugins.relatedpages.enabled %}
<div class="related-posts">
    <h3>Ähnliche Artikel</h3>
    {% include 'partials/relatedpages.html.twig' %}
</div>
{% endif %}
```

## Performance-Optimierung

### Caching-Strategie

```yaml
# user/pages/blog/blog.md
cache_enable: true
process:
  twig: true
```

### Image-Optimierung

```twig
{# Responsive Images #}
{% set blog_image = page.media[page.header.featured_image] %}
{{ blog_image.cropZoom(1200, 600).quality(85).html() }}

{# Oder mit srcset #}
<img 
  src="{{ blog_image.cropZoom(800, 400).url }}"
  srcset="{{ blog_image.cropZoom(400, 200).url }} 400w,
          {{ blog_image.cropZoom(800, 400).url }} 800w,
          {{ blog_image.cropZoom(1200, 600).url }} 1200w"
  sizes="(max-width: 768px) 100vw, 800px"
  alt="{{ page.title }}"
>
```

## Versionierung

Folgt [Semantic Versioning](https://semver.org/):

- **MAJOR** (1.0.0): Breaking Changes
- **MINOR** (0.1.0): Neue Features (rückwärtskompatibel)
- **PATCH** (0.0.1): Bugfixes

## Support und Community

- **GitHub Issues**: Bug-Reports und Feature-Requests
- **GitHub Discussions**: Allgemeine Fragen und Diskussionen
- **Grav Forum**: Community-Support
- **Grav Discord**: Echtzeit-Chat

## Lizenz

Dieses Projekt ist unter der MIT-Lizenz lizenziert - siehe [LICENSE](LICENSE) für Details.

---

**Hinweis**: Diese Dokumentation wird kontinuierlich aktualisiert. Für die neueste Version siehe GitHub.
