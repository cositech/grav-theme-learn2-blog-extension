# Learn2 Blog Extension

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Grav](https://img.shields.io/badge/Grav-1.6%2B-blue.svg)](https://getgrav.org)

Eine professionelle Blog-Erweiterung für das [Grav Learn2 Theme](https://github.com/getgrav/grav-theme-learn2), die vollständige Blog-Funktionalität hinzufügt.

## Features

- 📝 **Blog-Übersichtsseite** mit automatischer Post-Auflistung
- 📄 **Einzelne Blog-Posts** mit vollständiger Formatierung
- 🖼️ **Featured Images** Support
- 👤 **Autor-Informationen** und Veröffentlichungsdaten
- 🏷️ **Tags und Kategorien** mit automatischen Links
- ◀️▶️ **Navigation** zwischen Posts (Vor/Zurück)
- 📱 **Responsive Design** für alle Geräte
- 💬 **Kommentar-Integration** (wenn Plugin aktiviert)
- 📄 **Pagination** Support für große Blogs
- 🎨 **Nahtlose Integration** in das Learn2 Theme-Design

## Screenshots

### Blog-Übersicht

Zeigt alle Blog-Posts mit Featured Images, Metadaten und Zusammenfassungen.

### Einzelner Blog-Post

Vollständige Darstellung mit Navigation, Featured Image, Tags und Kategorien.

## Voraussetzungen

- Grav CMS 1.6 oder höher
- Learn2 Theme installiert

## Installation

### Manuelle Installation

1. **Repository klonen oder herunterladen:**

   ```bash
   cd user/themes/learn2
   ```

2. **Dateien kopieren:**
   - Kopiere den Inhalt von `templates/` nach `user/themes/learn2/templates/`
   - Kopiere den Inhalt von `blueprints/` nach `user/themes/learn2/blueprints/`
   - Kopiere den Inhalt von `css/` nach `user/themes/learn2/css/`

3. **CSS einbinden:**

   Füge in `user/themes/learn2/templates/partials/base.html.twig` im `stylesheets` Block hinzu:

   ```twig
   {% do assets.addCss('theme://css/blog.css',100) %}
   ```

4. **Cache leeren:**

   ```bash
   bin/grav clear-cache
   ```

### Als Theme-Fork

Alternativ kannst du dieses Repository als vollständigen Fork des Learn2 Themes verwenden:

```bash
cd user/themes
git clone https://github.com/DEIN-USERNAME/grav-theme-learn2-blog.git learn2
cd learn2
```

## Verwendung

### Blog-Hauptseite erstellen

1. **Im Admin-Panel:** Erstelle eine neue Seite und wähle Template "Blog"
2. **Als Datei:** Erstelle `user/pages/blog/blog.md`

**Beispiel-Frontmatter:**

```yaml
---
title: Blog
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

Willkommen in unserem Blog!
```

### Blog-Posts erstellen

1. **Im Admin-Panel:** Erstelle Unterseiten im Blog-Ordner mit Template "Blog Item"
2. **Als Dateien:** Erstelle Unterordner in `user/pages/blog/`

**Beispiel-Struktur:**

```
user/pages/blog/
├── blog.md (Blog-Übersicht)
├── 01.erster-post/
│   ├── blog-item.md
│   └── header.jpg
├── 02.zweiter-post/
│   ├── blog-item.md
│   └── featured.png
```

**Beispiel-Frontmatter für einen Post:**

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
published: true
---

## Einleitung

Dies ist der Inhalt meines ersten Blog-Posts...

===

Dies ist die Zusammenfassung für die Blog-Übersicht.
```

## Konfiguration

### Verfügbare Header-Optionen

#### Für die Blog-Übersicht (`blog`)

| Option | Typ | Beschreibung |
|--------|-----|--------------|
| `title` | String | Titel der Blog-Seite (Pflicht) |
| `subtitle` | String | Optionaler Untertitel |
| `template` | String | Muss `blog` sein |
| `content.items` | String | `@self.children` für Unterseiten |
| `content.order.by` | String | Sortierung (z.B. `date`) |
| `content.order.dir` | String | `asc` oder `desc` |
| `content.limit` | Integer | Posts pro Seite |
| `content.pagination` | Boolean | Pagination aktivieren |

#### Für Blog-Posts (`blog-item`)

| Option | Typ | Beschreibung |
|--------|-----|--------------|
| `title` | String | Post-Titel (Pflicht) |
| `template` | String | Muss `blog-item` sein |
| `author` | String | Autor-Name |
| `date` | Date | Veröffentlichungsdatum |
| `featured_image` | String | Dateiname des Featured Images |
| `published` | Boolean | Veröffentlichungsstatus |
| `visible` | Boolean | Sichtbarkeit im Menü (Standard: `false`) |
| `taxonomy.category` | Array | Kategorien |
| `taxonomy.tag` | Array | Tags |

**Hinweis:** Blog-Posts sind standardmäßig **nicht im Menü sichtbar** (`visible: false`), um die Navigation übersichtlich zu halten. Sie sind über die Blog-Übersichtsseite zugänglich. Um einen Post im Menü anzuzeigen, setze `visible: true`.

### Featured Images

Featured Images werden aus dem Seiten-Ordner geladen:

1. Lade ein Bild in den Post-Ordner hoch (z.B. `header.jpg`)
2. Referenziere es im Header:

   ```yaml
   featured_image: header.jpg
   ```

Das Plugin skaliert und beschneidet Bilder automatisch für die Übersicht.

### Zusammenfassungen

Verwende den `===` Separator, um eine Zusammenfassung zu definieren:

```markdown
Das ist die Zusammenfassung.

===

Hier beginnt der vollständige Artikel...
```

Ohne Separator werden die ersten 500 Zeichen verwendet.

## Anpassung

### Styling anpassen

Bearbeite `css/blog.css` um Farben, Schriftarten und Layout anzupassen:

```css
/* Beispiel: Primärfarbe ändern */
.list-blog-content footer .button {
    background-color: #ff6600; /* Deine Farbe */
}

.list-blog-content h2 a:hover {
    color: #ff6600;
}
```

### Templates anpassen

Die Templates befinden sich in `templates/`:

- `blog.html.twig` - Blog-Übersicht
- `blog-item.html.twig` - Einzelner Post
- `partials/blog-item.html.twig` - Post-Vorschau

## Empfohlene Plugins

- **[Pagination](https://github.com/getgrav/grav-plugin-pagination)** - Für große Blogs
- **[Comments](https://github.com/getgrav/grav-plugin-comments)** - Kommentar-Funktion
- **[Breadcrumbs](https://github.com/getgrav/grav-plugin-breadcrumbs)** - Navigation
- **[Feed](https://github.com/getgrav/grav-plugin-feed)** - RSS/Atom Feeds
- **[Archives](https://github.com/getgrav/grav-plugin-archives)** - Archiv-Navigation
- **[Taxonomy List](https://github.com/getgrav/grav-plugin-taxonomylist)** - Tag-Wolke

## Entwicklung

### Projektstruktur

```
grav-theme-learn2-blog/
├── blueprints/
│   ├── blog.yaml           # Blueprint für Blog-Übersicht
│   └── blog-item.yaml      # Blueprint für Blog-Posts
├── css/
│   └── blog.css            # Blog-Styling
├── templates/
│   ├── blog.html.twig      # Blog-Übersicht Template
│   ├── blog-item.html.twig # Blog-Post Template
│   └── partials/
│       └── blog-item.html.twig  # Blog-Item Partial
├── CHANGELOG.md
├── LICENSE
└── README.md
```

### Contributing

Pull Requests sind willkommen! Für größere Änderungen öffne bitte zuerst ein Issue.

1. Fork das Repository
2. Erstelle einen Feature-Branch (`git checkout -b feature/AmazingFeature`)
3. Committe deine Änderungen (`git commit -m 'Add some AmazingFeature'`)
4. Push zum Branch (`git push origin feature/AmazingFeature`)
5. Öffne einen Pull Request

## Roadmap

- [ ] Unterstützung für Featured Posts
- [ ] Autor-Profile mit Avataren
- [ ] Related Posts Funktion
- [ ] Social Media Share Buttons
- [ ] Lesezeit-Anzeige
- [ ] Blog-Widget für Sidebar
- [ ] Multi-Language Support

## Troubleshooting

### Templates werden nicht erkannt

1. Cache leeren: `bin/grav clear-cache`
2. Überprüfe, ob die Dateien im richtigen Verzeichnis sind
3. Stelle sicher, dass das Learn2 Theme aktiviert ist

### Styling wird nicht angewendet

1. Überprüfe, ob `blog.css` in `base.html.twig` eingebunden ist
2. Cache leeren
3. Browser-Cache leeren (Strg+F5)

### Featured Images werden nicht angezeigt

1. Stelle sicher, dass das Bild im Post-Ordner liegt
2. Überprüfe den Dateinamen im Header
3. Achte auf korrekte Groß-/Kleinschreibung

## Credits

- Basierend auf dem [Learn2 Theme](https://github.com/getgrav/grav-theme-learn2) von [Team Grav](https://getgrav.org)
- [Font Awesome](https://fontawesome.com/) für Icons
- Alle Contributors dieses Projekts

## License

MIT License - siehe [LICENSE](LICENSE) Datei für Details.

Das Original Learn2 Theme ist ebenfalls unter MIT lizenziert.

## Support

- **Issues:** [GitHub Issues](https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/issues)
- **Grav Forum:** [https://getgrav.org/forum](https://getgrav.org/forum)
- **Grav Chat:** [https://chat.getgrav.org](https://chat.getgrav.org)

## Links

- [Grav CMS](https://getgrav.org)
- [Learn2 Original Theme](https://github.com/getgrav/grav-theme-learn2)
- [Grav Documentation](https://learn.getgrav.org)
- [Twig Documentation](https://twig.symfony.com/doc/)

---

**Hinweis:** Dies ist eine Theme-Erweiterung und kein eigenständiges Theme. Das Learn2 Basis-Theme muss installiert sein.
