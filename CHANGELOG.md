# Changelog

Alle wichtigen Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

Das Format basiert auf [Keep a Changelog](https://keepachangelog.com/de/1.0.0/),
und dieses Projekt folgt [Semantic Versioning](https://semver.org/lang/de/).

## [Unreleased]

### Geplant
- Featured Posts Unterstützung
- Autor-Profile mit Avataren
- Related Posts Funktion
- Social Media Share Buttons
- Lesezeit-Anzeige
- Blog-Widget für Sidebar

## [1.0.0] - 2026-02-14

### Hinzugefügt
- Initiales Release der Blog-Erweiterung für Learn2 Theme
- Blog-Übersichtsseite Template (`blog.html.twig`)
- Einzelner Blog-Post Template (`blog-item.html.twig`)
- Blog-Item Partial für Listenansicht
- Blueprint für Blog-Übersicht (`blog.yaml`)
- Blueprint für Blog-Posts (`blog-item.yaml`)
- Vollständiges responsives CSS-Styling (`blog.css`)
- Featured Images Support
- Autor-Informationen
- Veröffentlichungsdatum
- Tags und Kategorien mit automatischen Links
- Vor/Zurück-Navigation zwischen Posts
- Pagination Support
- Kommentar-Integration (wenn Plugin aktiviert)
- Zusammenfassungen mit "Weiterlesen"-Button
- Responsive Design für Mobile, Tablet und Desktop
- Umfassende Dokumentation (README.md, BLOG_README.md)
- MIT Lizenz
- Contributing Guidelines
- Issue und Pull Request Templates

### Features im Detail

#### Templates
- **Blog-Übersicht**: Automatische Auflistung aller Posts mit Sortierung nach Datum
- **Blog-Post**: Vollständige Post-Darstellung mit Metadaten und Navigation
- **Partial**: Wiederverwendbares Template für Post-Vorschauen

#### Styling
- Mobile-First Design
- Flexbox-basiertes Layout
- Featured-Image-Unterstützung in zwei Größen
- Hover-Effekte und Transitionen
- Syntax-Highlighting-kompatibel
- Blockquote und Code-Block Styling

#### Administrator
- Admin-Panel Integration über Blueprints
- Benutzerfreundliche Felder für alle Metadaten
- Taxonomy-Verwaltung
- Datum/Zeit-Picker
- Published-Status Toggle

#### Kompatibilität
- Grav 1.6+
- Learn2 Theme nahtlose Integration
- Plugin-Ready (Pagination, Comments, Breadcrumbs)
- SEO-optimiert

---

## Versionshinweise

### Versionsnummern

Dieses Projekt verwendet Semantic Versioning:
- **MAJOR** (X.0.0): Inkompatible API-Änderungen
- **MINOR** (0.X.0): Neue Features (abwärtskompatibel)
- **PATCH** (0.0.X): Bugfixes (abwärtskompatibel)

### Upgrade-Hinweise

#### Von keiner Version (Neuinstallation)
Folge den Installationsanweisungen in der README.md.

---

[Unreleased]: https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/releases/tag/v1.0.0
