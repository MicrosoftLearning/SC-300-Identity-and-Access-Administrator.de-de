---
lab:
  title: '28: Überwachen und Verwalten Ihres Sicherheitsstatus mit Identitätssicherheitsbewertung'
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 28: Überwachen und Verwalten Ihres Sicherheitsstatus mit Identitätssicherheitsbewertung

## Labszenario

Microsoft Entra-Identitätsschutz bietet automatisierte Erkennung und Behebung identitätsbasierter Risiken und stellt Daten im Portal bereit, um potenzielle Risiken zu untersuchen. Microsoft Entra-Identitätsschutz bietet auch eine Identitätssicherheitsbewertung, um Ihren Identitätssicherheitsstatus zu überwachen und zu verbessern.  Auf die gleiche Weise wie Microsoft Defender XDR und Microsoft Defender for Cloud bietet die Identitätssicherheitsbewertung Verbesserungsmaßnahmen und Empfehlungen, die Ihren allgemeinen Sicherheitsstatus für Identität in Microsoft Entra ID verbessern können.  In dieser Übung wird diese Funktion untersucht. 

#### Geschätzte Dauer: 15 Minuten

### Übung 1: Verwenden der Identitätssicherheitsbewertung zum Überwachen und Verwalten des Identitätssicherheitsstatus

#### Aufgabe 1: Überprüfen von Identitätssicherheitsbewertung und Verbesserungsaktionen

1. Melden Sie sich bei [https://entra.microsoft.com](https://entra.microsoft.com) als globaler Administrator an.

2. Öffnen sie das Menü **Schutz**, und wählen Sie **Identitätssicherheitsbewertung** aus

3. Auf der Kachel **Übersicht** befindet sich **Identitätssicherheitsbewertung**.

4. Wählen Sie **Identitätssicherheitsbewertung** aus.  Dadurch gelangen Sie zum Dashboard „Identitätssicherheitsbewertung“.

5. Scrollen Sie nach unten, um die **Verbesserungsaktionen** anzuzeigen.

6. Im Gegensatz zu den Verbesserungsmaßnahmen in Microsoft Defender for Cloud und Microsoft Defender XDR sind diese Verbesserungsmaßnahmen spezifisch für die Identität.  Damit erhalten Sie eine fokussiertere Liste potenzieller Aktionen für Ihre Sicherheitsstatusverwaltung.  Alle Verbesserungsaktionen, die aus dieser Liste initiiert werden, wirken sich auch auf Ihren gesamten Mandantensicherheitsstatus aus. 

#### Aufgabe 2: Ausführen einer Verbesserungsaktion

1. Um einen Bereich des Identitätssicherheitsstatus zu verbessern, wählen Sie **Alle Benutzer mit einer Richtlinie zum Anmelderisiko schützen** aus.

2. Scrollen Sie in der daraufhin geöffneten Kachel nach unten, und wählen Sie **Erste Schritte** aus.

3. Eine neue Registerkarte wird für **Identity Protection | Anmelderisiko-Richtlinie** geöffnet.

4. Wählen Sie **Alle Benutzer** unter **Zuweisungen** aus.

5. Wählen Sie unter **Anmelderisiko** die Option **Mittel und höher** aus.

6. Wählen Sie **Zugriff zulassen** - **Multi-Faktor-Authentifizierung erfordern** unter **Steuerungen** aus.

7. Legen Sie **Richtlinienerzwingung** auf **Aktiviert** fest (falls nicht bereits geschehen), und wählen Sie **Speichern** aus.

8. Sie haben eine Anmelderisiko-Richtlinie erstellt, die jetzt Ihre Identitätssicherheitsbewertung erhöhen sollte.  Es kann bis zu 24 Stunden dauern, bis sie sich auf Ihre Identitätssicherheitsbewertung auswirkt.

9. Sehen Sie sich weitere Verbesserungsaktionen und die Schritte, um sie zu erstellen und zu aktivieren, an.
