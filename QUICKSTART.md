# Quick Start Guide

Schnellstartanleitung für die Learn2 Blog Extension - von der Installation bis zum ersten Blog-Post in 5 Minuten!

## ⚡ Voraussetzungen

- Grav CMS installiert
- Learn2 Theme installiert und aktiviert
- 5 Minuten Zeit ⏱️

## 📦 Installation (2 Minuten)

### Option A: Schnelle manuelle Installation

```bash
# 1. In dein Grav-Verzeichnis wechseln
cd /pfad/zu/deinem/grav

# 2. Repository klonen
git clone https://github.com/DEIN-USERNAME/grav-theme-learn2-blog.git temp-blog

# 3. Dateien kopieren
cp -r temp-blog/templates/* user/themes/learn2/templates/
cp -r temp-blog/blueprints/* user/themes/learn2/blueprints/
cp temp-blog/css/blog.css user/themes/learn2/css/

# 4. Aufräumen
rm -rf temp-blog

# 5. CSS einbinden
echo "{% do assets.addCss('theme://css/blog.css',100) %}" >> user/themes/learn2/templates/partials/base.html.twig

# 6. Cache leeren
bin/grav clear-cache
```

Fertig! ✅

## 📝 Erster Blog-Post (3 Minuten)

### 1. Blog-Hauptseite erstellen

Erstelle `user/pages/02.blog/blog.md`:

```markdown
---
title: Blog
template: blog
content:
    items: '@self.children'
    order:
        by: date
        dir: desc
---

Willkommen in meinem Blog!
```

### 2. Ersten Post erstellen

Erstelle `user/pages/02.blog/01.hello-world/blog-item.md`:

```markdown
---
title: Hello World!
template: blog-item
author: Dein Name
date: 14.02.2026
taxonomy:
    tag:
        - Grav
        - Blog
---

## Mein erster Post

Das ist mein erster Blog-Post mit der Learn2 Blog Extension!

### Was ich gelernt habe

- Installation ist super einfach
- Markdown macht Spaß
- Grav ist toll

===

Dies ist die Zusammenfassung für die Übersichtsseite.
```

### 3. Optional: Featured Image hinzufügen

```bash
# Kopiere ein Bild in den Post-Ordner
cp /pfad/zu/bild.jpg user/pages/02.blog/01.hello-world/header.jpg
```

Und füge in `blog-item.md` hinzu:

```yaml
featured_image: header.jpg
```

### 4. Ansehen! 🎉

Öffne in deinem Browser:

```
http://localhost:8000/blog
```

## 🎨 Schnelle Anpassungen

### Farben ändern

Bearbeite `user/themes/learn2/css/blog.css`:

```css
/* Primärfarbe ändern (z.B. zu deiner Markenfarbe) */
.list-blog-content footer .button {
    background-color: #ff6600; /* Deine Farbe hier */
}

.list-blog-content h2 a:hover {
    color: #ff6600;
}

.post-meta a {
    color: #ff6600;
}
```

### Mehr Posts pro Seite

In `blog.md`:

```yaml
content:
    limit: 20  # Standard: 10
```

### Sortierung ändern

```yaml
content:
    order:
        by: title  # oder 'date', 'folder'
        dir: asc   # oder 'desc'
```

## 🚀 Nächste Schritte

### Empfohlene Plugins installieren

```bash
# Pagination für große Blogs
bin/gpm install pagination

# Kommentare
bin/gpm install comments

# RSS Feed
bin/gpm install feed
```

### Mehr Posts erstellen

Kopiere einfach den Post-Ordner:

```bash
cp -r user/pages/02.blog/01.hello-world user/pages/02.blog/02.mein-zweiter-post
```

Dann bearbeite `blog-item.md` im neuen Ordner.

### Admin-Panel nutzen

Falls du das Admin-Plugin hast:

1. Gehe zu `/admin`
2. Klicke auf "Pages" → "Blog"
3. Klicke auf "Add Page"
4. Wähle Template "Blog Item"
5. Fülle die Felder aus
6. Speichern!

## 💡 Tipps

### Markdown-Features nutzen

```markdown
## Überschriften

### Unterüberschrift

**Fett** und *kursiv*

- Listen
- sind
- einfach

1. Nummerierte
2. Listen
3. auch!

> Zitate sehen so aus

`Code inline` oder:

```

Code-Blöcke
so hier

```

[Links](https://getgrav.org) sind easy

![Bilder](bild.jpg) auch!
```

### Zusammenfassungen definieren

Nutze `===` um eine Zusammenfassung zu definieren:

```markdown
Das ist die Zusammenfassung, die auf der Übersichtsseite erscheint.

===

Hier beginnt der volle Artikel-Inhalt...
```

### Tags und Kategorien verwenden

```yaml
taxonomy:
    category:
        - Tutorials
        - Technologie
    tag:
        - Grav
        - CMS
        - Web
        - PHP
```

### Datum-Formate

```yaml
date: 14.02.2026           # Einfach
date: 14.02.2026 10:30     # Mit Zeit
date: 2026-02-14           # ISO-Format
```

## 🔧 Troubleshooting

### Templates werden nicht erkannt?

```bash
# Cache leeren
bin/grav clear-cache

# Oder komplett
rm -rf cache/*
```

### CSS wird nicht geladen?

1. Prüfe ob `blog.css` existiert:

   ```bash
   ls -la user/themes/learn2/css/blog.css
   ```

2. Prüfe Einbindung in `base.html.twig`:

   ```bash
   grep "blog.css" user/themes/learn2/templates/partials/base.html.twig
   ```

3. Browser-Cache leeren (Strg+F5)

### Featured Image wird nicht angezeigt?

```bash
# Prüfe ob Bild existiert
ls -la user/pages/02.blog/01.hello-world/*.jpg

# Prüfe Berechtigungen
chmod 644 user/pages/02.blog/01.hello-world/*.jpg
```

## 📚 Weiterführende Dokumentation

- **Detaillierte Features**: [BLOG_README.md](BLOG_README.md)
- **Installation**: [INSTALL.md](INSTALL.md)
- **Vollständige Doku**: [README.md](README.md)
- **Anpassungen**: [DOCUMENTATION.md](DOCUMENTATION.md)

## 🎉 Fertig

Du hast jetzt:

- ✅ Blog Extension installiert
- ✅ Blog-Hauptseite erstellt
- ✅ Ersten Post veröffentlicht
- ✅ Weißt, wie es weitergeht

Viel Erfolg mit deinem Blog! 🚀

## 🆘 Hilfe benötigt?

- **Dokumentation**: Siehe Links oben
- **Issues**: [GitHub Issues](https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/issues)
- **Grav Forum**: [getgrav.org/forum](https://getgrav.org/forum)
- **Discord**: [chat.getgrav.org](https://chat.getgrav.org)

---

**Zeit**: ⏱️ ~5 Minuten  
**Schwierigkeit**: 🟢 Einfach  
**Ergebnis**: 🎉 Funktionierender Blog!
