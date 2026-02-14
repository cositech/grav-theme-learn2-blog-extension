# Blog Template für Learn2 Theme

Dieses Template erweitert das Learn2 Theme um vollständige Blog-Funktionalität.

## Enthaltene Dateien

### Templates
- `templates/blog.html.twig` - Haupttemplate für die Blog-Übersichtsseite
- `templates/blog-item.html.twig` - Template für einzelne Blog-Posts
- `templates/partials/blog-item.html.twig` - Partial für Blog-Einträge in der Übersicht

### Blueprints
- `blueprints/blog.yaml` - Blueprint für die Blog-Übersichtsseite
- `blueprints/blog-item.yaml` - Blueprint für einzelne Blog-Posts

### Styling
- `css/blog.css` - CSS-Styling für das Blog-Template

## Installation

1. Kopiere die Dateien in dein Learn2 Theme-Verzeichnis:
   - Templates nach `user/themes/learn2/templates/`
   - Blueprints nach `user/themes/learn2/blueprints/`
   - CSS nach `user/themes/learn2/css/`

2. Füge das Blog-CSS in die `custom.css` ein oder lade es in `base.html.twig`:
   ```twig
   {% do assets.addCss('theme://css/blog.css',100) %}
   ```

## Verwendung

### Blog-Hauptseite erstellen

1. Erstelle eine neue Seite im Admin-Panel oder als Markdown-Datei
2. Wähle das Template "Blog" aus
3. Beispiel Frontmatter (`blog.md`):

```yaml
---
title: Mein Blog
subtitle: Neuigkeiten und Artikel
template: blog
content:
    items: '@self.children'
    order:
        by: date
        dir: desc
    limit: 10
    pagination: true
---

Willkommen in meinem Blog! Hier findest du regelmäßig neue Artikel.
```

### Blog-Posts erstellen

1. Erstelle Unterseiten in deinem Blog-Ordner
2. Wähle das Template "Blog Item" aus
3. Beispiel Frontmatter (`01.mein-erster-post/blog-item.md`):

```yaml
---
title: Mein erster Blog-Post
template: blog-item
author: Max Mustermann
date: 14.02.2026
featured_image: header.jpg
taxonomy:
    category:
        - Technologie
        - Tutorial
    tag:
        - Grav
        - CMS
        - Web Development
---

Dies ist der Inhalt meines ersten Blog-Posts...

===

Dies ist die Zusammenfassung, die in der Blog-Übersicht angezeigt wird.
```

## Features

### Blog-Übersicht
- Automatische Auflistung aller Blog-Posts
- Sortierung nach Datum (neueste zuerst)
- Anzeige von Featured Images
- Zusammenfassungen mit "Weiterlesen"-Button
- Pagination-Unterstützung
- Autor, Datum, Tags und Kategorien

### Einzelner Blog-Post
- Featured Image Support
- Autor-Informationen
- Veröffentlichungsdatum
- Tags und Kategorien mit Links
- Vor/Zurück-Navigation
- Kommentar-Support (wenn Plugin aktiviert)
- Responsive Design

### Metadaten

Verfügbare Header-Optionen für Blog-Posts:

```yaml
title: Post-Titel             # Pflichtfeld
author: Autor-Name            # Optional
date: 14.02.2026              # Optional, Standard: Erstellungsdatum
featured_image: bild.jpg      # Optional, Dateiname des Featured Images
subtitle: Untertitel          # Optional (nur für Blog-Übersicht)
published: true               # Optional, Standard: true
taxonomy:                     # Optional
    category: [Cat1, Cat2]
    tag: [Tag1, Tag2, Tag3]
```

## Anpassung

### Styling anpassen

Bearbeite `css/blog.css` um das Aussehen anzupassen:
- Farben
- Schriftarten
- Abstände
- Layout

### Template-Anpassung

Die Templates können nach Bedarf angepasst werden:
- `blog.html.twig` - Übersichtsseite
- `blog-item.html.twig` - Einzelne Posts
- `partials/blog-item.html.twig` - Post-Vorschau

### Featured Images

Um Featured Images zu verwenden:
1. Lade das Bild in den Seiten-Ordner des Posts hoch
2. Setze den Dateinamen im Header:
   ```yaml
   featured_image: mein-bild.jpg
   ```

## Kompatibilität

- Grav CMS 1.6+
- Learn2 Theme
- Optional: Pagination Plugin
- Optional: Comments Plugin
- Optional: Breadcrumbs Plugin

## Tipps

1. **Zusammenfassungen**: Verwende `===` im Markdown, um eine Zusammenfassung zu definieren:
   ```markdown
   Zusammenfassung...
   
   ===
   
   Vollständiger Inhalt...
   ```

2. **Taxonomien**: Nutze Tags und Kategorien für bessere Organisation

3. **Pagination**: Aktiviere das Pagination Plugin für große Blogs

4. **SEO**: Füge Meta-Beschreibungen in den Header ein:
   ```yaml
   metadata:
       description: 'Beschreibung des Posts'
   ```

## Support

Bei Fragen oder Problemen kannst du:
- Die Grav-Dokumentation konsultieren: https://learn.getgrav.org
- Das Learn2 Theme-Repository besuchen: https://github.com/getgrav/grav-theme-learn2
