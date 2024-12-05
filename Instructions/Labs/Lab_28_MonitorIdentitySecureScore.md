---
lab:
  title: '28: Überwachen und Verwalten Ihres Sicherheitsstatus mit Identitätssicherheitsbewertung'
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 28: Überwachen und Verwalten Ihres Sicherheitsstatus mit Identitätssicherheitsbewertung

### Anmeldetyp = Microsoft 365 Admin

## Labszenario

Microsoft Entra-Identitätsschutz bietet automatisierte Erkennung und Behebung identitätsbasierter Risiken und stellt Daten im Portal bereit, um potenzielle Risiken zu untersuchen. Microsoft Entra-Identitätsschutz bietet auch eine Identitätssicherheitsbewertung, um Ihren Identitätssicherheitsstatus zu überwachen und zu verbessern.  Auf die gleiche Weise wie Microsoft Defender XDR und Microsoft Defender for Cloud bietet die Identitätssicherheitsbewertung Verbesserungsmaßnahmen und Empfehlungen, die Ihren allgemeinen Sicherheitsstatus für Identität in Microsoft Entra ID verbessern können.  In dieser Übung wird diese Funktion untersucht. 

**Hinweis** : Da dieses Lab in einer neuen erstellten Mandantenumgebung ausgeführt wird, erhalten Sie wahrscheinlich eine Identitätssicherheitsbewertung von 0,00 %.  Es dauert etwa 24 Stunden, bis wertvolle Daten in die Berechnung eingegeben werden, um Ihnen eine gültige Bewertung zu geben.

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

1. Um einen Bereich der Identitätssicherheit zu verbessern, wählen Sie **Anmeldungsrisiko-Richtlinie von Microsoft Entra ID Protection aktivieren**.

2. Scrollen Sie in der daraufhin geöffneten Kachel nach unten, und wählen Sie **Erste Schritte** aus.

3. Eine neue Registerkarte wird für **Identity Protection | Anmelderisiko-Richtlinie** geöffnet.
 **Hinweis**: Standardmäßig wird die Schaltfläche „Erste Schritte“ im Azure-Portal geöffnet. Sie können das Portal verwenden oder zum Entra Admin Center zurückkehren. Beides wird funktionieren.

6. Unter „Aufgaben“ wählen Sie den Text **Alle Benutzer**.

7. Wählen Sie unter Einschließen die Option Alle Benutzer aus.

8. Wählen Sie unter „Ausschließen“ die Option „Benutzer und Gruppen“ aus und wählen Sie Ihr **MOD-Administratorkonto** aus.

  - Microsoft empfiehlt, dass Sie mindestens ein Konto ausschließen, um zu verhindern, dass Sie ausgesperrt werden.

9. Unter „Anmelderisiko“ wählen Sie den Text aus, der **Niedrig und höher** lautet.

10. Wählen Sie **Mittel und höher** und dann **Fertig**.

10. Wählen Sie im Abschnitt **Steuerelemente** den Text **Zugriff blockieren** aus.

11. Wählen Sie **Zugriff zulassen – Multi-Faktor-Authentifizierung erforderlich**.

11. Wählen Sie Fertig aus.

14. Bestätigen Sie Ihre Einstellungen und setzen Sie die Richtliniendurchsetzung auf **Aktiviert**.

15. Wählen Sie **Speichern**.
