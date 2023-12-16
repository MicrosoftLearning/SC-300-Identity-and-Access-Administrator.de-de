---
lab:
  title: 01 – Verwalten von Benutzerrollen
  learning path: '01'
  module: Module 01 - Implement an Identity Management Solution
---

# WWL-Mandanten – Nutzungsbedingungen
Wenn Ihnen im Rahmen einer Präsenzschulung ein Mandant zugewiesen worden ist, steht dieser für Praxislabs innerhalb der Präsenzschulung zur Verfügung. Mandanten sollten nicht für Zwecke außerhalb von Praxislabs freigegeben oder verwendet werden. Der in diesem Kurs verwendete Mandant ist ein Testmandant; er kann nach Abschluss des Kurses nicht verwendet oder erreicht werden und ist nicht für Erweiterungen geeignet. Mandanten dürfen nicht in ein kostenpflichtiges Abonnement konvertiert werden. Die im Rahmen dieses Kurses erworbenen Mandanten verbleiben im Eigentum der Microsoft Corporation, und wir behalten uns das Recht vor, jederzeit auf Mandanten zuzugreifen und diese zurückzuziehen. 



# Lab 01: Verwalten von Benutzerrollen

## Labszenario

Ihr Unternehmen hat kürzlich einen neuen Mitarbeiter eingestellt, der Aufgaben als Anwendungsadministrator übernimmt. Sie müssen einen neuen Benutzer erstellen und die entsprechende Rolle zuweisen.

#### Geschätzte Dauer: 30 Minuten

### Übung 1 – Erstellen eines neuen Benutzers und Prüfen seiner Anwendungsadministratorrechte

#### Aufgabe 1 – Hinzufügen eines neuen Benutzers

