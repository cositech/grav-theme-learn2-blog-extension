# Häufig gestellte Fragen (FAQ)

Antworten auf häufig gestellte Fragen zur Learn2 Blog Extension.

## 📦 Installation

### Kann ich dies mit einem bestehenden Learn2 Theme verwenden?

**Ja!** Die Blog Extension ist speziell dafür entwickelt, das bestehende Learn2 Theme zu erweitern. Du musst nur die Templates, Blueprints und CSS-Dateien kopieren.

### Funktioniert dies mit anderen Grav-Themes?

**Nicht direkt.** Die Extension ist speziell für Learn2 entwickelt und verwendet dessen Basis-Templates. Für andere Themes müsstest du die Templates anpassen.

### Brauche ich Programmierkenntnisse?

**Nein!** Wenn du die Standardfunktionalität nutzt, brauchst du keine Programmierkenntnisse. Für Anpassungen sind HTML/CSS/Twig-Kenntnisse hilfreich.

---

## 🎨 Anpassung & Styling

### Wie ändere ich die Farben?

Bearbeite `user/themes/learn2/css/blog.css` und ändere die Farbwerte:

```css
/* Primärfarbe */
.list-blog-content footer .button {
    background-color: #DEINE-FARBE;
}
```

Siehe auch: [QUICKSTART.md](QUICKSTART.md#schnelle-anpassungen)

### Kann ich das Layout ändern?

**Ja!** Die Templates befinden sich in `user/themes/learn2/templates/`. Du kannst:

- `blog.html.twig` - Layout der Übersicht ändern
- `blog-item.html.twig` - Layout einzelner Posts ändern
- `css/blog.css` - Styling komplett anpassen

### Wie füge ich eigene CSS-Klassen hinzu?

In den Frontmatter deiner Seite:

```yaml
body_classes: my-custom-class another-class
```

---

## 📝 Inhalte erstellen

### Wie erstelle ich einen neuen Blog-Post?

**Via Admin-Panel:**

1. Gehe zu Pages → Blog
2. Klicke "Add Page"
3. Wähle Template "Blog Item"
4. Fülle Felder aus und speichere

**Via Datei:**

```bash
mkdir user/pages/02.blog/03.mein-post
nano user/pages/02.blog/03.mein-post/blog-item.md
```

Siehe: [QUICKSTART.md](QUICKSTART.md)

### Unterstützt es Markdown?

**Ja, vollständig!** Grav nutzt Markdown. Du kannst alle Standard-Markdown-Features verwenden:

- Überschriften
- Listen
- Links
- Bilder
- Code-Blöcke
- Tabellen
- und mehr

Siehe: [Grav Markdown Syntax](https://learn.getgrav.org/17/content/markdown)

### Wie füge ich Bilder hinzu?

**Featured Image:**

1. Lade Bild in Post-Ordner hoch
2. Referenziere in Frontmatter: `featured_image: bild.jpg`

**Im Text:**

```markdown
![Alt-Text](bild.jpg)

Oder mit Grav-Syntax:
![Alt-Text](bild.jpg?lightbox=600,400&cropResize=400,200)
```

### Kann ich Videos einbetten?

**Ja!** Nutze HTML oder Markdown:

```markdown
[plugin:youtube](https://www.youtube.com/watch?v=VIDEO_ID)

Oder direktes HTML:
<iframe width="560" height="315" 
  src="https://www.youtube.com/embed/VIDEO_ID" 
  frameborder="0" allowfullscreen></iframe>
```

---

## 🔧 Features & Funktionalität

### Wie aktiviere ich Kommentare?

1. Installiere Comments-Plugin:

   ```bash
   bin/gpm install comments
   ```

2. Konfiguriere in `user/config/plugins/comments.yaml`

3. Kommentare erscheinen automatisch unter Posts

### Funktioniert Pagination?

**Ja!** Installiere das Pagination-Plugin:

```bash
bin/gpm install pagination
```

Konfiguriere in der Blog-Hauptseite:

```yaml
content:
    pagination: true
    limit: 10
```

### Kann ich Posts als Draft speichern?

**Ja!** Setze in Frontmatter:

```yaml
published: false
```

Oder nutze den Published-Toggle im Admin-Panel.

### Warum erscheinen meine Blog-Posts nicht im Menü?

**Das ist gewollt!** Blog-Posts sind standardmäßig **nicht im Menü sichtbar** (`visible: false`), um die Navigation sauber zu halten. Sie sind aber über die Blog-Übersichtsseite erreichbar.

**Falls du einen Post im Menü anzeigen möchtest:**

Via Admin-Panel:
1. Öffne den Post
2. Gehe zu "Options"-Tab
3. Aktiviere "Visible in Menu"

Via Datei in Frontmatter:

```yaml
visible: true
```

**Hinweis:** Dies ist seit Version 1.1.0 das Standardverhalten.

**Für bestehende Installationen:**
Wenn du bereits Blog-Posts hast, die du manuell als "invisible" gesetzt hast, kannst du diese Einstellung entfernen. Neue Posts werden automatisch verborgen.

### Wie erstelle ich eine Serie von Posts?

Nutze Kategorien:

```yaml
taxonomy:
    category:
        - Meine Serie
        - Teil 1
```

Dann kannst du Posts nach Kategorie filtern.

### Unterstützt es Tags und Kategorien?

**Ja!** Beide werden voll unterstützt:

```yaml
taxonomy:
    category:
        - Tutorials
        - Technologie
    tag:
        - Grav
        - CMS
        - PHP
```

---

## 🔍 SEO & Performance

### Ist es SEO-optimiert?

**Ja!** Folgende SEO-Features sind enthalten:

- Semantisches HTML5
- Meta-Descriptions (via Zusammenfassung)
- Proper heading hierarchy
- Clean URLs
- Fast loading times

Zusätzlich empfohlen:

```bash
bin/gpm install seo
bin/gpm install sitemap
```

### Wie verbessere ich die Performance?

1. **Cache aktivieren:**

   ```yaml
   # user/config/system.yaml
   cache:
     enabled: true
   ```

2. **Asset-Pipeline nutzen:**

   ```yaml
   assets:
     css_pipeline: true
     js_pipeline: true
   ```

3. **Bilder optimieren:**
   - Nutze Gravs Image-Processing
   - WebP-Format verwenden
   - Lazy Loading aktivieren

4. **CDN verwenden** für statische Assets

### Unterstützt es RSS/Atom Feeds?

**Ja, mit Plugin!** Installiere Feed-Plugin:

```bash
bin/gpm install feed
```

Feed ist dann verfügbar unter:

- `/blog.atom`
- `/blog.rss`

---

## 🌐 Multi-Language

### Kann ich mehrsprachige Blogs erstellen?

**Derzeit nicht vollständig.** Multi-Language-Support ist für Version 1.3.0 geplant.

**Workaround:** Erstelle separate Blog-Ordner pro Sprache:

```
user/pages/
├── 02.blog-de/    # Deutsch
└── 03.blog-en/    # Englisch
```

---

## 🔒 Sicherheit & Privatsphäre

### Ist es sicher?

**Ja!** Die Extension folgt Grav-Best-Practices:

- Kein gefährlicher Code
- Twig auto-escaping
- Keine externen Dependencies
- MIT-lizenziert

Siehe: [SECURITY.md](SECURITY.md)

### Ist es GDPR-konform?

**Die Extension selbst ja.** Sie sammelt keine Daten. Beachte aber:

- Comments-Plugin: Konfiguriere Privacy-Settings
- Analytics: Nutze privacy-freundliche Lösungen
- Featured Images: Keine EXIF-Daten ohne Zustimmung

---

## 🐛 Troubleshooting

### Templates werden nicht erkannt

**Lösung:**

```bash
# Cache leeren
bin/grav clear-cache

# Verzeichnisse prüfen
ls -la user/themes/learn2/templates/blog*.twig
ls -la user/themes/learn2/blueprints/blog*.yaml
```

### CSS wird nicht geladen

**Lösung:**

1. Prüfe ob `blog.css` existiert
2. Prüfe Einbindung in `base.html.twig`
3. Browser-Cache leeren (Strg+F5)
4. Grav-Cache leeren: `bin/grav clear-cache`

### Featured Images werden nicht angezeigt

**Häufige Ursachen:**

- Dateiname falsch geschrieben (Groß-/Kleinschreibung!)
- Bild nicht im richtigen Ordner
- Dateiberechtigungen falsch

**Lösung:**

```bash
# Berechtigungen setzen
chmod 644 user/pages/02.blog/01.post/*.jpg

# Dateinamen prüfen
ls -la user/pages/02.blog/01.post/
```

### 404-Fehler bei Posts

**Lösung:**

1. Prüfe ob Posts als Unterseiten von Blog liegen
2. Prüfe `published: true` in Frontmatter
3. Cache leeren
4. Überprüfe URL-Struktur

### Blog-Seite ist leer

**Mögliche Ursachen:**

- Keine Posts erstellt
- Posts nicht veröffentlicht (`published: false`)
- Collection-Config falsch

**Lösung:**

```yaml
# In blog.md
content:
    items: '@self.children'  # Korrigiere wenn nötig
```

---

## 🔄 Migration & Update

### Kann ich von WordPress migrieren?

**Indirekt.** Es gibt keine automatische Migration, aber:

1. Exportiere WordPress-Posts als Markdown
2. Konvertiere zu Grav-Format
3. Kopiere in Post-Ordner

Tools:

- [wordpress-to-grav](https://github.com/perlkonig/wp2grav)
- Manueller Export/Import via Tools

### Wie update ich die Extension?

**Als Fork:**

```bash
cd user/themes/learn2
git pull origin main
bin/grav clear-cache
```

**Manuell:**

1. Backup erstellen
2. Neue Version herunterladen
3. Dateien überschreiben
4. CHANGELOG.md für Breaking Changes prüfen
5. Cache leeren

### Gehen meine Anpassungen beim Update verloren?

**Kommt darauf an:**

- ✅ Inhalte (Pages): **Nein**, bleiben erhalten
- ❌ Template-Änderungen: **Ja**, werden überschrieben
- ❌ CSS-Änderungen: **Ja**, werden überschrieben

**Best Practice:**

- Custom CSS in `custom.css`
- Template-Overrides außerhalb Extension
- Änderungen dokumentieren

---

## 💡 Best Practices

### Wie organisiere ich viele Posts?

**Option 1: Chronologisch**

```
02.blog/
├── 01.januar-2026/
├── 02.februar-2026/
└── 03.maerz-2026/
```

**Option 2: Nach Kategorie**

```
02.blog/
├── tutorials/
├── news/
└── reviews/
```

**Option 3: Fortlaufend**

```
02.blog/
├── 001.first-post/
├── 002.second-post/
└── 003.third-post/
```

### Sollte ich den Admin-Panel oder Dateien verwenden?

**Admin-Panel:**

- ✅ Einfacher für Anfänger
- ✅ GUI für alle Optionen
- ❌ Langsamer bei vielen Posts

**Dateien:**

- ✅ Schneller für erfahrene Nutzer
- ✅ Version Control (Git)
- ✅ Bulk-Operations möglich
- ❌ Markup-Kenntnisse erforderlich

**Empfehlung:** Nutze was dir liegt! Kombinieren ist auch möglich.

### Wie strukturiere ich SEO-freundliche URLs?

**Gut:**

```
/blog/mein-erster-post
/blog/grav-cms-tutorial
/blog/learn2-theme-anpassung
```

**Weniger gut:**

```
/blog/01.post
/blog/artikel-nummer-5
/blog/p1
```

**Tipp:** Setze `slug` in Frontmatter:

```yaml
slug: grav-cms-tutorial
```

---

## 🆘 Weitere Hilfe

### Wo finde ich mehr Dokumentation?

- **README.md** - Übersicht
- **INSTALL.md** - Installation
- **QUICKSTART.md** - Schnellstart
- **BLOG_README.md** - Features im Detail
- **DOCUMENTATION.md** - Technische Doku

### Community-Support

- **GitHub Issues**: Bug-Reports & Features
- **Grav Forum**: [getgrav.org/forum](https://getgrav.org/forum)
- **Grav Discord**: [chat.getgrav.org](https://chat.getgrav.org)
- **Grav Docs**: [learn.getgrav.org](https://learn.getgrav.org)

### Professioneller Support

Für kommerzielle Projekte:

- Grav Premium Support
- Theme-Entwickler kontaktieren
- Grav-Dienstleister beauftragen

---

## ❓ Deine Frage nicht dabei?

**Öffne ein Issue oder Discussion auf GitHub:**

- [GitHub Issues](https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/issues) - Bugs & Features
- [GitHub Discussions](https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/discussions) - Fragen & Diskussionen

---

**Letzte Aktualisierung:** 14. Februar 2026

Diese FAQ wird kontinuierlich erweitert basierend auf Community-Fragen.
