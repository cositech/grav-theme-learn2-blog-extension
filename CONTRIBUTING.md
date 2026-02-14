# Contributing zu Learn2 Blog Extension

Vielen Dank für dein Interesse an diesem Projekt! Wir freuen uns über alle Beiträge.

## Code of Conduct

Dieses Projekt folgt dem [Grav Community Code of Conduct](https://getgrav.org/code-of-conduct). Durch deine Teilnahme erklärst du dich mit diesen Richtlinien einverstanden.

## Wie kann ich beitragen?

### Bugs melden

Bugs werden als [GitHub Issues](https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/issues) verfolgt.

**Bevor du einen Bug meldest:**

- Überprüfe, ob das Problem bereits gemeldet wurde
- Stelle sicher, dass du die neueste Version verwendest
- Überprüfe die Dokumentation

**Beim Melden eines Bugs:**

- Verwende einen klaren und beschreibenden Titel
- Beschreibe die genauen Schritte zur Reproduktion
- Beschreibe das beobachtete Verhalten
- Beschreibe das erwartete Verhalten
- Füge Screenshots hinzu, wenn möglich
- Gib Details zu deiner Umgebung an:
  - Grav Version
  - PHP Version
  - Browser und Version
  - Betriebssystem

### Features vorschlagen

Feature-Anfragen werden ebenfalls als GitHub Issues verfolgt.

**Beim Vorschlagen eines Features:**

- Verwende einen klaren und beschreibenden Titel
- Beschreibe das Problem, das gelöst werden soll
- Beschreibe die vorgeschlagene Lösung
- Beschreibe Alternativen, die du in Betracht gezogen hast
- Füge Mockups oder Beispiele hinzu, wenn hilfreich

### Pull Requests

**Bevor du einen Pull Request erstellst:**

1. Erstelle ein Issue, um deine Änderung zu diskutieren (außer bei kleinen Fixes)
2. Fork das Repository
3. Erstelle einen Branch von `main`
4. Halte deine Änderungen fokussiert und atomar
5. Schreibe aussagekräftige Commit-Messages

**Pull Request Prozess:**

1. **Fork und Clone**

   ```bash
   git clone https://github.com/DEIN-USERNAME/grav-theme-learn2-blog.git
   cd grav-theme-learn2-blog
   ```

2. **Branch erstellen**

   ```bash
   git checkout -b feature/mein-neues-feature
   # oder
   git checkout -b fix/mein-bugfix
   ```

3. **Änderungen machen**
   - Folge den Code-Style-Richtlinien (siehe unten)
   - Teste deine Änderungen gründlich
   - Aktualisiere die Dokumentation, falls nötig

4. **Commit**

   ```bash
   git add .
   git commit -m "Add: Beschreibung des Features"
   ```

5. **Push**

   ```bash
   git push origin feature/mein-neues-feature
   ```

6. **Pull Request öffnen**
   - Verwende die PR-Vorlage
   - Verlinke relevante Issues
   - Beschreibe deine Änderungen ausführlich

## Code-Style-Richtlinien

### Twig Templates

```twig
{# Kommentare mit Leerzeichen #}

{# Einrückung: 4 Leerzeichen #}
{% if condition %}
    <div class="example">
        {{ variable }}
    </div>
{% endif %}

{# Leerzeichen um Operatoren #}
{% set var = value %}

{# Mehrzeilige Ausdrücke ordentlich formatieren #}
{% set config = {
    'option1': value1,
    'option2': value2,
    'option3': value3
} %}
```

### CSS

```css
/* Kommentare in eigener Zeile */

/* Einrückung: 4 Leerzeichen */
.selector {
    property: value;
    another-property: value;
}

/* Leerzeile zwischen Selektoren */
.another-selector {
    property: value;
}

/* Eigenschaften alphabetisch sortieren */
.example {
    background: #fff;
    border: 1px solid #ccc;
    color: #333;
    margin: 1rem;
    padding: 1rem;
}

/* Mobile-First Media Queries */
@media (min-width: 768px) {
    .selector {
        property: value;
    }
}
```

### YAML

```yaml
# Kommentare mit Leerzeichen
key: value

# Einrückung: 2 Leerzeichen
nested:
  key: value
  another_key: value

# Listen
items:
  - item1
  - item2
  - item3
```

### Commit Messages

Verwende konventionelle Commit-Messages:

```
Type: Kurze Beschreibung (max 50 Zeichen)

Detaillierte Erklärung, wenn nötig (max 72 Zeichen pro Zeile).
Erkläre das "Warum", nicht das "Was".

Fixes #123
Closes #456
```

**Types:**

- `Add:` Neues Feature
- `Fix:` Bugfix
- `Update:` Änderung an bestehendem Feature
- `Remove:` Feature entfernt
- `Docs:` Nur Dokumentation
- `Style:` Code-Formatierung (keine funktionalen Änderungen)
- `Refactor:` Code-Refactoring
- `Test:` Tests hinzufügen/ändern
- `Chore:` Build-Prozess, Dependencies, etc.

**Beispiele:**

```
Add: Featured post support
Fix: Featured image not displaying on mobile
Update: Improve responsive layout for tablets
Docs: Add pagination setup instructions
```

## Dokumentation

Wenn du Features hinzufügst oder änderst:

- Aktualisiere die README.md
- Aktualisiere BLOG_README.md, falls relevant
- Füge inline-Kommentare für komplexen Code hinzu
- Aktualisiere CHANGELOG.md

## Testing

Teste deine Änderungen in verschiedenen Umgebungen:

**Browser:**

- Chrome/Edge (aktuell)
- Firefox (aktuell)
- Safari (aktuell, wenn möglich)
- Mobile Browser (iOS Safari, Chrome Mobile)

**Grav Versionen:**

- Mindestens die Minimum-Version (1.6)
- Aktuelle stabile Version

**Szenarien:**

- Frische Installation
- Mit und ohne relevante Plugins
- Mit verschiedenen Theme-Konfigurationen
- Mobile und Desktop

## Fragen?

- **Dokumentation:** [Grav Learn](https://learn.getgrav.org)
- **Forum:** [Grav Forum](https://getgrav.org/forum)
- **Chat:** [Grav Discord](https://chat.getgrav.org)
- **Issues:** [GitHub Issues](https://github.com/DEIN-USERNAME/grav-theme-learn2-blog/issues)

## Lizenz

Indem du zu diesem Projekt beiträgst, stimmst du zu, dass deine Beiträge unter der MIT-Lizenz lizenziert werden.

## Anerkennung

Alle Contributors werden in der README.md aufgeführt. Danke für deine Beiträge! 🎉
