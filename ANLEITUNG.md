# Wichtel-Webseite online stellen

Die Seite liegt auf **GitHub** und läuft auf **Vercel**. Login und Datenbank kommen von **Firebase** (Google).
Für ein paar Freunde ist alles gratis (Firebase Spark-Plan, keine Kreditkarte nötig).
Einmal einrichten dauert etwa 15 Minuten.

## 1. Firebase-Projekt anlegen

1. Geh auf https://console.firebase.google.com und melde dich mit deinem Google-Konto an.
2. **Projekt hinzufügen** → Name z. B. `wichteln-2026` → Google Analytics kannst du ausschalten → **Projekt erstellen**.

## 2. Login mit Passwort einschalten

1. Links im Menü: **Build → Authentication** → **Jetzt starten**.
2. Reiter **Anmeldemethode** → **E-Mail-Adresse/Passwort** → **Aktivieren** → **Speichern**.
   (Deine Freunde brauchen keine E-Mail. Die Seite macht aus dem Benutzernamen intern eine Login-Adresse.)

## 3. Datenbank anlegen

1. Links: **Build → Firestore Database** → **Datenbank erstellen**.
2. Standort: `eur3 (europe-west)` oder `europe-west6 (Zürich)` → **Weiter**.
3. **Im Produktionsmodus starten** → **Erstellen**.

## 4. Web-App registrieren und Werte eintragen

1. Oben links auf das Zahnrad → **Projekteinstellungen** → ganz unten **Meine Apps** → Symbol **</>** (Web).
2. Name z. B. `wichteln` → **Hosting nicht ankreuzen** → **App registrieren**.
3. Du siehst einen Block `const firebaseConfig = { apiKey: ..., ... }`.
   Kopiere die Werte in die Datei `public/firebase-config.js` (oder schick sie mir, dann trage ich sie ein).
   Diese Werte sind nicht geheim, sie dürfen in der Webseite stehen.

## 5. Datenbank-Regeln einfügen

1. **Firestore Database → Regeln**.
2. Den ganzen Inhalt von `firestore.rules` hineinkopieren (alles Alte ersetzen) → **Veröffentlichen**.

Ohne diesen Schritt kann niemand etwas speichern.

## 6. Online stellen (GitHub + Vercel)

Der Code liegt auf GitHub, Vercel stellt die Seite online (Projekt-Einstellung: Framework «Other», Output-Ordner `public`, steht schon in `vercel.json`).
Jeder Push auf `main` aktualisiert die Seite automatisch.

Die Vercel-Adresse, z. B. `https://wichteln.vercel.app`, **ist der Link für deine Freunde.**

## 7. Wichtig: Du registrierst dich zuerst

Wer sich als **Erstes** registriert, wird automatisch Organisator.
Öffne also den Link und registriere dich, **bevor** du ihn verschickst.
Als Organisator kannst du:
- früher auslosen («Jetzt schon auslosen»),
- neu auslosen, falls jemand zu spät kommt,
- Wunschzettel löschen,
- deinen eigenen Zettel auch nach der Frist noch ändern.

## Wie es abläuft

- Bis **30. November, Mitternacht** tragen alle 3 bis 5 Wünsche ein (insgesamt 50–75 CHF, höchstens 75).
- Am **1. Dezember** wird automatisch ausgelost, sobald jemand die Seite öffnet.
- Alle sehen nur, wen **sie selbst** beschenken. Die Zuteilung ist mit dem Passwort der Person verschlüsselt.
  Auch du als Organisator siehst sie nicht, nicht einmal in der Firebase-Konsole.

## Passwort vergessen?

Es gibt kein «Passwort zurücksetzen». Lösche in der Firebase-Konsole unter **Authentication → Nutzer** das Konto
und in **Firestore** die Dokumente `users/<id>`, `keys/<id>` und `wichtel/<id>`. Die Person registriert sich dann neu.
Nach der Auslosung musst du danach **neu auslosen**, sonst kann sie ihre Zuteilung nicht lesen.
