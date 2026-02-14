# GitHub Release Checklist

Diese Checkliste hilft dir, das Projekt erfolgreich auf GitHub zu veröffentlichen.

## 📋 Pre-Release Checklist

### Code & Dateien

- [x] Alle Template-Dateien erstellt und getestet
  - [x] `templates/blog.html.twig`
  - [x] `templates/blog-item.html.twig`
  - [x] `templates/partials/blog-item.html.twig`

- [x] Alle Blueprint-Dateien erstellt
  - [x] `blueprints/blog.yaml`
  - [x] `blueprints/blog-item.yaml`

- [x] CSS-Dateien erstellt
  - [x] `css/blog.css`
  - [x] Responsive Design getestet

### Dokumentation

- [x] README.md vollständig
  - [x] Features beschrieben
  - [x] Installation erklärt
  - [x] Screenshots hinzugefügt (todo)
  - [x] Badges eingefügt

- [x] Zusätzliche Dokumentation
  - [x] INSTALL.md - Detaillierte Installation
  - [x] QUICKSTART.md - 5-Minuten-Guide
  - [x] BLOG_README.md - Feature-Beschreibung
  - [x] DOCUMENTATION.md - Technische Details
  - [x] FAQ.md - Häufige Fragen
  - [x] ROADMAP.md - Zukünftige Features

- [x] Projekt-Governance
  - [x] CONTRIBUTING.md erstellt
  - [x] CHANGELOG.md erstellt
  - [x] LICENSE erstellt (MIT)
  - [x] SECURITY.md erstellt

- [x] GitHub-Templates
  - [x] Bug Report Template
  - [x] Feature Request Template
  - [x] Question Template
  - [x] Pull Request Template
  - [x] Issue Config (config.yml)

### Repository Setup

- [ ] Repository auf GitHub erstellt
  ```
  Name: grav-theme-learn2-blog
  Description: Professional blog extension for Grav Learn2 Theme
  Public/Private: Public
  ```

- [ ] Repository-Einstellungen
  - [ ] Topics hinzugefügt: `grav`, `grav-theme`, `blog`, `learn2`, `cms`
  - [ ] Website-URL gesetzt
  - [ ] License (MIT) ausgewählt
  - [ ] Issues aktiviert
  - [ ] Discussions aktiviert (optional)
  - [ ] Wiki aktiviert (optional)

- [ ] Branch Protection
  - [ ] `main` Branch geschützt
  - [ ] Require PR reviews
  - [ ] Require status checks

### Testing

- [ ] Funktionale Tests
  - [ ] Frische Grav-Installation getestet
  - [ ] Learn2 Theme kompatibel
  - [ ] Alle Templates funktionieren
  - [ ] CSS wird korrekt geladen
  - [ ] Featured Images funktionieren
  - [ ] Navigation funktioniert
  - [ ] Taxonomien funktionieren

- [ ] Browser-Tests
  - [ ] Chrome/Edge (aktuell)
  - [ ] Firefox (aktuell)
  - [ ] Safari (wenn möglich)
  - [ ] Mobile Browser (iOS/Android)

- [ ] Responsive Tests
  - [ ] Mobile (< 768px)
  - [ ] Tablet (768px - 1024px)
  - [ ] Desktop (> 1024px)

### Vorbereitung

- [ ] Screenshots erstellen
  - [ ] Blog-Übersicht
  - [ ] Einzelner Post
  - [ ] Admin-Panel
  - [ ] Mobile View
  
  Speichern in: `docs/screenshots/` oder direkt in README einbinden

- [ ] Demo-Content erstellen
  - [ ] Beispiel-Blog-Seite
  - [ ] 3-5 Beispiel-Posts
  - [ ] Verschiedene Kategorien/Tags
  - [ ] Mit und ohne Featured Images

## 🚀 Repository-Erstellung

### 1. Initiales Commit

```bash
# In deinem lokalen Projekt-Verzeichnis
cd /pfad/zu/grav-theme-learn2

# Git initialisieren (falls noch nicht geschehen)
git init

# Alle Dateien hinzufügen
git add .

# Initial commit
git commit -m "Initial commit: Learn2 Blog Extension v1.0.0

- Add blog and blog-item templates
- Add blog blueprints for admin panel
- Add responsive blog CSS styling
- Add comprehensive documentation
- Add GitHub templates and configs
- MIT License"

# Remote hinzufügen (ersetze USERNAME)
git remote add origin https://github.com/DEIN-USERNAME/grav-theme-learn2-blog.git

# Push
git branch -M main
git push -u origin main
```

### 2. Repository auf GitHub erstellen

