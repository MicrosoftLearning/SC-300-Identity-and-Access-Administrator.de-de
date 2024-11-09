---
lab:
  title: 10 – Microsoft Entra ID-Authentifizierung für virtuelle Windows- und Linux-Computer
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Übung 10: Microsoft Entra-Authentifizierung für virtuelle Windows- und Linux-Computer

**Hinweis**: Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen dazu finden Sie in Lab 00.

## Labszenario

Das Unternehmen hat entschieden, dass Microsoft Entra ID verwendet werden sollte, um sich bei VMs für den Remotezugriff anzumelden.  In dieser Übung wird gezeigt, wie dies für virtuelle Windows- und Linux-Computer eingerichtet werden kann.

#### Geschätzte Dauer: 30 Minuten

### Übung 1 – Anmelden bei virtuellen Windows-Computern in Azure mit Microsoft Entra ID

#### Aufgabe 1 – Erstellen eines virtuellen Windows-Computers mit aktivierter Microsoft Entra ID-Anmeldung

1. Navigieren Sie zu [https://portal.azure.com](https://portal.azure.com)

1. Wählen Sie **+ Ressource erstellen** aus.

1. Geben Sie **Windows 11** in die Suchleiste des Marketplace ein und drücken Sie dann die **Eingabetaste**.

1. Wählen Sie im Feld **Windows 11** die Option **Erstellen v** und wählen Sie **Windows 11 Enterprise, Version 22H2** aus dem sich öffnenden Menü.

1. Erstellen Sie die VM unter Verwendung der folgenden Werte auf der Registerkarte **Grundlagen**:
  | Feld | Zu verwendender Wert |
  | :-- | :-- |
  | Abonnement | Azure Pass-Förderung |
  | Ressourcengruppe | Neu erstellen – rgEntraLogin |
  | Name des virtuellen Computers | vmEntraLogin |
  | Region | *default* |
  | Verfügbarkeitsoptionen | Keine Infrastrukturredundanz erforderlich |
  | Sicherheitstyp | Standard |
  | Größe | Standard DC1s_v3 – 1 vCPU, 8 GiB Arbeitsspeicher |
  | Benutzername des Administrators | vmEntraAdmin |
  | Administratorkennwort | Verwenden Sie das von der Laborumgebung bereitgestellte Kennwort oder erstellen Sie ein sicheres Kennwort, das Sie sich merken können. |
  | Lizenzierung | Bestätigen, dass Sie über eine Lizenz verfügen |

1. Auf den Registerkarten **Datenträger** oder **Netzwerke** brauchen Sie nichts zu ändern, aber Sie können die Werte überprüfen.

1. Wechseln Sie zur Registerkarte **Verwaltung** und aktivieren Sie im Abschnitt „Microsoft Entra ID“ das Kontrollkästchen **Mit Microsoft Entra ID anmelden**.

        NOTE: You will notice that the **System assigned managed identity** under the Identity section is automatically checked and turned grey. This action should happen automatically once you enable Login with Microsoft Entra ID.

1. Klicken Sie auf **Bewerten + erstellen**.

1. Wählen Sie **Erstellen**aus.

#### Aufgabe 2 – Microsoft Entra ID-Anmeldung für vorhandene Microsoft Azure Virtual Machines

1. Navigieren Sie zu **Virtuelle Computer** in [https://portal.azure.com](https://portal.azure.com).

1. Wählen Sie den in Aufgabe 1 neu erstellten virtuellen Computer aus.

1. Wählen Sie **Zugriffssteuerung (IAM)** aus.

1. Wählen Sie **+ Hinzufügen** und dann **Rollenzuweisung hinzufügen** aus, um die Seite „Rollenzuweisung hinzufügen“ zu öffnen.

1. Weisen Sie die folgenden Einstellungen zu:
    - **Zuweisungstyp**: Rollen der Auftragsfunktion
    - **Rolle**: VM-Administratoranmeldung
    - **Mitglieder**: Wählen Sie „Benutzer, Gruppe oder Dienstprinzipal“ aus.  Verwenden Sie dann **+ Mitglieder auswählen**, um **Joni Sherman** als bestimmten Benutzer für die VM hinzuzufügen.

1. Wählen Sie **Überprüfen und Zuweisen** zwei Mal aus, um den Prozess abzuschließen.

#### Aufgabe 3 – Aktualisieren der Server-VM zur Unterstützung der Microsoft Entra ID-Anmeldung

1. Wählen Sie im Menü **Verbinden** die Option **Verbinden** aus.

1. Wählen Sie auf der Registerkarte **RDP****RDP-Datei herunterladen** aus.  Wenn Sie dazu aufgefordert werden, wählen Sie die **Beibehalten** für die Datei aus.  Die Datei wird in Ihrem Ordner „Downloads“ gespeichert.

1. Öffnen Sie den Ordner **Downloads** im Datei-Manager.

1. Öffnen Sie den RDP.

1. Melden Sie sich als alternativer Benutzer an.

1. Verwenden Sie den Benutzernamen und das Kennwort des Administrators, den Sie beim Einrichten des virtuellen Computers erstellt haben.
   - Wenn Sie dazu aufgefordert werden, wählen Sie „Ja“ aus, um den Zugriff auf den virtuellen Computer oder die RDP-Sitzung zuzulassen.

1. Warten Sie, bis die VM geöffnet und die gesamte Software geladen ist.

1. Wählen Sie die Schaltfläche **Start** im virtuellen Computer aus.

1. Geben Sie **Systemsteuerung** ein, und starten Sie die Systemsteuerungs-App.

1. Wählen Sie **System und Sicherheit** in der Liste der Einstellungen aus.

1. Wählen Sie in der Einstellung **System** die Option **Remotezugriff zulassen** aus.

  HINWEIS: Sie müssen das System-Untermenü nicht öffnen. Die Option ist unter dem Systemheader verfügbar.

1. Im daraufhin geöffneten Dialogfeld wird unten der Abschnitt **Remotedesktop** angezeigt.

1. **Deaktivieren Sie** das Kontrollkästchen **Verbindungen nur von Computern zulassen, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt**.

1. Wählen Sie **Übernehmen** und anschließend **OK** aus.

1. **Beenden** Sie die RDP-Sitzung mit der VM.

#### Aufgabe 4 – Ändern der RDP-Datei zur Unterstützung der Microsoft Entra ID-Anmeldung

1. Öffnen Sie den Ordner **Downloads** im Datei-Manager.

1. **Erstellen Sie eine Kopie** der RDP-Datei und fügen Sie **-EntraID** am Ende des Dateinamens an.

1. Bearbeiten Sie die neue Version der RDP-Datei im Editor, die Sie soeben kopiert haben. Fügen Sie die folgenden beiden Textzeilen am Ende der Datei hinzu:
     ```
        enablecredsspsupport:i:0
        authentication level:i:2
     ```
 
 1. **Speichern** Sie die RDP-Datei.  Sie sollten jetzt über zwei Versionen der Datei verfügen:
      - <<virtual machine name>>.RDP
      - <<virtual machine name>>-EntraID.RDP

#### Aufgabe 5 – Herstellen einer Verbindung mit dem virtuellen Windows-Computer mithilfe der Microsoft Entra ID-Anmeldung

1. Öffnen Sie das **<<virtual machine name>>-EntraID.RDP

1. Wählen Sie das Symbol **Verbinden** aus, wenn das Dialogfeld geöffnet wird.

1. Anstatt dazu aufgefordert zu werden, mit welchem Benutzerkonto Sie sich anmelden sollen, sollten Sie eine Meldung erhalten, in der Sie gefragt werden, ob Sie eine Verbindung mit dem Remotecomputer herstellen möchten.

1. Wählen Sie unten auf der Bildschirm **Ja** aus.

1. Die Remotedesktopsitzung sollte geöffnet werden und den Windows Server-Anmeldebildschirm anzeigen.  **Anderer Benutzer** mit einer OK-Schaltfläche sollte angezeigt werden.

1. Klickan Sie auf **OK**.

1. Geben Sie im Dialogfeld „Anmeldung“ die folgenden Informationen ein:
   - Benutzername = **AzureAD\JoniS@ Ihr Domänenname**
   - Kennwort = Geben Sie das Kennwort ein, das von Ihrem Labanbieter bereitgestellt wird.

   HINWEIS: JoniS ist der Benutzer, dem wir in der Aufgabe 1 Zugriff auf die Anmeldung als Administrator gewährt haben.

1. Windows sollte die Anmeldung bestätigen und den normalen Bildschirm öffnen.

#### Aufgabe 6 – Optionale Tests zum Erkunden der Microsoft Entra ID-Anmeldung

1. Überprüfen Sie, ob JoniS der einzige Benutzer war, der der Gruppe „Administratoren“ hinzugefügt wurde.

1. Klicken Sie mit der sekundären Maustaste auf die Startschaltfläche und wählen Sie dann im Popupmenü **Computerverwaltung** aus.

1. Öffnen Sie **Lokale Benutzer und Gruppen**, und navigieren Sie dann zu **Gruppen, Administratoren**.

1. **Azure\JoniSherman....** sollte in der Liste angezeigt werden.

1. Überprüfen Sie, ob sich andere Microsoft Entra ID-Mitglieder anmelden können.

1. Beenden Sie die Remotedesktopsitzung.

1. Starten Sie die Datei **<<server name>>-EntraID.RDP** erneut.

1. Versuchen Sie, sich mit den Benutzernamen anderer Microsoft Entra-Benutzerkonten wie AdeleV, AlexW oder DiegoS anzumelden.

1. Beachten Sie, dass jedem dieser Benutzer der Zugriff verweigert wird.

### Optionale Übung 2: Anmelden bei virtuellen Linux-Computern in Azure mit Microsoft Entra ID

#### Aufgabe 1: Erstellen einer Linux-VM mit systemseitig zugewiesener verwalteter Identität

1. Navigieren Sie zu [https://portal.azure.com](https://portal.azure.com)

1. Wählen Sie **+ Ressource erstellen** aus.

1. Suchen Sie nach **Ubuntu**.

1. Wählen Sie unter **Ubuntu Server 22.04 LTS** **Erstellen** aus. Sie können andere Linux-Server für diese Testumgebung verwenden.

1. Aktivieren Sie auf der Registerkarte **Verwaltung** das Kontrollkästchen, um **Anmeldung mit Microsoft Entra ID** zu aktivieren.

1. Stellen Sie sicher, dass die Option **Systemseitig zugewiesene verwaltete Identität** aktiviert ist.

1. Führen Sie die weiteren Schritte zum Erstellen eines virtuellen Computers aus. Während dieser Vorschauphase müssen Sie ein Administratorkonto mit Benutzernamen und Kennwort oder öffentlichem SSH-Schlüssel erstellen.

#### Aufgabe 2 – Microsoft Entra ID-Anmeldung für vorhandene Microsoft Azure Virtual Machines

1. Navigieren Sie zu **Virtuelle Computer** in [https://portal.azure.com](https://portal.azure.com).

1. Wählen Sie **Zugriffssteuerung (IAM)** aus.

1. Wählen Sie „Hinzufügen > Rollenzuweisung hinzufügen“ aus, um die Seite „Rollenzuweisung hinzufügen“ zu öffnen.

1. Weisen Sie die folgende Rolle zu. 
    - **Rolle**: VM-Administratoranmeldung oder VM-Benutzeranmeldung
    - **Zugriff zuweisen zu**: Benutzer, Gruppe oder Dienstprinzipal oder verwaltete Identität

1. Ausführliche Informationen finden Sie unter Zuweisen von Azure-Rollen über das Azure-Portal.
