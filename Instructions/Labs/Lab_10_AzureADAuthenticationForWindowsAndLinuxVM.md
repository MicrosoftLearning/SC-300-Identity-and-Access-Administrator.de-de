---
lab:
  title: '10: Azure AD-Authentifizierung für virtuelle Windows- und Linux-Computer'
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Lab 10: Azure AD-Authentifizierung für virtuelle Windows- und Linux-Computer

**Hinweis**: Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen dazu finden Sie in Lab 00.

## Labszenario

Das Unternehmen hat beschlossen, dass Azure Active Directory verwendet werden sollte, um sich bei virtuellen Computern für den Remotezugriff anzumelden.  In dieser Übung wird gezeigt, wie dies für virtuelle Windows- und Linux-Computer eingerichtet werden kann.

#### Geschätzte Dauer: 30 Minuten

### Übung 1: Anmelden bei virtuellen Windows-Computern in Azure mit Azure AD

#### Aufgabe 1: Erstellen eines virtuellen Windows-Computers mit aktivierter Azure AD-Anmeldung

1. Navigieren Sie zu [https://portal.azure.com](https://portal.azure.com)

1. Wählen Sie **+ Ressource erstellen** aus.

1. Geben Sie **Windows Server** in der Suchleiste „Marketplace durchsuchen“ ein.

1. Wählen Sie **Windows Server** aus, und wählen Sie **Windows Server 2022 Datacenter** in der Dropdownliste zur Auswahl einer Software aus.

1. Sie müssen einen Administratorbenutzernamen und ein Kennwort für den virtuellen Computer auf der Registerkarte „Grundeinstellungen“ erstellen.
   - Verwenden Sie einen Benutzernamen, den Sie sich merken können, und ein sicheres Kennwort.

1. Aktivieren Sie auf der Registerkarte **Verwaltung** das Kontrollkästchen „Mit Azure AD anmelden“ im Abschnitt „Azure AD“.

1. Sie werden feststellen, dass die **Systemseitig zugewiesene verwaltete Identität** im Abschnitt „Identität“ automatisch aktiviert und grau angezeigt wird. Diese Aktion sollte automatisch erfolgen, nachdem Sie „Mit Azure AD anmelden“ aktiviert haben.

1. Führen Sie die weiteren Schritte zum Erstellen eines virtuellen Computers aus. 

1. Wählen Sie „Erstellen“ aus.

#### Aufgabe 2: Azure AD-Anmeldung für vorhandene virtuelle Azure-Computer

1. Navigieren Sie zu **Virtuelle Computer** in [https://portal.azure.com](https://portal.azure.com).

1. Wählen Sie den in Aufgabe 1 neu erstellten virtuellen Computer aus.

1. Wählen Sie **Zugriffssteuerung (IAM)** aus.

1. Wählen Sie **+ Hinzufügen** und dann **Rollenzuweisung hinzufügen** aus, um die Seite „Rollenzuweisung hinzufügen“ zu öffnen.

1. Weisen Sie die folgenden Einstellungen zu:
    - **Zuweisungstyp**: Rollen der Auftragsfunktion
    - **Rolle**: VM-Administratoranmeldung
    - **Mitglieder**: Wählen Sie „Benutzer, Gruppe oder Dienstprinzipal“ aus.  Verwenden Sie dann **+ Mitglieder auswählen**, um **Joni Sherman** als bestimmten Benutzer für die VM hinzuzufügen.

1. Wählen Sie **Überprüfen und Zuweisen** zwei Mal aus, um den Prozess abzuschließen.

#### Aufgabe 3: Aktualisieren der Server-VM zur Unterstützung der Azure AD-Anmeldung

1. Wählen Sie den Menüeintrag **Verbinden** aus.

1. Wählen Sie auf der Registerkarte **RDP****RDP-Datei herunterladen** aus.  Wenn Sie dazu aufgefordert werden, wählen Sie die **Beibehalten** für die Datei aus.  Die Datei wird in Ihrem Ordner „Downloads“ gespeichert.

1. Öffnen Sie den Ordner **Downloads** im Datei-Manager.

1. Öffnen Sie den RDP.

1. Melden Sie sich als alternativer Benutzer an.

1. Verwenden Sie den Benutzernamen und das Kennwort des Administrators, den Sie beim Einrichten des virtuellen Computers erstellt haben.
   - Wenn Sie dazu aufgefordert werden, wählen Sie „Ja“ aus, um den Zugriff auf den virtuellen Computer oder die RDP-Sitzung zuzulassen.

1. Warten Sie, bis der Server geöffnet ist, und die gesamte Software, wie etwa das Server-Manager-Dashboard, geladen ist.

1. Wählen Sie die Schaltfläche **Start** im virtuellen Computer aus.

1. Geben Sie **Systemsteuerung** ein, und starten Sie die Systemsteuerungs-App.

1. Wählen Sie **System und Sicherheit** in der Liste der Einstellungen aus.

1. Wählen Sie in der Einstellung **System** die Option **Remotezugriff zulassen** aus.

1. Im daraufhin geöffneten Dialogfeld wird unten der Abschnitt **Remotedesktop** angezeigt.

1. **Deaktivieren Sie** das Kontrollkästchen **Verbindungen nur von Computern zulassen, auf denen Remotedesktop mit Authentifizierung auf Netzwerkebene ausgeführt**.

1. Wählen Sie **Übernehmen** und anschließend **OK** aus.

1. **Beenden** Sie die RDP-Sitzung mit der VM.


#### Aufgabe 4: Ändern Ihrer RDP-Datei zur Unterstützung der Azure AD-Anmeldung

1. Öffnen Sie den Ordner **Downloads** im Datei-Manager.

1. **Erstellen Sie eine Kopie** der RDP-Datei, und fügen Sie **-AzureAD** am Ende des Dateinamens hinzu.

1. Bearbeiten Sie die neue Version der RDP-Datei im Editor, die Sie soeben kopiert haben. Fügen Sie die folgenden beiden Textzeilen am Ende der Datei hinzu:
     ```
        enablecredsspsupport:i:0
        authentication level:i:2
     ```
 
 1. **Speichern** Sie die RDP-Datei.  Sie sollten jetzt über zwei Versionen der Datei verfügen:
      - <<virtual machine name>>.RDP
      - <<virtual machine name>>-AzureAD.RDP

#### Aufgabe 5: Verbinden zum Windows Server 2022-Rechenzentrum mit der Azure AD-Anmeldung

1. Öffnen Sie die **<<virtual machine name>>-AzureAD.RDP

1. Wählen Sie das Symbol **Verbinden** aus, wenn das Dialogfeld geöffnet wird.

1. Anstatt dazu aufgefordert zu werden, mit welchem Benutzerkonto Sie sich anmelden sollen, sollten Sie eine Meldung erhalten, in der Sie gefragt werden, ob Sie eine Verbindung mit dem Remotecomputer herstellen möchten.

1. Wählen Sie unten auf der Bildschirm **Ja** aus.

1. Die Remotedesktopsitzung sollte geöffnet werden und den Windows Server-Anmeldebildschirm anzeigen.  **Anderer Benutzer** mit einer OK-Schaltfläche sollte angezeigt werden.

1. Wählen Sie **OK** aus.

1. Geben Sie im Dialogfeld „Anmeldung“ die folgenden Informationen ein:
   - Benutzername = **AzureAD\JoniS@<<your lab domainname>>
   - Kennwort = Geben Sie das Kennwort ein, das von Ihrem Labanbieter bereitgestellt wird.

   HINWEIS: JoniS ist der Benutzer, dem wir in der Aufgabe 1 Zugriff auf die Anmeldung als Administrator gewährt haben.

1. Windows Server sollte die Anmeldung bestätigen und das normale Server-Manager-Dashboard öffnen.

#### Aufgabe 6: Optionale Tests zum Erkunden der Azure AD-Anmeldung

1. Überprüfen Sie, ob JoniS der einzige Benutzer war, der der Gruppe „Administratoren“ hinzugefügt wurde.

1. Wählen Sie im Server-Manager-Dashboard links oben das Menü **Tools** aus.

1. Starten Sie das Tool **Computerverwaltung**.

1. Öffnen Sie **Lokale Benutzer und Gruppen**, und navigieren Sie dann zu **Gruppen, Administratoren**.

1. **Azure\JoniSherman....** sollte in der Liste angezeigt werden.

1. Überprüfen Sie, ob sich andere Azure AD-Mitglieder anmelden können.

1. Beenden Sie die Remotedesktopsitzung.

1. Öffnen Sie die Datei **<<server name>>-AzureAD.RDP** erneut.

1. Versuchen Sie, sich als andere Azure AD-Mitglieder wie AdeleV oder AlexW oder DiegoS anzumelden.

1. Beachten Sie, dass jedem dieser Benutzer der Zugriff verweigert wird.

### Optionale Übung 2: Anmelden bei virtuellen Linux-Computern in Azure mit Azure AD

#### Aufgabe 1: Erstellen einer Linux-VM mit systemseitig zugewiesener verwalteter Identität

1. Navigieren Sie zu [https://portal.azure.com](https://portal.azure.com)

1. Wählen Sie **+ Ressource erstellen** aus.

1. Wählen Sie **Erstellen** in der Ansicht „Beliebt“ unter **Ubuntu Server 18.04 LTS** aus.

1. Aktivieren Sie auf der Registerkarte **Verwaltung** das Kontrollkästchen zum Aktivieren von **Mit Azure Active Directory anmelden (Vorschau)**.

1. Stellen Sie sicher, dass die Option **Systemseitig zugewiesene verwaltete Identität** aktiviert ist.

1. Führen Sie die weiteren Schritte zum Erstellen eines virtuellen Computers aus. Während dieser Vorschauphase müssen Sie ein Administratorkonto mit Benutzernamen und Kennwort oder öffentlichem SSH-Schlüssel erstellen.

#### Aufgabe 2: Azure AD-Anmeldung für vorhandene virtuelle Azure-Computer

1. Navigieren Sie zu **Virtuelle Computer** in [https://portal.azure.com](https://portal.azure.com).

1. Wählen Sie **Zugriffssteuerung (IAM)** aus.

1. Wählen Sie „Hinzufügen > Rollenzuweisung hinzufügen“ aus, um die Seite „Rollenzuweisung hinzufügen“ zu öffnen.

1. Weisen Sie die folgende Rolle zu. 
    - **Rolle**: VM-Administratoranmeldung oder VM-Benutzeranmeldung
    - **Zugriff zuweisen zu**: Benutzer, Gruppe oder Dienstprinzipal oder verwaltete Identität

1. Ausführliche Informationen finden Sie unter Zuweisen von Azure-Rollen über das Azure-Portal.
