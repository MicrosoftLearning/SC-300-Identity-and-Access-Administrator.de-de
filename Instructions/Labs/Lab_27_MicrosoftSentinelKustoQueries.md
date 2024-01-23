---
lab:
  title: '27: Erkunden von Microsoft Sentinel-Kusto-Abfragen für Azure AD-Datenquellen'
  learning path: '04'
  module: Module 04 - Plan and Implement and Identity Governance Strategy
---

# Lab 27: Erkunden von Microsoft Sentinel-Kusto-Abfragen für Azure AD-Datenquellen

**Hinweis**: Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen dazu finden Sie in Lab 00.

## Labszenario

Microsoft Sentinel ist eine skalierbare, cloudnative SIEM- und SOAR-Lösung von Microsoft.  Durch das Verbinden von Datenquellen aus Microsoft- und Drittanbieter-Sicherheitslösungen haben Sie die Möglichkeit, Aufgaben für Security Operations auszuführen.  In dieser Übung erstellen Sie einen Microsoft Sentinel-Arbeitsbereich mit Datenconnectors zu Azure AD für die Ausführung von Hunting-Abfragen mithilfe der Kusto-Abfragesprache (KQL). 

#### Geschätzte Dauer: 30 Minuten

### Übung 1: Konfigurieren von Microsoft Sentinel für Kusto-Abfragen

#### Aufgabe 1: Erstellen eines Microsoft Sentinel-Arbeitsbereichs

1. Melden Sie sich bei [https://portal.azure.com](https://portal.azure.com) als globaler Administrator an.

1. Suchen Sie nach **Microsoft Sentinel**, und wählen Sie diese Option aus. 

1. Wählen Sie **Microsoft Sentinel erstellen** aus.

1. Wählen Sie auf der Kachel **Add Microsoft Sentinel to a workspace** die Option **Neuen Arbeitsbereich erstellen** aus.

1. Wählen Sie unter **Ressourcengruppe** die Option **Neu erstellen** aus, und geben Sie **Sentinel-RG** ein.

1. Geben Sie dem Arbeitsbereich den Namen.  Beispiel: SentinelLogAnalytics.

1. Wählen Sie eine Region in Ihrer Nähe aus.

1. Wählen Sie **Überprüfen + erstellen** und danach **Erstellen** aus.

1. Nachdem die Bereitstellung des Log Analytics-Arbeitsbereichs abgeschlossen ist, wählen Sie die Schaltfläche **Aktualisieren** aus. Wählen Sie Ihren Arbeitsbereich und dann **Hinzufügen** aus.  Dadurch wird der Arbeitsbereich zu Microsoft Sentinel hinzugefügt und Microsoft Sentinel geöffnet.

1. Wenn Sie dazu aufgefordert werden, wählen Sie **OK** aus, um die kostenlose Testversion von Microsoft Sentinel zu aktivieren.

#### Aufgabe 2: Hinzufügen von Azure AD als Datenquelle

1. Navigieren Sie in **Microsoft Sentinel** im Menü zu **Konfiguration**, und wählen Sie **Datenconnectors** aus.

1. Suchen Sie in der Liste der „Datenconnectors“ nach **Azure Active Directory**, und wählen Sie sie aus.

1. Rechts wird eine Vorschaukachel geöffnet.  Wählen Sie **Connectorseite öffnen** aus.

1. Auf der Connectorseite werden die Anweisungen und nächsten Schritte für den Datenconnector angezeigt. Vergewissern Sie sich, dass alle **Voraussetzungen** aktiviert sind (ein Häkchen ist vorhanden), um mit der **Konfiguration** fortzufahren.

1. Aktivieren Sie unter **Konfiguration** die Kontrollkästchen für **Anmeldeprotokolle** und **Überwachungsprotokolle**. Weitere Protokollquellen sind verfügbar, befinden sich jedoch derzeit in der **Vorschau** und außerhalb des Gültigkeitsbereichs für diesen Kurs.

1. Wählen Sie **Änderungen übernehmen** aus. 

1. Es wird eine Benachrichtigung angezeigt, dass die Änderungen erfolgreich angewendet wurden. Navigieren Sie zum Arbeitsbereich **Microsoft Sentinel**, indem Sie rechts oben auf der Connectorseite das **X** auswählen.

1. Wählen Sie **Aktualisieren** in der Kachel **Microsoft Sentinel | Datenconnectors** aus, und die Zahl 1 wird in der Anzahl für **Verbunden** angezeigt.

   **Hinweis**: Es kann einige Minuten dauern, bis der Azure AD-Datenconnector die aktive Anzahl anzeigt. 

#### Aufgabe 3: Ausführen der Kusto-Abfrage für Benutzeraktivitäten

1. Navigieren Sie in **Microsoft Sentinel** unter der Menüüberschrift **Allgemein** zu **Protokolle**.

1. Schließen Sie bei Bedarf das Fenster **Willkommen bei Log Analytics!**.

1. Es wird ein Fenster mit Beispielabfragen geöffnet. Wählen Sie **Audit** aus, und scrollen Sie zu **Benutzer-IDs**.

1. Wählen Sie **Ausführen** aus. 

1. Dadurch wird eine Liste der Benutzer-IDs in Azure AD bereitgestellt.  Da wir den Arbeitsbereich gerade erst erstellt haben, werden möglicherweise keine Ergebnisse angezeigt.  Beachten Sie das Format der Abfrage.

1. Wählen Sie unter **Bedrohungsmanagement** im Menü **Hunting** aus. 

1. Scrollen Sie nach unten, und suchen Sie die Abfrage **Anomalous sign-in location by user account and authenticating application**.  Diese Abfrage für die Azure Active Directory-Anmeldung berücksichtigt alle Benutzeranmeldungen für jede Azure Active Directory-Anwendung und wählt die anomalste Änderung des Standortprofils für einen Benutzer innerhalb einer einzelnen Anwendung aus. Die Absicht besteht darin, nach einer Kompromittierung des Benutzerkontos zu suchen, möglicherweise über einen bestimmten Anwendungsvektor. 

1. Wählen Sie **Ausführen** aus, um die Abfrage auszuführen.

1. Dies liefert möglicherweise keine Ergebnisse mit dem neuen Arbeitsbereich, aber Sie haben jetzt gesehen, wie Abfragen ausgeführt werden können, um Informationen zu sammeln oder potenzielle Bedrohungen zu suchen.
