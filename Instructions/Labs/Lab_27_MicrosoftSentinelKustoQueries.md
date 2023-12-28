---
lab:
  title: 27 – Microsoft Sentinel Kusto Abfragen für Microsoft Entra-Datenquellen
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Übung 27 – Microsoft Sentinel Kusto Abfragen für Microsoft Entra-Datenquellen

**Hinweis** : Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen finden Sie in Lab 00.

## Labszenario

Microsoft Sentinel ist eine skalierbare, cloudnative SIEM- und SOAR-Lösung.  Durch das Verbinden von Datenquellen aus Microsoft- und Sicherheitslösungen von Drittanbietern haben Sie die Möglichkeit, Sicherheitsvorgänge auszuführen.  In dieser Übung erstellen Sie einen Microsoft Sentinel-Arbeitsbereich mit Datenconnectors zu Azure AD zum Ausführen von Suchabfragen mithilfe von Kusto-Abfragesprache (KQL). 

#### Geschätzte Dauer: 30 Minuten

### Übung 1 – Konfigurieren von Microsoft Sentinel für Kusto-Abfragen

#### Verwalten eines Microsoft Sentinel-Arbeitsbereichs

1. Melden Sie sich als globaler Administrator an.

1. Suchen Sie nach **Microsoft Sentinel**, und wählen Sie diese Lösung aus. 

1. Wählen Sie links oben **Ressource erstellen** aus.

1. Wählen Sie auf dem Bildschirm „Add Microsoft Sentinel to a workspace“ (Microsoft Sentinel einem Arbeitsbereich hinzufügen) die Option Neuen Arbeitsbereich erstellen.

1. Wählen Sie unter **Ressourcengruppe** die Option **Neu erstellen** aus, und geben Sie  ein.

1. Geben Sie dem Arbeitsbereich den Namen .  Beispiel : SentinelLogAnalytics.

1. Wählen Sie eine Region in Ihrer Nähe aus.

1. Wählen Sie **Überprüfen + erstellen** und danach **Erstellen** aus.

1. Nachdem die Bereitstellung des Log Analytics-Arbeitsbereichs abgeschlossen ist, wählen Sie die **Schaltfläche "Aktualisieren"** aus. Wählen Sie Ihren Arbeitsbereich und dann **Hinzufügen** aus.  Dadurch wird der Arbeitsbereich zu Microsoft Sentinel hinzugefügt und Microsoft Sentinel geöffnet.

1. Wenn Sie dazu aufgefordert werden, wählen Sie **"OK** " aus, um die kostenlose Testversion von Microsoft Sentinel zu aktivieren.

#### Aufgabe 2 : Hinzufügen von Azure AD als Datenquelle
    **Note** - As of 11/1/2023, the data source is still Azure AD (not Microsoft Entra ID)

1. Scrollen Sie im Bereich **Microsoft Sentinel** im linken Menü nach unten zu **Inhaltsverwaltung**, und wählen Sie **Content Hub** aus.

1. Verwenden Sie das Suchfeld, um in der Liste der Connectors nach Azure** zu suchen, Azure Active Directory** zu suchen **** und das Kontrollkästchen zu markieren.

1. Rechts wird eine Vorschaukachel geöffnet.  Wählen Sie **Installieren** aus.

1. Wählen Sie nach Abschluss der Installation das **Menüelement "Datenkonnektoren** " im Menü "Konfiguration" aus.

    **Hinweis**: Sie sollten 1 Verbinden or installiert anzeigen und microsoft Entra ID** aufgeführt sehen**.

1. Wählen Sie in der Liste Datenconnectors die Option Microsoft Entra ID und dann Connector-Seite öffnen aus.

1. Auf der Connectorseite werden die Anweisungen und nächsten Schritte für den Datenconnector bereitgestellt. Stellen Sie sicher, dass sich neben jedem der **Voraussetzungen** ein Häkchen befindet, um mit der **Konfiguration** fortzufahren.

1. Aktivieren Sie unter **"Konfiguration**" die Kontrollkästchen für **Anmeldeprotokolle** und **Überwachungsprotokolle**. Weitere Protokollquellen sind verfügbar, befinden sich jedoch derzeit in **der Vorschau** und außerhalb des Gültigkeitsbereichs für diesen Kurs.

1. Wählen Sie **Änderungen übernehmen** aus. 

1. Die Benachrichtigung wird bereitgestellt, dass die Änderungen erfolgreich angewendet wurden. Navigieren Sie zum **Microsoft Sentinel-Arbeitsbereich** , indem Sie oben rechts auf der Connectorseite das **X** auswählen.

1. Wählen Sie **"Aktualisieren"** in **Microsoft Sentinel | Kachel "Datenkonnektoren**" und die Zahl 1 werden in der **anzahl Verbinden angezeigt**.

   **Hinweis** : Der Azure AD-Datenconnector kann einige Minuten dauern, um die aktive Anzahl anzuzeigen. 

#### Aufgabe 3 – Ausführen der Kusto-Abfrage für Benutzeraktivitäten

1. Navigieren Sie in **Microsoft Sentinel** unter der **Menüüberschrift "Allgemein**" zu **"Protokolle**".

1. Schließen Sie bei Bedarf das Fenster **Willkommen bei Log Analytics!** .

1. Ein Fenster wird mit Beispielabfragen geöffnet, "Überwachen"** und **"Suchen nach **Benutzer-IDs**" ausgewählt.

1. Klicken Sie auf **Run** (Ausführen). 

1. Dadurch wird eine Liste der Benutzer-IDs auf der Microsoft Entra-ID bereitgestellt.  Da wir gerade den Arbeitsbereich erstellt haben, werden möglicherweise keine Ergebnisse angezeigt.  Beachten Sie das Format der Abfrage.

1. Wählen Sie unter **"Bedrohungsverwaltung**" im Menü "Suche"** aus**. 

1. Scrollen Sie nach unten, um den Anomalen Anmeldespeicherort der Abfrage **nach Benutzerkonto und Authentifizierungsanwendung** zu finden.  Diese Abfrage über die Microsoft Entra-Anmeldung berücksichtigt alle Benutzeranmeldungen für jede Microsoft Entra-Anwendung und wählt die aomale Änderung des Standortprofils für einen Benutzer innerhalb einer einzelnen Anwendung aus. Die Absicht besteht darin, nach einer Kompromittierung des Benutzerkontos zu suchen, möglicherweise über einen bestimmten Anwendungsvektor. 

1. Wählen Sie **Ausführen** aus, um die Abfrageergebnisse anzuzeigen.

1. Dies liefert möglicherweise keine Ergebnisse mit dem neuen Arbeitsbereich, aber Sie haben jetzt gesehen, wie Abfragen ausgeführt werden können, um Informationen zu sammeln oder potenzielle Bedrohungen zu suchen.
