---
lab:
  title: 'Lab: Azure AD-Authentifizierung für virtuelle Windows- und Linux-Computer'
  learning path: '02'
  module: Module 02 - Implement an Authentication and Access Management Solution
---

# Lab 3.3: Microsoft Entra-Authentifizierung für virtuelle Windows-Computer und virtuelle Linux-Computer

**Hinweis** : Für dieses Lab ist ein Azure Pass erforderlich. Anweisungen finden Sie in Lab 00.

## Labszenario

Das Unternehmen hat beschlossen, dass Azure Active Directory verwendet werden sollte, um sich bei virtuellen Computern für den Remotezugriff anzumelden.  In dieser Übung wird gezeigt, wie dies für virtuelle Windows- und Linux-Computer eingerichtet werden kann.

#### Geschätzte Dauer: 30 Minuten

### Übung 1 – Anmelden bei virtuellen Windows-Computern in Azure mit Azure AD

#### Aufgabe 1 : Erstellen eines virtuellen Windows-Computers mit aktivierter Azure AD-Anmeldung

1. Navigieren Sie zur folgenden URL: [https://portal.azure.com](https://portal.azure.com)

1. Wählen Sie **+ Ressource erstellen**.

1. Geben Sie **Windows Server** auf der Suchleiste „Marketplace durchsuchen“ ein.

1. Wählen Sie im **Feld "Windows 11** Enterprise 22H2" in der Dropdownliste "Softwareplan auswählen" die Option **"Windows 11 Enterprise 22H2** " aus.

1. Sie müssen einen Administratorbenutzernamen und ein Kennwort für den virtuellen Computer erstellen.
   - Verwenden Sie einen Benutzernamen, den Sie sich merken werden, und ein sicheres Kennwort.

1. Aktivieren Sie auf der Registerkarte „Verwaltung" das Kontrollkästchen Anmeldung mit Azure AD im Azure AD-Abschnitt .

    HINWEIS: Seit dem 11.1.2023 wurde diese Benutzeroberfläche nicht aktualisiert, um Die Microsoft Entra-ID anzuzeigen, sie verweist weiterhin auf Azure AD.

    HINWEIS 2: Sie werden feststellen, dass die **vom System zugewiesene verwaltete Identität im Abschnitt "Identität** " automatisch überprüft und grau gedreht wird. Diese Aktion sollte automatisch erfolgen, nachdem Sie die Anmeldung bei Azure AD aktiviert haben.

1. Führen Sie die weiteren Schritte zum Erstellen eines virtuellen Computers aus. 

1. Klicken Sie auf Erstellen.

#### Aufgabe 2 – Azure AD-Anmeldung für vorhandene virtuelle Azure-Computer

1. Navigieren Sie zu virtuellen Computern in der[https://portal.azure.com](https://portal.azure.com) .** **

1. Klicken Sie im Menü auf Virtuelle Maschine erstellen.

1. Wählen Sie die Option **Zugriffssteuerung (IAM)** aus.

1. Wählen Sie „Hinzufügen“ und dann „Rollenzuweisung hinzufügen“ aus, um die Seite „Rollenzuweisung hinzufügen“ zu öffnen.

1. Weisen Sie die folgenden Einstellungen zu:
    - **Zuordnungstyp**: Rollen der Auftragsfunktion
    - **VM-Administratoranmeldung:**
    - Wählen Sie die Option Benutzer, Gruppe oder Dienstprinzipal aus.  Verwenden Sie **dann +Select-Mitglieder**, um Joni Sherman** als bestimmten Benutzer für die VM hinzuzufügen**.

1. Wählen Sie **Überprüfen und Zuweisen** zwei Mal aus, um den Vorgang abzuschließen.

#### Aufgabe 3 – Aktualisieren der Server-VM zur Unterstützung der Azure AD-Anmeldung

1. Wählen Sie das **Menüelement Verbinden** aus.

1. Wählen Sie auf der Registerkarte **RDP****RDP-Datei herunterladen** aus.  Wenn Sie dazu aufgefordert werden, wählen Sie die **Option "Beibehalten"** für die Datei aus.  Sie wird in Ihrem Ordner "Downloads" gespeichert.

1. Öffnen Sie den **Ordner "Downloads** " im Datei-Manager.

1. Öffnen Sie das RDP.

1. Melden Sie sich als alternativer Benutzer an.

1. Verwenden Sie den Benutzernamen und das Kennwort des Administrators, den Sie beim Einrichten des virtuellen Computers erstellen.
   - Wenn Sie dazu aufgefordert werden, sagen Sie "Ja", um den Zugriff auf den virtuellen Computer oder die RDP-Sitzung zuzulassen.

1. Warten Sie, bis der Server geöffnet ist, und alle zu ladenden Software, z. B. das Server-Manager-Dashboard.

1. Wählen Sie die **Schaltfläche "Start"** auf dem virtuellen Computer aus.

1. Geben Sie Systemsteuerung ein **, und starten Sie **die Systemsteuerungs-App.

1. Wählen Sie **"System und Sicherheit** " aus der Liste der Einstellungen aus.

1. Wählen Sie in der **Systemeinstellung** die **Option "Remotezugriff zulassen" aus** .

1. Unten im daraufhin geöffneten Dialogfeld wird ein **Abschnitt "Remotedesktop** " angezeigt.

1. **Deaktivieren Sie** das Kontrollkästchen " **Verbindungen nur von Computern zulassen", auf denen Remotedesktop mit Authentifizierung** auf Netzwerkebene ausgeführt wird.

1. Wählen Sie **Apply** (Übernehmen) und anschließend **OK** aus.

1. RDP-Sitzung mit der VM (virtueller Computer)


#### Aufgabe 4 – Ändern Ihrer RDP-Datei zur Unterstützung der Azure AD-Anmeldung

1. Öffnen Sie den **Ordner "Downloads** " im Datei-Manager.

1. **Erstellen Sie eine Kopie** der RDP-Datei, und fügen Sie "-AzureAD **" am Ende des Dateinamens hinzu**.

1. Bearbeiten Sie die neue Version der RDP-Datei, die Sie soeben mit Editor kopiert haben. Fügen Sie die beiden Textzeilen am Ende der Datei hinzu:
     ```
        enablecredsspsupport:i:0
        authentication level:i:2
     ```
 
 1. Speichern der RDP-Datei  Sie sollten jetzt über zwei Versionen der Datei verfügen:
      - RDP.
      - <<virtual machine name>>-AzureAD.RDP

#### Aufgabe 5 – Verbinden zum Windows Server 2022-Rechenzentrum unter Verwendung der Azure AD-Anmeldung

1. Öffnen Sie das **<<virtual machine name>>-AzureAD.RDP

1. Wählen Sie das Symbol für das **Dialogfeld „Verbindung öffnen“** aus.

1. Anstatt dazu aufgefordert zu werden, mit welchem Benutzerkonto sie sich anmelden soll, sollten Sie eine Meldung erhalten, in der Sie gefragt werden, ob Sie eine Verbindung mit dem Remotecomputer herstellen möchten.

1. Wählen Sie unten auf der Bildschirm **Abbrechen** aus.

1. Die Remotedesktopsitzung sollte geöffnet werden; und zeigen Sie den Windows Server-Anmeldebildschirm an.  **Ein anderer Benutzer** mit einer Schaltfläche "OK" sollte angezeigt werden.

1. Klickan Sie auf **OK**.

1. Geben Sie im Dialogfeld Benutzer die folgenden Informationen ein:
   - Benutzername = **AzureAD\JoniS@<<your lab domainname>>
   - Geben Sie das Administratorkennwort ein, das von Ihrem Lab-Hostinganbieter bereitgestellt wird.

   HINWEIS: JoniS ist der Benutzer, dem wir während der Aufgabe 1 Zugriff auf die Anmeldung als Administrator gewährt haben.

1. Windows Server sollte die Anmeldung bestätigen und das normale Server-Manager Dashboard öffnen.

#### Aufgabe 6 – Optionale Tests zum Erkunden der Azure AD-Anmeldung

1. Überprüfen Sie, ob JoniS der einzige Benutzer war, der der Gruppe "Administratoren" hinzugefügt wurde.

1. Wählen Sie im Server-Manager-Dashboard oben links das **Menü "Extras**" aus.

1. Starten Sie das **Computerverwaltungstool** .

1. Öffnen Sie **lokale Benutzer und Gruppen** , und navigieren Sie dann zu **"Gruppen", "Administratoren"**.

1. Azure\JoniSherman....** sollte in der Liste angezeigt **werden.

1. Überprüfen Sie, ob sich andere Azure AD-Mitglieder anmelden können.

1. Melden Sie sich bei der Remotedesktopsitzung ab.

1. Starten Sie die **<<server name>Datei >-AzureAD.RDP** erneut.

1. Versuchen Sie, sich als andere Azure AD-Mitglieder wie AdeleV oder AlexW oder DiegoS anzumelden.

1. Beachten Sie, dass jedem dieser Benutzer der Zugriff verweigert wird.

### Optionale Übung 2 – Anmelden bei virtuellen Linux-Computern in Azure mit Azure AD

#### Erstellen einer GNU/Linux-VM mit systemseitig zugewiesener verwalteter Identität

1. Navigieren Sie zur folgenden URL: [https://portal.azure.com](https://portal.azure.com)

1. Wählen Sie **+ Ressource erstellen**.

1. Wählen Sie in der Ansicht Beliebt unter Ubuntu Server 18.04 LTS die Option Erstellen aus.

1. und aktivieren Sie das Kontrollkästchen, um die Anmeldung mit Azure Active Directory (Vorschau) zu aktivieren.

1. Stellen Sie sicher, dass die Option **Systemseitig zugewiesene verwaltete Identität** aktiviert ist.

1. Führen Sie die weiteren Schritte zum Erstellen eines virtuellen Computers aus. Während dieser Vorschauphase müssen Sie ein Administratorkonto mit Benutzernamen und Kennwort oder öffentlichem SSH-Schlüssel erstellen.

#### Aufgabe 2 – Azure AD-Anmeldung für vorhandene virtuelle Azure-Computer

1. Navigieren Sie zu virtuellen Computern in der[https://portal.azure.com](https://portal.azure.com) .** **

1. Wählen Sie die Option **Zugriffssteuerung (IAM)** aus.

1. Wählen Sie „Hinzufügen“ und dann „Rollenzuweisung hinzufügen“ aus, um die Seite „Rollenzuweisung hinzufügen“ zu öffnen.

1. Weisen Sie die folgende Rolle zu. 
    - VM-Administratoranmeldung oder VM-Benutzeranmeldung
    - Sie können eine Rolle einem Benutzer, einer Gruppe, einem Dienstprinzipal oder einer verwalteten Identität zuweisen.

1. Ausführliche Informationen finden Sie unter Zuweisen von Azure-Rollen über das Azure-Portal.
