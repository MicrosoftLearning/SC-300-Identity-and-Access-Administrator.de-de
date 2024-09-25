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

1. Um einen Bereich der Identitätssicherheit zu verbessern, wählen Sie **Anmelderisiko-Richtlinien von Microsoft Entra ID Protection aktivieren**.

2. Scrollen Sie in der daraufhin geöffneten Kachel nach unten, und wählen Sie **Erste Schritte** aus.

3. Eine neue Registerkarte wird für den **bedingten Zugriff** geöffnet.
 **Hinweis**: Standardmäßig wird die Schaltfläche „Erste Schritte“ im Azure-Portal geöffnet. Sie können das Portal verwenden oder zum Entra Admin Center zurückkehren. Beides wird funktionieren.

4. Wählen Sie **+ Neue Richtlinie** aus.

5. Benennen Sie Ihre Richtlinie. Es wird empfohlen, dass Unternehmen einen aussagekräftigen Standard für die Namen ihrer Richtlinien erstellen.

6. Wählen Sie unter Zuweisungen die Option Benutzer- oder Workloadidentitäten aus.

7. Wählen Sie unter Einschließen die Option Alle Benutzer aus.

8. Wählen Sie unter Ausschließen die Option Benutzer und Gruppen und dann alle Konten aus, die die Möglichkeit aufweisen müssen, die Legacyauthentifizierung zu verwenden. Microsoft empfiehlt, dass Sie mindestens ein Konto ausschließen, um zu verhindern, dass Sie ausgesperrt werden.

9. Wählen Sie unter Zielressourcen > Cloud-Apps > Einschließen die Option Alle Cloud-Apps aus.

10. Legen Sie unter Bedingungen > Client-Apps die Option Konfigurieren auf „Ja“ fest.
 - Aktivieren Sie nur die Kontrollkästchen Exchange ActiveSync-Clients und Andere Clients.

11. Wählen Sie Fertig aus.

12. Wählen Sie unter Kontrollen > Zuweisung die Option „Zugriff blockieren“ aus.

13. Wählen Sie Auswählen.

14. Bestätigen Sie die Einstellungen, und legen Sie Richtlinie aktivieren auf Nur Bericht fest.

15. Wählen Sie Erstellen aus, um die Richtlinie zu erstellen und zu aktivieren.
