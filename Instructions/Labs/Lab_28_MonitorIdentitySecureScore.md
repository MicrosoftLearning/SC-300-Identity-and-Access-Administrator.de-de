---
lab:
  title: 'Lab: Überwachen und Verwalten Ihres Sicherheitsstatus mit Identitätssicherheitsbewertung'
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab: Überwachen und Verwalten Ihres Sicherheitsstatus mit Identitätssicherheitsbewertung

## Labszenario

Microsoft Entra Identity Protection bietet automatisierte Erkennung und Behebung identitätsbasierter Risiken und stellt Daten im Portal bereit, um potenzielle Risiken zu untersuchen. Microsoft Entra Identity Protection bietet auch eine Identitätssicherheitsbewertung, um Ihren Identitätssicherheitsstatus zu überwachen und zu verbessern.  Auf die gleiche Weise wie Microsoft 365 Defender und Microsoft Defender für Cloud bietet Identity Secure Score Verbesserungsmaßnahmen und Empfehlungen, die Ihren allgemeinen Sicherheitsstatus für Identität in Microsoft Entra ID verbessern können.  In dieser Übung wird diese Funktion untersucht. 

#### Geschätzte Dauer: 15 Minuten

### Übung 1 – Verwenden der Identitätssicherheitsbewertung zum Überwachen und Verwalten des Identitätssicherheitsstatus

#### Aufgabe 1 – Überprüfen von Sicherheitsbewertungs- und Verbesserungsmaßnahmen für Identitäten

1. Melden Sie sich als globaler Administrator an.

2. Öffnen sie das **Menü "Schutz** ", und wählen Sie "Identitätssicherheitsbewertung" aus **.**

3. Auf der **Kachel "Übersicht"** finden **Sie die Identitätssicherheitsbewertung**.

4. Identitätssicherheitsbewertung.  Dadurch gelangen Sie zum Dashboard für die Identitätssicherheitsbewertung.

5. Scrollen Sie nach unten, um die **Verbesserungsaktionen** anzuzeigen.

6. Im Gegensatz zu den Verbesserungsmaßnahmen in Microsoft Defender für Cloud und Microsoft 365 Defender sind diese Verbesserungsmaßnahmen für identitätsspezifisch.  Dies bietet eine fokussiertere Liste potenzieller Aktionen für Ihre Sicherheitsstatusverwaltung.  Alle Verbesserungsmaßnahmen, die aus dieser Liste initiiert werden, wirken sich auch auf Ihren gesamten Mandantensicherheitsstatus aus. 

#### Aufgabe 2 – Ausführen einer Verbesserungsaktion

1. Um einen Bereich des Identitätssicherheitsstatus zu verbessern, wählen Sie " **Alle Benutzer mit einer Anmelderisikorichtlinie schützen"** aus.

2. Scrollen Sie in der daraufhin geöffneten Kachel nach unten, und wählen Sie "Erste Schritte **" aus**.

3. Eine neue Registerkarte wird für **Identitätsschutz geöffnet | Anmelderisikorichtlinie**.

4. Wählen Sie **"Alle Benutzer** " unter **"** Aufgaben" aus.

5. Wählen Sie unter **Anmelderisiko** die Option **Mittel und darüber** aus.

6. Klicken Sie unter **Zugriffssteuerung** - **Gewähren** auf **Mehrstufige Authentifizierung anfordern**.

7. Aktivieren Sie die Richtlinienerzwingung** auf **"Aktiviert"** (sofern noch nicht geschehen), und wählen Sie "Speichern" aus****.**

8. Sie haben eine Anmelderisikorichtlinie erstellt, die jetzt Ihre Identitätssicherheitsbewertung erhöhen sollte.  Dies dauert bis zu 24 Stunden, bis sie sich auf Ihre Identitätssicherheitsbewertung auswirken.

9. Überprüfen Sie weitere Verbesserungsmaßnahmen und die Schritte zum Erstellen und Aktivieren.
