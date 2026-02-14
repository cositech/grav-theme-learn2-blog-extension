# Detaillierte Installationsanleitung

Diese Anleitung führt dich Schritt für Schritt durch die Installation der Learn2 Blog Extension.

## Voraussetzungen

Bevor du beginnst, stelle sicher, dass folgendes installiert ist:

- **Grav CMS** Version 1.6 oder höher
- **Learn2 Theme** installiert und aktiviert
- **PHP** Version 7.3.6 oder höher (empfohlen: PHP 8.1+)
- **Webserver** (Apache, Nginx, oder PHP Built-in Server für Entwicklung)

### Grav installieren (falls noch nicht vorhanden)

```bash
# Mit Grav CLI (empfohlen)
cd /var/www/html
wget https://getgrav.org/download/core/grav-admin/latest
unzip grav-admin-latest.zip
cd grav-admin

# Oder mit Composer
composer create-project getgrav/grav grav-admin
cd grav-admin
bin/gpm install admin
```

### Learn2 Theme installieren

```bash
# Mit GPM
bin/gpm install learn2

# Oder manuell
cd user/themes
git clone https://github.com/getgrav/grav-theme-learn2.git learn2
```

Theme in `user/config/system.yaml` aktivieren:

```yaml
pages:
  theme: learn2
```

## Installation der Blog Extension

### Methode 1: Manuelle Installation (empfohlen für Entwicklung)

1. **Repository klonen oder herunterladen:**

```bash
cd /pfad/zu/deinem/grav
git clone https://github.com/DEIN-USERNAME/grav-theme-learn2-blog.git temp-blog
```

1. **Dateien in Learn2 Theme kopieren:**

```bash
# Templates kopieren
cp -r temp-blog/templates/* user/themes/learn2/templates/

# Blueprints kopieren
cp -r temp-blog/blueprints/* user/themes/learn2/blueprints/

# CSS kopieren
cp temp-blog/css/blog.css user/themes/learn2/css/

# Aufräumen
rm -rf temp-blog
```

1. **CSS in base.html.twig einbinden:**

Öffne `user/themes/learn2/templates/partials/base.html.twig` und füge im `{% block stylesheets %}` Block hinzu:

```twig
{% block stylesheets %}
    {% do assets.addCss('theme://css-compiled/nucleus.css',102) %}
    {% do assets.addCss('theme://css-compiled/theme.css',101) %}
    {% do assets.addCss('theme://css/blog.css',100) %}  {# Diese Zeile hinzufügen #}
    {% do assets.addCss('theme://css/custom.css',100) %}
    {% do assets.addCss('theme://css/font-awesome.min.css',100) %}
    {# ... rest ... #}
{% endblock %}
```

1. **Cache leeren:**

```bash
bin/grav clear-cache
```

### Methode 2: Als vollständiger Theme-Fork

Diese Methode ist ideal, wenn du das Theme als Ganzes verwenden möchtest:

```bash
cd user/themes

# Backup erstellen (falls Learn2 bereits installiert ist)
mv learn2 learn2-backup

# Repository als learn2 klonen
git clone https://github.com/DEIN-USERNAME/grav-theme-learn2-blog.git learn2
cd learn2
```

Das CSS ist bereits eingebunden, Cache leeren:

```bash
cd ../..
bin/grav clear-cache
```

### Methode 3: Als Git Submodule (für fortgeschrittene Nutzer)

```bash
cd user/themes/learn2
git submodule add https://github.com/DEIN-USERNAME/grav-theme-learn2-blog.git blog-extension
```

Dann symbolische Links erstellen oder Dateien manuell kopieren.

## Konfiguration

### Empfohlene Plugins installieren

1. **Pagination** (für große Blogs mit vielen Posts):

```bash
bin/gpm install pagination
```

Konfiguriere in `user/config/plugins/pagination.yaml`:

```yaml
enabled: true
built_in_css: true
delta: 0
```

1. **Breadcrumbs** (für Navigation):

```bash
bin/gpm install breadcrumbs
```

1. **Comments** (für Kommentarfunktion):

```bash
bin/gpm install comments
```

1. **Feed** (für RSS/Atom Feeds):

```bash
bin/gpm install feed
```

1. **Archives** (für Archiv-Ansicht):

```bash
bin/gpm install archives
```

1. **Taxonomy List** (für Tag-Wolke):

```bash
bin/gpm install taxonomylist
```

### System-Konfiguration

Optimale Einstellungen in `user/config/system.yaml`:

```yaml
pages:
  theme: learn2
  dateformat:
    default: 'd.m.Y H:i'
    short: 'd.m.Y'
    long: 'l, d. F Y'
  order:
    by: default
    dir: asc
  list:
    count: 20
  publish_dates: true
  
cache:
  enabled: true
  check:
    method: file
  driver: auto
  prefix: g
  purge_at: '0 4 * * *'
  
twig:
  cache: true
  debug: false
  auto_reload: true
  autoescape: false
```

## Erste Schritte

### 1. Blog-Hauptseite erstellen

#### Via Admin-Panel

1. Gehe zu **Admin Panel** → **Pages**
2. Klicke auf **Add Page**
3. Wähle **Blog** als Template
4. Titel: `Blog`
5. Folder Name: `blog`
6. Klicke auf **Continue**

Füge folgenden Inhalt ein:

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

Willkommen in unserem Blog! Hier findest du regelmäßig neue Artikel und Neuigkeiten.
```

#### Via Datei

Erstelle `user/pages/02.blog/blog.md`:

```markdown
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

### 2. Ersten Blog-Post erstellen

#### Via Admin-Panel