1. Melden Sie sich bei  [https://entra.microsoft.com](https://entra.microsoft.com) als globaler Administrator an.

2. Wählen Sie im linken Menü **Identität** aus.

3. Wählen Sie im linken Navigationsmenü unter **Benutzer** die Option **Alle Benutzer** und dann **+ Neuer Benutzer** und **Neuen Benutzer erstellen** aus.

4. Wählen Sie die Schaltfläche **Benutzer erstellen** aus. Erstellen Sie anschließend einen Benutzer mit den folgenden Informationen:

    | **Einstellung**| **Wert**|
    | :--- | :--- |
    | Benutzerprinzipalname| ChrisG|
    | Anzeigename| Chris Green|

5. Wählen Sie die Option **Kennwort automatisch generieren** aus.

6. Kopieren Sie das generierte Kennwort an einen Speicherort, an dem Sie es für die nächste Aufgabe speichern können.

     *Sie müssen das Kennwort bei der ersten Anmeldung bei diesem Konto ändern.*

7. Klicken Sie auf **Überprüfen + erstellen**. Wählen Sie dann **Erstellen** auf dem Überprüfungsbildschirm aus. Der Benutzer wird nun in Ihrer Organisation erstellt und registriert.

#### Aufgabe 2 – Anmelden und Erstellen einer App

1. Starten Sie ein neues InPrivate-Browserfenster.
2. Öffnen Sie das Microsoft Entra Admin Center [https://entra.microsoft.com](https://entra.microsoft.com) als Chris Green.

    | **Einstellung**| **Wert**|
    | :--- | :--- |
    | Benutzername| ChrisG@`your domain name.com`|
    | Kennwort| Geben Sie das automatisch generierte Kennwort aus der vorherigen Aufgabe ein. |

3. Aktualisieren Sie Ihr Kennwort.

    | **Einstellung**| **Wert**|
    | :--- | :--- |
    | Current Password| Verwenden Sie das automatisch generierte Kennwort|
    | Neues Kennwort| Geben Sie ein eindeutiges und sicheres Kennwort ein |
    | Kennwort bestätigen| Geben Sie das eindeutige und sichere Kennwort erneut ein |

4. Wenn ein **Tour-Dialogfeld** angezeigt wird, wählen Sie die Schaltfläche **Vielleicht später** aus.

5. Suchen Sie im Suchdialogfeld oben auf dem Bildschirm nach ** Unternehmensanwendungen**, und wählen Sie diese Option aus.
7. Wählen Sie **+ Neue Anwendung** aus. Beachten Sie, dass **+ Eigene Anwendung erstellen** nicht verfügbar ist.

9. Versuchen Sie, einige der anderen Einstellungen wie **Anwendungsproxy**, **Benutzereinstellungen** und andere auszuwählen, um zu überprüfen, dass **Chris Green** keine Rechte hat.
10. Wählen Sie in der oberen rechten Ecke den Namen **ChrisG** aus, und melden Sie sich ab.


### Übung 2 – Zuweisen der Anwendungsadministratorrolle und Erstellen einer App

#### Aufgabe 1: Zuweisen einer Rolle zu einem Benutzer

Mit Microsoft Entra ID können Sie eingeschränkte Administrator*innen festlegen, um Identitätsaufgaben in weniger privilegierten Rollen zu verwalten. Administratoren können für Zwecke wie das Hinzufügen oder Ändern von Benutzern, das Zuweisen von Administratorrollen, das Zurücksetzen von Benutzerkennwörtern, das Verwalten von Benutzerlizenzen oder das Verwalten von Domänennamen festgelegt werden.

1. Wenn Sie noch nicht mit der globalen Administratorrolle angemeldet sind, öffnen Sie das Microsoft Entra Admin Center, und melden Sie sich an.
2. Navigieren Sie zu „Identität“, und wählen Sie dann die Seite „Benutzer“ aus.
3. Wählen Sie im Abschnitt „Verwalten“ des Menüs die Option **Alle Benutzer** aus.
4. Wählen Sie das Konto **Chris Green** aus.
5. Wählen Sie im Menü „Verwalten“ die Option **Zugewiesene Rollen** aus.
6. Wählen Sie **+ Zuweisungen hinzufügen** aus, und markieren Sie die Rolle `Application administrator`.
7. Wählen Sie **Hinzufügen** aus

    ![Seite „Zugewiesene Rollen“ mit der ausgewählten Rolle](./media/directory-role-select-role.png)

**Hinweis**: Wenn die Lab-Umgebung Microsoft Entra ID Premium P2 bereits aktiviert hat, wird Privileged Identity Management (PIM) aktiviert, und Sie müssen **Weiter** auswählen und diesem Benutzer eine permanente Rolle zuweisen.

9. Wählen Sie die Schaltfläche **Aktualisieren** aus.

**Hinweis: Die neu zugewiesene Rolle „Anwendungsadministrator“ wird auf der Seite „Zugewiesene Rollen“ des Benutzers angezeigt.**

#### Aufgabe 2 – Überprüfen der Anwendungsberechtigungen

1. Starten Sie ein neues InPrivate-Browserfenster.
2. Öffnen Sie das Microsoft Entra Admin Center [https://entra.microsoftcom](https://entra.microsoft.com) als Chris Green.

    | **Einstellung**| **Wert**|
    | :--- | :--- |
    | Benutzername| ChrisG@`your domain name.com`|
    | Kennwort| Geben Sie das zuvor erstellte eindeutige und sichere Kennwort ein |

3. Wenn das Tour-Dialogfeld **Willkommen bei Microsoft Azure** angezeigt wird, wählen Sie die Schaltfläche **Vielleicht später** aus.
4. Suchen Sie im Suchdialogfeld oben auf dem Bildschirm nach ** Unternehmensanwendungen**, und wählen Sie diese Option aus.
5. Beachten Sie, dass **+ Neue Anwendung** jetzt verfügbar ist.
6. Wählen Sie **+ Neue Anwendung** aus.
7. Die Ansicht **„**+ Eigene Anwendung erstellen**“ ist nicht ausgegraut. Wenn Sie eine Katalog-App auswählen, ist die Schaltfläche **Erstellen** verfügbar.

   **Hinweis: Diese Rolle kann jetzt dem Mandanten Anwendungen hinzuzufügen. Wir werden in späteren Labs mehr mit diesem Feature experimentieren.**

7. Melden Sie sich von der Chris Green-Instanz des Azure-Portals ab, und schließen Sie den Browser.

### Übung 3 – Entfernen einer Rollenzuweisung

#### Aufgabe 1 – Entfernen des Anwendungsadministrators von Chris Green

Diese Aufgabe verwendet eine alternative Methode, um die zugewiesene Rolle zu entfernen, nämlich die Option **Rollen und Administratoren** in Azure AD.

1. Wenn Sie noch nicht als globaler Administrator angemeldet sind, starten Sie das Microsoft Entra Admin Center, und melden Sie sich jetzt an.
2. Geben Sie im Suchfeld **Rollen und** ein, und starten Sie dann Microsoft Entra ID-Rollen und -Verwaltung.
3. Wählen Sie in  **Alle Rollen** von  **Rollen und Administratoren** die Rolle **Anwendungsadministrator** aus der Liste aus.
4. Auf der Seite **Anwendungsadministrator | Zuweisungen** sollte der Name von Chris Green aufgelistet sein.
5. Aktivieren Sie das Kontrollkästchen neben Chris Green.
6. Wählen Sie **X Zuweisungen entfernen** in den Optionen oben im Dialogfeld aus.
7. Antworten Sie mit **Ja**, wenn das Bestätigungsfeld geöffnet wird.
8. Schließen Sie den Bildschirm.

### Übung 4 – Massenimport von Benutzern

#### Aufgabe 1: Massenvorgänge zum Erstellen von Benutzern mit einer CSV-Datei

1. Öffnen Sie im Menü „Microsoft Entra ID“ zuerst **Identität**, und wählen Sie dann **Benutzer** und **Alle Benutzer** aus.

2. Auf der Kachel **Benutzer | Alle Benutzer** wählen Sie den Dropdownpfeil neben **Massenvorgänge** und dann **Massenerstellung** aus.

3. Wenn Sie **Massenerstellung** auswählen, wird eine neue Kachel geöffnet. Diese Kachel enthält einen **Herunterladen**-Link zu einer Vorlagendatei, die Sie bearbeiten, um ihre Benutzerinformationen aufzufüllen und hochzuladen, um die Massenerstellung von Benutzern hinzuzufügen.

4. Wählen Sie **Herunterladen** aus, um die CSV-Datei herunterzuladen.

5. Die CSV-Vorlage enthält die Felder, die im Benutzerprofil enthalten sind. Dazu gehören der erforderliche Benutzername, der Anzeigename und das anfängliche Kennwort. Zu diesem Zeitpunkt können Sie auch optionale Felder, wie Abteilung und Nutzungsspeicherort, ausfüllen. Der folgende Screenshot ist ein Beispiel, wie Sie die CSV-Datei abschließen können: 

    ![Massenimport mithilfe des CSV-Dateieintrags](./media/bulkimportexample.png)

    Sie können diese Datei ändern, um Benutzer in einem Massenvorgang hinzuzufügen.  Beachten Sie, dass Sie nicht alle Felder ausfüllen müssen.  Gemäß den bereitgestellten Beispieldaten müssen Sie hauptsächlich den Namen und den Benutzernamen hinzufügen.

6. Eine CSV-Beispieldatei wurde im Ordner Allfiles/Lab1 – **SC300BulkUser.csv** bereitgestellt.
   1. Öffnen Sie Notepad.
     - Wählen Sie in der Lab-Umgebung die Schaltfläche START aus, und geben Sie „Editor“ ein.  
   1. Öffnen Sie die Datei „SC300BulkUser.csv“.
   1. Ändern Sie das Feld **Domänennamen eingeben** in die Domäne Ihrer Azure-Lab-Umgebung ein.
   1. Speichern Sie die Datei .

7. Wählen Sie im Dialogfeld **Massenerstellung von Benutzern** das Symbol „Dateiordner“ in Schritt 3 aus.

8. Gehen Sie zum Ordner „Allfiles/Lab1“, und wählen Sie die Datei **SC300BulkUser.csv** aus.

9. Klicken Sie auf **Öffnen**.

7. Sie werden benachrichtigt, dass die Datei erfolgreich hochgeladen wurde. Wählen Sie **Absenden** aus, um die Benutzer hinzuzufügen. 

Nachdem die Benutzer erstellt wurden, erhalten Sie eine Meldung, dass die Erstellung erfolgreich war.  Schließen Sie die Kachel „Massenerstellung von Benutzern“, und die neuen Benutzer werden in der Liste der **Benutzer | Alle Benutzer** aufgefüllt. 

#### Aufgabe 2 – Massenerstellung von Benutzern mithilfe von PowerShell

1. Starten Sie PowerShell als Administrator. Dazu können Sie in Windows nach PowerShell suchen und „Als Administrator ausführen“ auswählen. 

**Hinweis**: Sie müssen PowerShell Version 7.2 oder höher verwenden, damit dieses Lab funktioniert.  Wenn PowerShell geöffnet wird, wird oben auf dem Bildschirm die Version angezeigt. Wenn Sie eine ältere Version verwenden, befolgen Sie die angezeigten Anweisungen, um zu https://aka.ms/PowerShell-Release?tag=7.3.9 zu wechseln. Scrollen Sie nach unten zum Abschnitt „Assets“, und wählen Sie „powershell-7.3.1-win-x64.msi“ aus. Wenn der Download abgeschlossen ist, wählen Sie „Datei öffnen“ aus. Installieren Sie unter Verwendung aller Standardwerte.

2. Sie müssen das Microsoft.Graph PowerShell-Modul installieren, wenn Sie es noch nicht verwendet haben.  Führen Sie die folgenden beiden Befehle aus, und drücken Sie „Y“, wenn Sie aufgefordert werden zu bestätigen:

    ```
    Install-Module Microsoft.Graph
    ```
3. Vergewissern Sie sich, dass das Microsoft.Graph-Modul installiert ist:

    ```
    Get-InstalledModule Microsoft.Graph
    ```
    

4. Als Nächstes müssen Sie sich bei Azure anmelden, indem Sie Folgendes ausführen:  

    ```
    Connect-MgGraph -Scopes "User.ReadWrite.All"
    ``` 
    Der Edge-Browser wird geöffnet, und Sie werden aufgefordert, sich anzumelden.  Verwenden Sie das MOD-Administratorkonto, um eine Verbindung herzustellen.  Akzeptieren Sie die Berechtigungsanforderung; schließen Sie dann das Browserfenster.

5. Um zu überprüfen, ob Sie verbunden sind, und um vorhandene Benutzer anzuzeigen, führen Sie Folgendes aus:  

    ``` 
    Get-MgUser 
    ```
    
7. Um allen neuen Benutzern ein gemeinsames temporäres Kennwort zuzuweisen, führen Sie den folgenden Befehl aus, und ersetzen Sie das <Enter a complex Password> Kennwort durch das Kennwort, das Sie Ihren Benutzern zur Verfügung stellen möchten.  

    ``` 
    $PWProfile = @{
        Password = "<Enter a complex password you will>";
        ForceChangePasswordNextSignIn = $false
    }
    ```

8. Sie sind nun bereit, neue Benutzer zu erstellen.  Der folgende Befehl wird mit den Benutzerinformationen aufgefüllt und ausgeführt.  Wenn Sie mehrere Benutzer hinzufügen möchten, können Sie eine TXT-Datei des Editors verwenden, um die Benutzerinformationen hinzuzufügen und sie in PowerShell zu kopieren/einzufügen. 

    ```
    New-MgUser `
        -DisplayName "New PW User" `
        -GivenName "New" -Surname "User" `
        -MailNickname "newuser" `
        -UsageLocation "USA" `
        -UserPrincipalName "newuser@<labtenantname.com>" `
        -PasswordProfile $PWProfile -AccountEnabled `
        -Department "Research" -JobTitle "Trainer"
    ```
**Hinweis**: Ersetzen Sie **labtenantname.com** durch den **onmicrosoft.com**-Namen, der vom Lab-Mandanten zugewiesen wurde.

## Experimentieren mit der Verwaltung von Benutzern

Sie können Benutzer mit der Microsoft Entra ID-Seite hinzufügen und entfernen.  Mithilfe der Skripterstellung können jedoch Benutzer erstellt sowie Rollen zugewiesen werden.  Experimentieren Sie mit dem Chris Green-Benutzerkonto mit der Verwendung von Skripts. 
 

### Übung 5 – Entfernen eines Benutzerkontos aus Microsoft Entra ID

#### Aufgabe 1 – Entfernen eines Benutzers

Es kann vorkommen, dass ein Konto gelöscht und dann wiederhergestellt werden muss. Sie müssen überprüfen, ob Sie ein Konto wiederherstellen können, das kürzlich gelöscht wurde.

1. Navigieren Sie zu [https://entra.micrososft.com](Microsoft Entra admin center).

2. Wählen Sie im linken Navigationsbereich unter **Identität** die Option **Benutzer** aus.

3. Öffnen Sie die Liste **Alle Benutzer**, und aktivieren Sie das Kontrollkästchen für einen Benutzer, der gelöscht werden soll. Wählen Sie beispielsweise **Chris Green** aus.

    **Tipp**: Durch Auswahl von Benutzern in der Liste können Sie mehrere Benutzer gleichzeitig verwalten. Wenn Sie den Benutzer auswählen, um die Seite des jeweiligen Benutzers zu öffnen, werden nur die Einstellungen dieses einzelnen Benutzers verwaltet.

    ![Screenshot mit der Liste „Alle Benutzer“ mit einem aktivierten Benutzerkontrollkästchen und einem weiteren hervorgehobenen Kontrollkästchen, um zu zeigen, dass mehrere Benutzer in der Liste ausgewählt werden können.](./media/lp1-mod2-remove-user.png)

4. Wählen Sie das Benutzerkonto aus, und klicken Sie im Menü auf **Löschen**.

5. Überprüfen Sie das Dialogfeld, und wählen Sie dann **Ja** aus.

#### Aufgabe 2 – Wiederherstellen eines gelöschten Benutzers

1. Wählen Sie auf der Seite **Alle Benutzer** im linken Navigationsbereich **Gelöschte Benutzer** aus.

2. Überprüfen Sie die Liste der gelöschten Benutzer, und wählen Sie **Chris Green** aus.

    **Wichtig**: Standardmäßig werden gelöschte Benutzerkonten automatisch nach 30 Tagen dauerhaft aus Azure Active Directory entfernt.

3. Wählen Sie im Menü die Option **Benutzer wiederherstellen** aus.

4. Überprüfen Sie das Dialogfeld, und klicken Sie dann auf **OK**.

5. Wählen Sie im linken Navigationsbereich **Alle Benutzer** aus.

6. Vergewissern Sie sich, dass der Benutzer wiederhergestellt wurde.


### Übung 6 – Hinzufügen einer Windows 10-Lizenz zu einem Benutzerkonto

#### Aufgabe 1 – Suchen Ihres nicht lizenzierten Benutzers in Azure Active Directory

Einigen Benutzerkonten in Ihrer Organisation werden nicht alle verfügbaren Produkte in der zugewiesenen Lizenz bereitgestellt oder benötigen Updates oder Ergänzungen zur Lizenzzuweisung. Sie müssen sicherstellen, dass Sie die Lizenzzuweisung eines Benutzerkontos in Azure AD aktualisieren können.

1. Navigieren Sie zu [https://entra.microsoft.com]( https://entra.microsoft.com).

2. Wählen Sie im linken Navigationsbereich unter **Identität** die Option **Benutzer** und dann **Alle Benutzer** aus.

3. Geben Sie auf der Seite „Benutzer“ **Raul** in das Suchfeld ein.

4. Wählen Sie **Raul Razo** aus.

5. Überprüfen Sie Rauls Profil, und stellen Sie sicher, dass ein Nutzungsspeicherort für ihn festgelegt ist.

    **Warnung**: Damit einem Benutzer eine Lizenz zugewiesen werden kann, muss dem Benutzer ein Nutzungsspeicherort zugewiesen werden.

6. Wählen Sie das Menüelement **Lizenzen** im linken Menü aus.

7. Stellen Sie sicher, dass für Raul „Keine Lizenzzuweisungen gefunden“ angezeigt wird.

8. Navigieren Sie zurück zu **Alle Benutzer** im linken Navigationsbereich, und wählen Sie unter **Identität** die Option **Benutzer** aus.

9. Wählen Sie auf der Seite „Benutzer“ **Raul Razo** aus.

10. Wählen Sie im linken Navigationsbereich **Lizenzen** aus.

11. Wählen Sie die Schaltfläche **+ Zuweisungen** aus. 

12. Aktivieren Sie auf der Seite „Lizenzzuweisungen aktualisieren“ das Kontrollkästchen für eine **Windows 10/11 Enterprise E3**-Lizenz.

    ![Screenshot der Seite „Lizenzzuweisungen aktualisieren“ mit hervorgehobenen Lizenzoptionen](./media/lp1-mod2-assign-user-license-options.png)

13. Klicken Sie zum Abschluss auf **Speichern**.

14. Wählen Sie oben auf dem Bildschirm **Start**, den Eintrag **Contoso** aus, und wählen Sie dann **Benutzer** und **Raul Razo** aus.

15. Beachten Sie, dass die Lizenz zugewiesen wurde.
