# Familienkalender – Einrichtung (einmalig, ca. 15 Minuten)

Du richtest das einmal ein. Christin und John bekommen danach nur einen Link,
sie brauchen kein Konto und müssen nichts einrichten.

## 1. Dateien auf GitHub hochladen

1. Auf github.com anmelden und oben rechts **+ → New repository** wählen.
2. Name: `familienkalender`, **Public** auswählen, auf **Create repository** tippen.
3. Auf der neuen Seite auf **uploading an existing file** tippen.
4. Alle Dateien aus diesem Ordner hochladen: `index.html`, `manifest.webmanifest`,
   `sw.js`, `icon-192.png`, `icon-512.png` (die Anleitung und `firestore.rules` sind optional).
5. Unten auf **Commit changes** tippen.

## 2. Webseite einschalten (GitHub Pages)

1. Im Repository auf **Settings → Pages** gehen.
2. Bei **Branch** `main` und `/ (root)` wählen und **Save** tippen.
3. Nach 1–2 Minuten steht dort deine Adresse, z. B.
   `https://robertpahl1987-creator.github.io/familienkalender/`

## 3. Kostenlose Datenbank anlegen (Firebase)

1. Auf **console.firebase.google.com** mit deinem Google-Konto anmelden.
2. **Projekt erstellen**, Name z. B. `familienkalender`. Google Analytics kannst du ausschalten.
3. Im Projekt auf das **Web-Symbol `</>`** tippen, App-Name `Familienkalender` eingeben und
   **App registrieren** wählen. Hosting musst du nicht ankreuzen.
4. Es erscheint ein Code-Block `const firebaseConfig = { … }`. **Den ganzen Block kopieren.**
5. Links im Menü **Build → Firestore Database → Datenbank erstellen** wählen.
   - Standort: **europe-west3 (Frankfurt)**
   - **Im Produktionsmodus starten**

## 4. Datenbank-Regeln setzen

1. In Firestore oben auf den Reiter **Regeln** gehen.
2. Alles löschen und Folgendes einfügen (steht auch in `firestore.rules`):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /familien/{code}/eintraege/{eintrag} {
      allow read, write: if code.size() >= 18;
    }
  }
}
```

3. Auf **Veröffentlichen** tippen.

## 5. App verbinden und Familie einladen

1. Deine Adresse aus Schritt 2 auf dem Handy öffnen.
2. Im Fenster **Einrichtung** den kopierten Firebase-Block einfügen und auf **Verbinden** tippen.
3. Oben rechts auf das **Personen-Symbol** tippen und den **Einladungslink**
   per WhatsApp an Christin und John schicken.
4. Auf jedem Handy im Chrome-Menü **„Zum Startbildschirm hinzufügen“** wählen.
   Dann ist der Kalender wie eine normale App da.

## Gut zu wissen

- **Kostenlos:** Der Firebase-Gratistarif (Spark) reicht für eine Familie locker. Du musst keine Zahlungsdaten hinterlegen.
- **Sicherheit:** Wer den Einladungslink hat, kann den Kalender sehen und ändern.
  Gib ihn also nur an die Familie. Wenn er mal in falsche Hände gerät: in der App auf
  „Auf diesem Handy trennen“ tippen, neu verbinden (dabei entsteht ein neuer Code) und den neuen Link verschicken.
- **Offline:** Termine werden gespeichert und automatisch übertragen, sobald wieder Internet da ist.
- **6 Uhr morgens:** Der Wecker im Handy erinnert dich. Die Tagesübersicht in der App bleibt stehen,
  bis man auf „Gelesen ✓“ tippt.

## Datenschutz & Impressum

- Die Seite `datenschutz.html` ist in der App unten und unter „Teilen & Einstellungen“ verlinkt.
- Die App lädt keine Google-Schriften und nutzt kein Google Analytics.
- Unter „Teilen & Einstellungen“ gibt es „Alle Termine exportieren (.ics)“ und „Kalender endgültig löschen“.

## Nur-Lese-Links (z. B. für Papa) – einmalig einschalten

1. console.firebase.google.com → Projekt **familienkalender**
2. Links **Sicherheit → Authentication** → „Jetzt starten“ → Reiter **Anmeldemethode** → **Anonym** → aktivieren → Speichern
3. **Firestore Database → Regeln**: alles ersetzen durch den Inhalt von `firestore.rules` → **Veröffentlichen**
4. In der App: Personen-Symbol → „Nur-Lese-Links“ → Name eingeben, Spalte(n) wählen → „Nur-Lese-Link erstellen“