1. Gehe zur Blog-Seite
2. Klicke auf **Add Page**
3. Wähle **Blog Item** als Template
4. Titel: `Mein erster Blog-Post`
5. Folder Name: `erster-post`

Konfiguriere Metadaten:

- Author: Dein Name
- Published Date: Wähle Datum
- Tags: `Test, Grav, CMS`
- Categories: `Allgemein`

#### Via Datei

Erstelle `user/pages/02.blog/01.erster-post/blog-item.md`:

```markdown
---
title: Mein erster Blog-Post
template: blog-item
author: Max Mustermann
date: 14.02.2026 10:00
featured_image: header.jpg
taxonomy:
    category:
        - Allgemein
        - Tutorial
    tag:
        - Grav
        - CMS
        - Blog
published: true
---

## Willkommen!

Dies ist mein erster Blog-Post mit dem Learn2 Blog Template.

### Features

- **Markdown Support**: Schreibe in Markdown
- **Featured Images**: Zeige Bilder an
- **Tags & Kategorien**: Organisiere deine Posts

===

Dies ist die Zusammenfassung, die auf der Blog-Übersichtsseite angezeigt wird.
```

### 3. Featured Image hinzufügen

Kopiere ein Bild in den Post-Ordner:

```bash
cp /pfad/zu/deinem/bild.jpg user/pages/02.blog/01.erster-post/header.jpg
```

## Anpassung

### Blog-URL ändern

Standardmäßig ist der Blog unter `/blog` erreichbar. Um dies zu ändern:

1. Benenne den Ordner um: `02.blog` → `02.news`
2. Die URL ist jetzt `/news`

### Anzahl Posts pro Seite

In der Blog-Hauptseite (`blog.md`):

```yaml
content:
    limit: 20  # Ändere auf gewünschte Anzahl
```

### Sortierung ändern

```yaml
content:
    order:
        by: date     # oder 'title', 'folder', 'header.author'
        dir: desc    # oder 'asc'
```

### Styling anpassen

Bearbeite `user/themes/learn2/css/blog.css`:

```css
/* Primärfarbe ändern */
.list-blog-content footer .button {
    background-color: #ff6600; /* Deine Markenfarbe */
}

/* Schriftgröße anpassen */
.blog-list-item h2 {
    font-size: 2rem; /* Standard: varies */
}
```

## Fehlerbehebung

### Templates werden nicht erkannt

**Problem:** Nach der Installation werden die Blog-Templates nicht angezeigt.

**Lösung:**

```bash
# Cache vollständig leeren
bin/grav clear-cache
rm -rf cache/*

# In Admin-Panel
Tools → Clear Cache → All Cache
```

### CSS wird nicht geladen

**Problem:** Das Blog-Styling wird nicht angewendet.

**Lösung:**

1. Überprüfe, ob `blog.css` existiert
2. Prüfe `base.html.twig` auf CSS-Einbindung
3. Browser-Cache leeren (Strg+F5)
4. Asset-Pipeline-Cache leeren

### Featured Images werden nicht angezeigt

**Problem:** Featured Images erscheinen nicht.

**Lösung:**

1. Überprüfe Dateinamen (Groß-/Kleinschreibung!)
2. Stelle sicher, dass das Bild im richtigen Ordner liegt
3. Prüfe Dateiberechtigungen (755 für Ordner, 644 für Dateien)

```bash
chmod 755 user/pages/02.blog/01.erster-post/
chmod 644 user/pages/02.blog/01.erster-post/header.jpg
```

### 404-Fehler bei Blog-Posts

**Problem:** Blog-Posts führen zu 404-Fehlern.

**Lösung:**

1. Überprüfe, ob Posts als Unterseiten der Blog-Hauptseite liegen
2. Prüfe `published: true` in Frontmatter
3. Cache leeren

## Produktions-Optimierung

Für Live-Seiten:

### 1. Cache aktivieren

`user/config/system.yaml`:

```yaml
cache:
  enabled: true
  check:
    method: file
  driver: auto
  lifetime: 604800  # 1 Woche
  gzip: true
```

### 2. Twig-Debug deaktivieren

```yaml
twig:
  cache: true
  debug: false
  auto_reload: false
```

### 3. Asset-Pipeline aktivieren

```yaml
assets:
  css_pipeline: true
  css_minify: true
  css_rewrite: true
  js_pipeline: true
  js_minify: true
```

### 4. Performance-Plugins

```bash
bin/gpm install sitemap
bin/gpm install seo
```

## Backup

Vor wichtigen Änderungen:

```bash
# Vollständiges Backup
tar -czf grav-backup-$(date +%Y%m%d).tar.gz user/

# Nur Seiten und Konfiguration
tar -czf grav-pages-backup-$(date +%Y%m%d).tar.gz user/pages/ user/config/
```

## Updates

Blog-Extension aktualisieren:

### Wenn als Fork installiert

```bash
cd user/themes/learn2
git pull origin main
bin/grav clear-cache
```

### Wenn manuell installiert

1. Backup erstellen
2. Neue Version herunterladen
3. Dateien überschreiben
4. Cache leeren

## Support

- **Dokumentation:** [README.md](README.md)
- **Issues:** [GitHub Issues](https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/issues)
- **Grav Forum:** [https://getgrav.org/forum](https://getgrav.org/forum)
- **Grav Discord:** [https://chat.getgrav.org](https://chat.getgrav.org)

## Nächste Schritte

Nach der Installation:

1. [Konfiguration verstehen](BLOG_README.md)
2. [Contributing Guidelines lesen](CONTRIBUTING.md)
3. Mehrere Posts erstellen und testen
4. Styling an deine Marke anpassen
5. Plugins nach Bedarf hinzufügen

Viel Erfolg mit deinem Blog! 🚀
