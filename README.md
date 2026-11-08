# familienplaner-kalender

Stündlich gespiegelter Familienkalender – **nur verschlüsselt**.

Ein GitHub-Actions-Workflow (`.github/workflows/kalender.yml`) lädt jede Stunde
zu Minute 50 den veröffentlichten iCloud-Kalender, verschlüsselt ihn mit
AES-256-CBC (PBKDF2, 200 000 Iterationen, Salt) und committet ausschließlich
`kalender.ics.enc` – und nur, wenn sich der Kalenderinhalt geändert hat.
Die unverschlüsselte ICS-Datei gelangt nie ins Repository.

Benötigte Actions-Secrets: `ICS_URL`, `KAL_PASS`.

Entschlüsseln:

```sh
openssl enc -d -aes-256-cbc -pbkdf2 -iter 200000 -pass env:KAL_PASS \
  -in kalender.ics.enc -out kalender.ics
```
