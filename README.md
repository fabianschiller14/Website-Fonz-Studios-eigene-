# fonz.studios

Die Website von Fonz Studios. Eine einzelne HTML-Datei ohne Framework, ohne
Bauschritt und ohne Abhängigkeiten. Wer sie öffnet, sieht sie; wer sie
hochlädt, hat sie online.

---

## Wichtig, bevor ihr das Repository anlegt

**Stellt es auf „Private".** In einem öffentlichen Repository kann jeder
alles lesen, und hier liegen Dinge, die niemanden von außen etwas angehen:

- die sechs Entwurfsseiten mit Namen, Adressen und Fotos von Betrieben, die
  uns noch nicht erlaubt haben, ihre Entwürfe zu zeigen,
- die Rechtsprüfung und die Liste der offenen Punkte unter `doku/`,
- die Liste unserer eigenen Fehler in `doku/bau-regeln.md`.

Für den Betrieb der Seite muss das Repository nicht öffentlich sein. Vercel
und Netlify lesen auch aus privaten Repositories.

---

## Hochladen

### Bei GitHub

1. Neues Repository anlegen, Sichtbarkeit **Private**.
2. Alle Dateien aus diesem Ordner hineinziehen, mitsamt der Unterordner.
3. Fertig. Es gibt nichts zu bauen und nichts zu installieren.

### Von dort ins Netz, mit Vercel

1. Auf vercel.com „Add New… → Project" und das Repository auswählen.
2. Framework Preset: **Other**.
3. Build Command: **leer lassen**. Output Directory: **leer lassen**.
4. „Deploy".

Vercel nimmt `index.html` als Startseite und `404.html` für Adressen, die es
nicht gibt. Beides passiert von allein, es muss nichts eingestellt werden.

---

## Was wo liegt

```
index.html                       die ganze Seite, deutsch und englisch
404.html                         Seite für falsche Adressen
robots.txt                       was Suchmaschinen lesen dürfen
sitemap.xml                      Verzeichnis für Suchmaschinen
vorschau.png                     Bild beim Teilen (WhatsApp, Social Media)

schriften/                       → hier fehlen noch drei Dateien, siehe darin

projekt-toshi-sushi.html         die sechs Entwürfe
projekt-med-duerum.html
projekt-helmar-federowski.html
projekt-gut-grossschoenau.html
projekt-hirsch-cut-style.html
projekt-zu-den-linden.html

doku/                            Arbeitsunterlagen, nicht für Besucher
bau/                             Werkzeug zum Umbauen und Prüfen
```

Die Ordner `doku/` und `bau/` dürfen mit hochgeladen werden. Sie stören den
Betrieb nicht: Vercel liefert nur aus, was jemand direkt aufruft, und auf
diese Dateien verweist nichts.

---

## Die Entwurfsseiten

Die sechs `projekt-*.html` sind **Gestaltungsentwürfe**, keine offiziellen
Auftritte der genannten Betriebe. Jede trägt dafür

- `<meta name="robots" content="noindex, nofollow">`, damit Google sie nicht
  aufnimmt und sie niemand über die Suche für die echte Seite hält,
- einen festen Hinweisbalken am unteren Rand, der genau das sagt.

**Sie liegen derzeit noch in der alten Fassung bei Vercel.** Der Hinweisbalken
greift erst, wenn sie neu hochgeladen sind.

---

## Zwei Sprachen

Die Seite ist auf Deutsch geschrieben. Englisch entsteht beim Klick auf
**EN** oben rechts: ein Wörterbuch in `bau/sprache.py` tauscht jeden
sichtbaren Text, auch die Entwürfe und den Planer, die erst beim Antippen
entstehen. Die Wahl bleibt beim nächsten Besuch erhalten.

Impressum und Datenschutz bleiben bewusst deutsch. Es sind verbindliche
Texte; eine Übersetzung wäre eine zweite Rechtslage, und im Streitfall gälte
die für uns ungünstigere Lesart. In der englischen Ansicht steht ein Hinweis
darüber.

### Wenn ihr einen Text ändert

Jeder geänderte deutsche Satz braucht seinen englischen in
`bau/sprache.py`, sonst steht an der Stelle plötzlich Deutsch. Danach:

```bash
node bau/pruefe_sprache.js      # muss „OHNE ÜBERSETZUNG: 0" melden
```

---

## Prüfen vor jedem Hochladen

```bash
python3 bau/pruefe_html.py index.html 404.html projekt-*.html
node     bau/pruefe_sprache.js
node     bau/test_sprache.js
```

`pruefe_html.py` bildet die Regeln des W3C-Prüfers nach, die bei einer
handgeschriebenen Seite wirklich greifen: unerlaubte Attribute, doppelte
`id`, Verweise ins Leere, Bilder ohne Alternativtext. Findet der echte
Prüfer auf validator.w3.org einmal etwas, das dieser hier nicht kennt,
gehört die Regel ergänzt, nicht nur die eine Stelle repariert.

Die Regeln und die Fehler, aus denen sie entstanden sind, stehen in
`doku/bau-regeln.md`. Dort nachzulesen, bevor jemand größer umbaut, spart
einen halben Abend.

---

## Was noch offen ist

Die vollständige Liste steht in `doku/VOR-DEM-ONLINEGANG.md`. Das Wichtigste:

1. **Die drei Schriftdateien** nach `schriften/` legen.
2. **Die Internetadresse kaufen.** In der Seite steht überall
   `https://fonz.studios/`. Wird es eine andere, müssen `og:`-Angaben,
   der strukturierte Datensatz, `robots.txt` und `sitemap.xml` mitziehen.
3. **Die sechs Betriebe fragen**, ob wir ihre Entwürfe zeigen dürfen.
4. **Die Entwurfsseiten neu hochladen**, damit der Hinweisbalken greift.
5. **Fremde Inhalte in den Entwürfen ersetzen**: Google Fonts lokal,
   Karten und Videos erst nach einem Klick laden.

---

## Fassung

Die aktuelle Fassung steht im Kommentar ganz oben im `<head>` von
`index.html`. Sucht im Quelltext nach `Fassung:` — dort steht heute:

```
Fassung: 2026-11-07-2135
```

Bei jeder Änderung mitziehen. Zweimal kam schon ein Fehlerbericht zu einer
Datei, die längst ersetzt war; mit der Nummer ist das in zehn Sekunden
geklärt.
