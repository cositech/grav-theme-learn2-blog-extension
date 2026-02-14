# Security Policy

## Unterstützte Versionen

Wir stellen Sicherheitsupdates für die folgenden Versionen bereit:

| Version | Unterstützt          |
| ------- | -------------------- |
| 1.0.x   | :white_check_mark:   |
| < 1.0   | :x:                  |

## Sicherheitslücken melden

Die Sicherheit dieses Projekts nehmen wir ernst. Wenn du eine Sicherheitslücke findest, bitten wir dich, verantwortungsvoll damit umzugehen.

### Bitte NICHT:

- ❌ Öffne **kein** öffentliches GitHub Issue für Sicherheitsprobleme
- ❌ Poste Sicherheitslücken nicht in sozialen Medien
- ❌ Veröffentliche Details nicht vor einer Lösung

### Stattdessen:

1. **Sende eine E-Mail** an: [DEINE-EMAIL@example.com]
   
   Oder nutze GitHubs Security Advisory Feature:
   - Gehe zu: https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/security/advisories
   - Klicke auf "Report a vulnerability"

2. **Folgende Informationen helfen uns:**
   - Beschreibung der Sicherheitslücke
   - Schritte zur Reproduktion
   - Betroffene Versionen
   - Mögliche Auswirkungen
   - Vorschläge zur Behebung (falls vorhanden)

3. **Erwarte eine Antwort innerhalb von:**
   - **48 Stunden**: Bestätigung des Erhalts
   - **7 Tage**: Erste Einschätzung
   - **30 Tage**: Geplanter Fix oder Workaround

## Unser Prozess

1. **Bestätigung** - Wir bestätigen den Erhalt deiner Meldung
2. **Bewertung** - Wir bewerten die Schwere und Auswirkung
3. **Entwicklung** - Wir entwickeln einen Fix
4. **Testing** - Wir testen den Fix gründlich
5. **Release** - Wir veröffentlichen einen Patch
6. **Veröffentlichung** - Wir veröffentlichen Details nach dem Fix

## Security Best Practices

Beim Verwenden dieser Extension:

### Dateiberechtigungen

```bash
# Ordner
chmod 755 user/themes/learn2/
chmod 755 user/pages/

# Dateien
chmod 644 user/themes/learn2/templates/*.twig
chmod 644 user/themes/learn2/css/*.css
chmod 644 user/pages/**/*.md
```

### Benutzer-generierter Content

Wenn du Kommentare oder Benutzer-generierten Content zulässt:

1. **Validiere Input**: Nutze Gravs eingebaute Validierung
2. **Sanitize Output**: Twig escaped automatisch, aber prüfe `|raw` Filter
3. **CSRF Protection**: Nutze Gravs Form Security
4. **Rate Limiting**: Implementiere Rate Limits für Formulare

### Uploads

Featured Images und andere Uploads:

```yaml
# In user/config/system.yaml
media:
  enable_media_timestamp: false
  unsupported_inline_types: []
  allowed_fallback_types: []
  auto_metadata_exif: false
```

Beschränke erlaubte Dateitypen:
```yaml
# In Blog-Item Blueprint
header.featured_image:
  type: file
  accept:
    - image/jpeg
    - image/png
    - image/webp
  limit: 1024  # KB
```

### Template-Sicherheit

In benutzerdefinierten Templates:

```twig
{# ✅ SICHER: Auto-escaped #}
{{ page.title }}
{{ user_input }}

{# ⚠️ VORSICHT: Nicht escaped #}
{{ page.content|raw }}

{# ✅ BESSER: Bedingtes escaping #}
{% if page.content is trusted %}
    {{ page.content|raw }}
{% else %}
    {{ page.content }}
{% endif %}
```

### Updates

- **Aktuell bleiben**: Halte Grav, Plugins und Themes aktuell
- **Patch-Releases**: Installiere Sicherheitsupdates zeitnah
- **Abhängigkeiten**: Überprüfe regelmäßig auf veraltete Abhängigkeiten

```bash
# Grav aktualisieren
bin/gpm selfupgrade

# Plugins aktualisieren
bin/gpm update

# Blog-Extension aktualisieren (wenn als Fork installiert)
cd user/themes/learn2
git pull origin main
```

### Grav-spezifische Sicherheit

Folge den [Grav Security Best Practices](https://learn.getgrav.org/17/advanced/security):

1. **Admin-Zugang schützen**:
   ```yaml
   # user/config/security.yaml
   security:
     salt: 'DEIN-EINDEUTIGER-SALT'
   ```

2. **Zwei-Faktor-Authentifizierung** aktivieren (Login Plugin)

3. **Starke Passwörter** verwenden

4. **Admin-URL ändern**:
   ```yaml
   # user/config/plugins/admin.yaml
   route: '/administrator'  # Statt /admin
   ```

5. **SSL/TLS verwenden** in Produktion

## Bekannte Sicherheitsaspekte

### Twig Template-Injection

**Risiko**: Mittel  
**Betrifft**: Benutzer mit Admin-Zugang

Nutzer mit Zugriff auf Template-Bearbeitung könnten potentiell Code ausführen. Dies ist Grav-Standard-Verhalten und kein Bug.

**Mitigation**:
- Beschränke Admin-Zugang auf vertrauenswürdige Nutzer
- Nutze Grav's Berechtigungssystem
- Aktiviere Audit-Logging

### Benutzer-Uploads

**Risiko**: Mittel

Unvalidierte Bild-Uploads könnten potentiell schädliche Dateien enthalten.

**Mitigation**:
- Validiere Dateitypen im Blueprint
- Nutze Grav's Media-Security-Features
- Beschränke Upload-Größen
- Speichere Uploads außerhalb des Web-Roots (Grav Standard)

## Sicherheits-Checkliste für Produktion

- [ ] Grav auf aktuellste Version aktualisiert
- [ ] Alle Plugins aktualisiert
- [ ] SSL/TLS aktiviert (HTTPS)
- [ ] Admin-Route geändert
- [ ] Starke Passwörter verwendet
- [ ] Dateiberechtigungen korrekt gesetzt
- [ ] Debug-Modus deaktiviert (`system.yaml`)
- [ ] Cache aktiviert
- [ ] Backup-Strategie implementiert
- [ ] Security-Headers konfiguriert (Server)
- [ ] Rate Limiting aktiviert (Server/Plugin)

## Server-Level Security

### Apache

`.htaccess` Ergänzungen:

```apache
# Security Headers
Header always set X-Frame-Options "SAMEORIGIN"
Header always set X-Content-Type-Options "nosniff"
Header always set X-XSS-Protection "1; mode=block"
Header always set Referrer-Policy "strict-origin-when-cross-origin"

# CSP Policy
Header always set Content-Security-Policy "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; img-src 'self' data:;"
```

### Nginx

```nginx
# Security Headers
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
```

## Hall of Fame

Wir danken den folgenden Personen für verantwortungsvolle Offenlegung:

<!-- 
- [Name] - [Beschreibung] - [Datum]
-->

*Noch keine Einträge*

## Weitere Ressourcen

- [Grav Security Guide](https://learn.getgrav.org/17/advanced/security)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Twig Security](https://twig.symfony.com/doc/3.x/api.html#sandbox-extension)
- [PHP Security Best Practices](https://www.php.net/manual/en/security.php)

## Kontakt

Für Sicherheitsfragen, die keine Schwachstellen sind:
- **GitHub Discussions**: [Link zu Discussions]
- **E-Mail**: [DEINE-EMAIL@example.com]

---

**Letzte Aktualisierung**: 14. Februar 2026