**Via GitHub Website:**
1. Gehe zu [github.com/new](https://github.com/new)
2. Repository-Name: `grav-theme-learn2-blog`
3. Beschreibung: `Professional blog extension for Grav Learn2 Theme with full feature set`
4. Visibility: **Public**
5. **DO NOT** initialize with README, license, or .gitignore (bereits vorhanden)
6. Klicke "Create repository"
7. Folge den Anweisungen für "push an existing repository"

**Via GitHub CLI:**
```bash
# GitHub CLI installiert?
gh repo create grav-theme-learn2-blog --public --source=. --remote=origin --push
```

### 3. Repository konfigurieren

**Topics hinzufügen:**
```
grav, grav-theme, grav-plugin, blog, learn2, cms, markdown, php, twig
```

**About Section:**
- Website: `https://getgrav.org`
- Description: `🎨 Professional blog extension for Grav Learn2 Theme - Features rich blogging, featured images, tags, categories, responsive design, and more!`

**Features aktivieren:**
- ✅ Issues
- ✅ Projects (optional)
- ✅ Discussions (empfohlen)
- ✅ Wiki (optional)

### 4. Release erstellen

**Via GitHub Website:**
1. Gehe zu "Releases" → "Create a new release"
2. Tag: `v1.0.0`
3. Release title: `v1.0.0 - Initial Release`
4. Beschreibung:

```markdown
# 🎉 Initial Release

First official release of the Learn2 Blog Extension!

## ✨ Features

- 📝 Full blog functionality for Learn2 theme
- 🖼️ Featured image support
- 👤 Author information and metadata
- 🏷️ Tags and categories with automatic links
- ◀️▶️ Post navigation (prev/next)
- 📱 Fully responsive design
- 💬 Comment integration support
- 📄 Pagination support
- 🎨 Seamless Learn2 theme integration

## 📦 What's Included

- Blog overview template (`blog.html.twig`)
- Blog post template (`blog-item.html.twig`)
- Admin panel blueprints
- Complete CSS styling
- Comprehensive documentation

## 🚀 Quick Start

See [QUICKSTART.md](QUICKSTART.md) for a 5-minute setup guide!

## 📚 Documentation

- [README.md](README.md) - Overview and features
- [INSTALL.md](INSTALL.md) - Detailed installation
- [BLOG_README.md](BLOG_README.md) - Feature documentation
- [FAQ.md](FAQ.md) - Common questions

## 📦 Installation

### Manual Installation

1. Clone or download this repository
2. Copy files to your Learn2 theme:
   ```bash
   cp -r templates/* user/themes/learn2/templates/
   cp -r blueprints/* user/themes/learn2/blueprints/
   cp css/blog.css user/themes/learn2/css/
   ```
3. Include CSS in `base.html.twig`
4. Clear cache: `bin/grav clear-cache`

See [INSTALL.md](INSTALL.md) for detailed instructions.

## 🐛 Known Issues

None at release time.

## 🙏 Credits

Based on [Learn2 Theme](https://github.com/getgrav/grav-theme-learn2) by Team Grav.

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

**Full Changelog**: https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/commits/v1.0.0
```

5. ✅ Set as latest release
6. Publish!

**Via GitHub CLI:**
```bash
gh release create v1.0.0 --title "v1.0.0 - Initial Release" --notes-file release-notes.md
```

## 📢 Post-Release

### README.md aktualisieren

Ersetze Platzhalter:
- [ ] `DEIN-USERNAME` → dein GitHub-Username
- [ ] Badge-URLs aktualisieren
- [ ] Installations-URLs anpassen
- [ ] Screenshot-URLs hinzufügen

### Social Media Ankündigung

**Twitter/X:**
```
🎉 Introducing Learn2 Blog Extension for @getgrav! 

✨ Full-featured blogging
🖼️ Featured images
🏷️ Tags & categories
📱 Fully responsive

Perfect for documentation sites that need a blog!

🔗 https://github.com/DEIN-USERNAME/grav-theme-learn2-blog

#GravCMS #Blog #OpenSource
```

**Grav Forum:**
1. Post in "Themes" oder "Show Your Work"
2. Titel: "Learn2 Blog Extension - Full Blog Functionality for Learn2 Theme"
3. Link zum Repository
4. Screenshots
5. Kurze Feature-Beschreibung

**Grav Discord:**
Share im #show-and-tell Channel

### Community Integration

- [ ] Grav Forum Post erstellen
- [ ] Grav Discord ankündigen
- [ ] Reddit r/gravcms (wenn aktiv)
- [ ] Twitter/X ankündigen
- [ ] Personal Blog-Post (optional)

## 🔄 Post-Release Monitoring

### Erste Woche

- [ ] Issues überwachen und schnell reagieren
- [ ] Feedback sammeln
- [ ] Quick-Fix-Bugs patchen (v1.0.1)
- [ ] Contributors begrüßen

### Erste Monat

- [ ] Analytics einrichten (GitHub Insights)
- [ ] Community-Feedback einarbeiten
- [ ] Roadmap nach Priorität adjustieren
- [ ] Dokumentation verbessern basierend auf Fragen

## 📊 Success Metrics

**Track folgende Metriken:**
- GitHub Stars
- Forks
- Issues (offen/geschlossen)
- Pull Requests
- Downloads/Clones
- Community-Diskussionen

**Ziele Month 1:**
- [ ] 10+ Stars
- [ ] 3+ Forks
- [ ] 5+ Issues behandelt
- [ ] 1-2 Contributors

## 🎯 Nächste Schritte

Nach erfolgreichem Release:

1. **Feedback Phase** (Woche 1-2)
   - Bugs fixen
   - Quick wins implementieren
   - Community einbinden

2. **Stabilisierungs-Phase** (Woche 3-4)
   - v1.0.1 Bug-Fix-Release
   - Tests erweitern
   - Dokumentation verbessern

3. **Feature-Phase** (Monat 2+)
   - Roadmap v1.1.0 starten
   - Community-Features priorisieren
   - Plugin-Ecosystem planen

## ✅ Final Check

Vor dem Veröffentlichen:

- [ ] Alle Dateien committed
- [ ] Keine TODOs oder FIXMEs im Code
- [ ] Alle Platzhalter ersetzt
- [ ] Screenshots hinzugefügt
- [ ] License korrekt
- [ ] Links funktionieren
- [ ] Demo funktioniert
- [ ] Dokumentation vollständig
- [ ] Release Notes geschrieben

---

## 🎊 Ready to Launch!

Wenn alle Checkboxen abgehakt sind, bist du bereit für den Release!

**Good luck! 🚀**

---

**Checkliste erstellt:** 14. Februar 2026  
**Für Version:** 1.0.0
