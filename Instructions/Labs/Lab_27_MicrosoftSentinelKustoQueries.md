---
lab:
  title: 27 – Microsoft Sentinel Kusto Abfragen für Microsoft Entra-Datenquellen
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 27 (optional) – Microsoft Sentinel Kusto Abfragen für Microsoft Entra-Datenquellen

**Hinweis** : Dieses Lab kann zurzeit nicht in der bereitgestellten Schulungsumgebung abgeschlossen werden.  Wir verlassen den Übungsschritt hier, damit Sie es optional in Ihrer BYOS-Umgebung (Bring You Own Subscription) ausprobieren können.  Lesen Sie die Schritte, um zu sehen, was möglich ist.  Wir arbeiten aktiv daran, dieses Lab zu aktualisieren, um eine Lösung in der Lab-Umgebung zu finden, und werden es bald aktualisieren.

### Anmeldetyp = Azure Resource-Anmeldung

## Labszenario

Microsoft Sentinel ist eine skalierbare, cloudnative SIEM- und SOAR-Lösung von Microsoft.  Durch das Verbinden von Datenquellen aus Microsoft- und Drittanbieter-Sicherheitslösungen haben Sie die Möglichkeit, Aufgaben für Security Operations auszuführen.  In dieser Labübung werden Sie einen Microsoft Sentinel-Arbeitsbereich mit Datenconnectors zu Microsoft Entra ID zum Ausführen von Suchabfragen mithilfe der Kusto Query Language (KQL) erstellen. 

#### Geschätzte Dauer: 30 Minuten

### Übung 1: Konfigurieren von Microsoft Sentinel für Kusto-Abfragen

#### Aufgabe 1: Erstellen eines Microsoft Sentinel-Arbeitsbereichs

1. Melden Sie sich bei [https://portal.azure.com](https://portal.azure.com) als globaler Administrator an.

1. Suchen Sie nach **Microsoft Sentinel**, und wählen Sie diese Option aus. 

1. Wählen Sie **+ Erstellen** in der oberen linken Ecke aus.

1. Wählen Sie in der Kachel **Hinzufügen von Microsoft Sentinel zu einem Arbeitsbereich** **+ Neuen Arbeitsbereich erstellen** aus.

1. Wählen Sie unter **Ressourcengruppe** die Option **Neu erstellen** aus, und geben Sie **Sentinel-RG** ein.

1. Geben Sie dem Arbeitsbereich den Namen.  Beispiel: SentinelLogAnalytics.

1. Wählen Sie eine Region in Ihrer Nähe aus.

1. Wählen Sie **Überprüfen + erstellen** und danach **Erstellen** aus.

1. Nachdem die Bereitstellung des Log Analytics-Arbeitsbereichs abgeschlossen ist, wählen Sie die Schaltfläche **Aktualisieren** aus. Wählen Sie Ihren Arbeitsbereich und dann **Hinzufügen** aus.  Dadurch wird der Arbeitsbereich zu Microsoft Sentinel hinzugefügt und Microsoft Sentinel geöffnet.

1. Wenn Sie dazu aufgefordert werden, wählen Sie **OK** aus, um die kostenlose Testversion von Microsoft Sentinel zu aktivieren.

#### Aufgabe 2 – Hinzufügen von Microsoft Entra ID als Datenquelle

1. Navigieren Sie in **Microsoft Sentinel** zum Menü zur **Content-Verwaltung** und wählen Sie **Content-Hub**aus.

1. Verwenden Sie das Suchfeld, um in der Liste der Connectors nach **Entra** und dann **Microsoft Entra ID** zu suchen und das Kontrollkästchen zu markieren.

1. Rechts wird eine Vorschaukachel geöffnet.  Wählen Sie **Installieren** aus.

1. Wählen Sie nach Abschluss der Installation das Menüelement **Datenconnectors** im Konfigurationsmenü aus.

    **Hinweis**: Sie sollten 1 Connector installiert und **Microsoft Entra ID** aufgeführt sehen.

1. Wählen Sie **Microsoft Entra ID** und dann **Connector-Seite öffnen** aus.

1. Auf der Connectorseite werden die Anweisungen und nächsten Schritte für den Datenconnector angezeigt. Vergewissern Sie sich, dass alle **Voraussetzungen** aktiviert sind (ein Häkchen ist vorhanden), um mit der **Konfiguration** fortzufahren.

1. Aktivieren Sie unter **Konfiguration** die Kontrollkästchen für **Anmeldeprotokolle** und **Überwachungsprotokolle**. Weitere Protokollquellen sind verfügbar, befinden sich jedoch derzeit in der **Vorschau** und außerhalb des Gültigkeitsbereichs für diesen Kurs.

1. Klicken Sie auf **Änderungen übernehmen**. 

1. Es wird eine Benachrichtigung angezeigt, dass die Änderungen erfolgreich angewendet wurden. Navigieren Sie zum Arbeitsbereich **Microsoft Sentinel**, indem Sie rechts oben auf der Connectorseite das **X** auswählen.

1. Wählen Sie **Aktualisieren** in der Kachel **Microsoft Sentinel | Datenconnectors** aus, und die Zahl 1 wird in der Anzahl für **Verbunden** angezeigt.

   **Hinweis:** Der Microsoft Entra ID-Datenconnector kann einige Minuten dauern, um die aktive Anzahl anzuzeigen. 

#### Aufgabe 3: Ausführen der Kusto-Abfrage für Benutzeraktivitäten

1. Navigieren Sie in **Microsoft Sentinel** unter der Menüüberschrift **Allgemein** zu **Protokolle**.

1. Schließen Sie bei Bedarf das Fenster **Willkommen bei Log Analytics!**.

1. Ein Fenster mit Beispielabfragen wird geöffnet, wählen Sie **Überprüfung** aus und suchen Sie nach **Benutzer-IDs**.

1. Klicken Sie auf **Run** (Ausführen). 

1. Dadurch wird eine Liste der Benutzer-IDs auf der Microsoft Entra ID bereitgestellt.  Da wir den Arbeitsbereich gerade erst erstellt haben, werden möglicherweise keine Ergebnisse angezeigt.  Beachten Sie das Format der Abfrage.
