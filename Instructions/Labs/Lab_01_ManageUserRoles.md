---
lab:
  title: "01\_– Verwalten von Benutzerrollen"
  learning path: '01'
  module: Module 01 - Implement an Identity Management Solution
---

# WWL-Mandanten – Nutzungsbedingungen
Wenn Ihnen im Rahmen einer Präsenzschulung ein Mandant zugewiesen worden ist, steht dieser für Praxislabs innerhalb der Präsenzschulung zur Verfügung. Mandanten sollten nicht für Zwecke außerhalb von Praxislabs freigegeben oder verwendet werden. Der in diesem Kurs verwendete Mandant ist ein Testmandant; er kann nach Abschluss des Kurses nicht verwendet oder erreicht werden und ist nicht für Erweiterungen geeignet. Mandanten dürfen nicht in ein kostenpflichtiges Abonnement konvertiert werden. Die im Rahmen dieses Kurses erworbenen Mandanten verbleiben im Eigentum der Microsoft Corporation, und wir behalten uns das Recht vor, jederzeit auf Mandanten zuzugreifen und diese zurückzuziehen. 



# Lab 01: Verwalten von Benutzerrollen

## Labszenario

Ihr Unternehmen hat kürzlich einen neuen Mitarbeiter eingestellt, der Aufgaben als Anwendungsadministrator übernimmt. Sie müssen einen neuen Benutzer erstellen und die entsprechende Rolle zuweisen.

#### Geschätzte Dauer: 30 Minuten

### Übung 1 – Erstellen eines neuen Benutzers und Testen der Anwendungsadministratorrechte

#### Aufgabe 1 – Hinzufügen eines neuen Benutzers

1. Melden Sie sich bei [https://portal.azure.com](https://portal.azure.com) als globaler Administrator an.

2. Suchen Sie nach **Azure Active Directory**, und wählen Sie diese Option aus.

3. Wählen Sie im linken Navigationsmenü unter **Verwalten** die Option **Benutzer**, dann **+ Neuer Benutzer** und **Neuen Benutzer erstellen** aus.

4. Wählen Sie die Schaltfläche **Benutzer erstellen** aus. Erstellen Sie einen Benutzer mit den folgenden Informationen:

    | **Einstellung**| **Wert**|
    | :--- | :--- |
    | Benutzername| ChrisG|
    | Name| Chris Green|
    | Vorname| Chris|
    | Nachname| Grün|

5. Aktivieren Sie die Option **Kennwort automatisch generieren**.

6. Kopieren Sie das generierte Kennwort an einen Speicherort, damit Sie es für die nächste Aufgabe verwenden können.

     *Sie müssen das Kennwort bei der ersten Anmeldung bei diesem Konto ändern.*

7. Wählen Sie **Erstellen** aus. Der Benutzer wird nun in Ihrer Organisation erstellt und registriert.

#### Aufgabe 2 – Anmelden und Versuchen, eine App zu erstellen

1. Öffnen Sie ein neues InPrivate-Browserfenster.
2. Öffnen Sie das Azure-Portal [https://portal.azure.com](https://portal.azure.com) als Chris Green.

    | **Einstellung**| **Wert**|
    | :--- | :--- |
    | Benutzername| ChrisG@`your domain name.com`|
    | Kennwort| Geben Sie das automatisch generierte Kennwort aus der vorherigen Aufgabe ein. |

3. Aktualisieren Sie Ihr Kennwort.

    | **Einstellung**| **Wert**|
    | :--- | :--- |
    | Aktuelles Kennwort| Verwenden Sie das automatisch generierte Kennwort.|
    | Neues Kennwort| Geben Sie ein eindeutiges und sicheres Kennwort ein. |
    | Kennwort bestätigen| Geben Sie erneut das eindeutige und sichere Kennwort ein. |

4. Wenn das Tour-Dialogfeld **Willkommen bei Microsoft Azure** angezeigt wird, wählen Sie die Schaltfläche **Vielleicht später** aus.

5. Suchen Sie über Suchdialogfeld oben auf dem Bildschirm nach **Unternehmensanwendungen**, und wählen Sie sie aus.
7. Wählen Sie **+ Neue Anwendung** aus. Beachten Sie, dass **+ Eigene Anwendung erstellen** nicht verfügbar ist.

9. Versuchen Sie, einige der anderen Einstellungen wie **Anwendungsproxy**, **Benutzereinstellungen** und andere auszuwählen, um zu sehen, dass **Chris Green** keine Rechte hat.
10. Wählen Sie in der rechten oberen Ecke den Namen **ChrisG** aus, und melden Sie sich ab.


### Übung 2 – Zuweisen der Anwendungsadministratorrolle und Erstellen einer App

#### Aufgabe 1: Zuweisen einer Rolle zu einem Benutzer

Mithilfe von Azure Active Directory (Azure AD) können Sie Administratoren mit eingeschränkten Rechten bestimmen, um Identitätsaufgaben in Rollen mit weniger privilegierten Rechten zu verwalten. Administratoren können für Zwecke wie das Hinzufügen oder Ändern von Benutzern, das Zuweisen von Administratorrollen, das Zurücksetzen von Benutzerkennwörtern, das Verwalten von Benutzerlizenzen oder das Verwalten von Domänennamen festgelegt werden.

1. Wenn Sie noch nicht unter der globalen Administratorrolle angemeldet sind, öffnen Sie das Azure-Portal, und melden Sie sich an.
2. Navigieren Sie zur Seite „Azure Active Directory“.
3. Wählen Sie im Abschnitt „Verwalten“ des Menüs die Option **Benutzer** aus.
4. Wählen Sie das Konto **Chris Green** aus.
5. Wählen Sie im Menü „Verwalten“ die Option **Zugewiesene Rolle** aus.
6. Wählen Sie Select **+ Zuweisungen hinzufügen** aus und markieren Sie die Rolle `Application administrator`.
7. Wählen Sie **Hinzufügen** aus

    ![Seite „Zugewiesene Rollen“ mit der ausgewählten Rolle](./media/directory-role-select-role.png)

**Hinweis**: Wenn in der Labumgebung Azure AD Premium P2 bereits aktiviert ist, wird Privileged Identity Management (PIM) aktiviert, und Sie müssen **Weiter** auswählen und diesem Benutzer eine permanente Rolle zuweisen.

8. Wählen Sie die Schaltfläche **Zurücksetzen** aus.

**Hinweis: Die neu zugewiesene Rolle „Anwendungsadministrator“ wird auf der Seite „Zugewiesene Rollen“ des Benutzers angezeigt.**

#### Aufgabe 2 – Überprüfen von Anwendungsberechtigungen

1. Öffnen Sie ein neues InPrivate-Browserfenster.
2. Öffnen Sie das Azure-Portal [https://portal.azure.com](https://portal.azure.com) als Chris Green.

    | **Einstellung**| **Wert**|
    | :--- | :--- |
    | Benutzername| ChrisG@`your domain name.com`|
    | Kennwort| Geben Sie den Benutzernamen und das Kennwort ein, den bzw. das Sie zuvor erstellt haben. |

3. Wenn das Tour-Dialogfeld **Willkommen bei Microsoft Azure** angezeigt wird, wählen Sie die Schaltfläche **Vielleicht später** aus.
4. Suchen Sie über Suchdialogfeld oben auf dem Bildschirm nach **Unternehmensanwendungen**, und wählen Sie sie aus.
5. Beachten Sie, dass **+ Neue Anwendung** jetzt verfügbar ist.
6. Wählen Sie **+ Neue Anwendung** aus.

   **Hinweis: Diese Rolle verfügt jetzt über die Möglichkeit, dem Mandanten Anwendungen hinzuzufügen. Wir werden in späteren Labs mehr mit diesem Feature experimentieren.**

7. Melden Sie sich bei der Chris Green-Instanz des Azure-Portals ab, und schließen Sie den Browser.

### Übung 3: Entfernen einer Rollenzuweisung

#### Aufgabe 1: Entfernen des Anwendungsadministrators von Chris Green

In dieser Aufgabe wird eine alternative Methode verwendet, um die zugewiesene Rolle zu entfernen, und zwar die Option **Rollen und Administratoren** in Azure AD.

1. Wenn Sie noch nicht als globaler Administrator angemeldet sind, öffnen Sie das Azure-Portal und melden sich jetzt an.
2. Geben Sie im Filtersuchfeld **Azure Active Directory** ein, und starten Sie Azure AD.
3. Wählen Sie in  **Azure Active Directory** die Option  **Rollen und Administratoren** und dann die Rolle **Anwendungsadministrator** in der Liste aus.

**Hinweis**: Wenn in der Labumgebung Azure AD Premium P2 bereits aktiviert ist, wird Privileged Identity Management (PIM) aktiviert, und Sie müssen **Weiter** auswählen und diesem Benutzer eine permanente Rolle zuweisen.

4. Auf der Seiten **Anwendungsadministrator | Zuweisungen** sollte der Name von Chris Green aufgelistet sein.
5. Setzen Sie ein Häkchen in das Kästchen neben Chris Green.
6. Wählen Sie **X Zuweisungen entfernen** in den Optionen am oberen Rand des Dialogfelds aus.
7. Antworten Sie mit **Ja**, wenn das Bestätigungsfeld geöffnet wird.
8. Schließen Sie Azure Active Directory.

### Übung 4: Massenimport von Benutzern

#### Aufgabe 1: Massenvorgänge zum Erstellen von Benutzern mit einer CSV-Datei

1. Wählen Sie im Azure AD-Menü **Benutzer** unter **Verwalten** aus.

2. Wählen Sie auf der Kachel **Benutzer | Alle Benutzer** den Dropdownpfeil **Massenvorgänge** aus, und wählen Sie **Massenerstellung** aus.

3. Durch die Auswahl von **Massenerstellung** wird eine neue Kachel geöffnet. Diese Kachel enthält einen **Downloadlink** zu einer Vorlagendatei, die Sie bearbeiten werden, um ihre Benutzerinformationen aufzufüllen und hochzuladen und die Massenerstellung von Benutzern hinzuzufügen.

4. Wählen Sie **Download** aus, um die CSV-Datei herunterzuladen.

5. Die CSV-Vorlage enthält die Felder, die im Benutzerprofil enthalten sind. Dazu gehören die erforderlichen Felder „Benutzername“, „Anzeigename“ und „Anfängliches Kennwort“. Sie können auch optionale Felder, wie „Abteilung“ und „Nutzungsspeicherort“, zu diesem Zeitpunkt ausfüllen. Der folgende Screenshot ist ein Beispiel dafür, wie Sie die CSV-Datei ausfüllen können: 

    ![Massenimport mithilfe des CSV-Dateieintrags](./media/bulkimportexample.png)

    Sie können diese Datei ändern, um Benutzer massenweise hinzuzufügen.  Beachten Sie, dass Sie nicht alle Felder ausfüllen müssen.  Gemäß den bereitgestellten Beispieldaten müssen Sie hauptsächlich den Namen und Benutzernameninformationen hinzufügen.

6. Eine CSV-Beispieldatei ist im Ordner „Allfiles/Lab1“ bereitgestellt: **SC300BulkUser.csv**.
   1. Öffnen Sie den Editor.
     - Wählen Sie in der Labumgebung die Schaltfläche START aus, und geben Sie „Editor“ ein.  
   1. Öffnen Sie die Datei SC300BulkUser.csv.
   1. Ändern Sie **Geben Sie Ihren Domänennamen ein** in die Domäne Ihrer Azure-Labumgebung.
   1. Speichern Sie die Datei.

7. Wählen Sie im Dialogfeld **Benutzer für Massenerstellung** das Symbol „Dateiordner“ in Schritt 3 aus.

8. Pfad zum Ordner „Allfiles/Lab1“, und wählen Sie **SC300BulkUser.csv** aus.

9. Wählen Sie **Öffnen** aus.

7. Sie werden benachrichtigt, dass die Datei erfolgreich hochgeladen wurde.  Wählen Sie **Submit** aus, um die Benutzer hinzuzufügen. 

Nachdem die Benutzer erstellt wurden, werden Sie darüber benachrichtigt, dass die Erstellung erfolgreich war.  Schließen Sie die Kachel „Benutzer für Massenerstellung“, und die neuen Benutzer werden in die Liste der **Benutzer | Alle Benutzer** übernommen. 

#### Aufgabe 2: Massenhinzufügen von Benutzern mit PowerShell

1. Starten Sie PowerShell als Administrator.  Dazu können Sie in Windows nach PowerShell suchen und „Als Administrator ausführen“ auswählen. 

**Hinweis**: Wählen Sie PowerShell und nicht PowerShell ISE aus.

2. Sie müssen das Azure AD PowerShell-Modul hinzufügen und importieren, wenn Sie es noch nicht verwendet haben.  Führen Sie die beiden folgenden Befehl aus, und bestätigen Sie den Vorgang mit „J“, wenn Sie dazu aufgefordert werden:

    ```
    Install-Module AzureAD
    Import-Module AzureAD
    ```

3. Vergewissern Sie sich, dass das Modul ordnungsgemäß installiert ist, indem Sie den folgenden Befehl ausführen:  

    ```
    Get-Module AzureAD 
    ```

4. Als Nächstes müssen Sie sich bei Azure anmelden, indem Sie Folgendes ausführen:  

    ```
    Connect-AzureAD 
    ``` 

5. Das Microsoft-Anmeldefenster wird angezeigt, in dem Sie sich bei Azure AD anmelden können.  

6. Um zu überprüfen, ob Sie verbunden sind und vorhandene Benutzer anzeigen können, führen Sie Folgendes aus:  

    ``` 
    Get-AzureADUser 
    ```
    
7. Um allen neuen Benutzern ein gemeinsames temporäres Kennwort zuzuweisen, führen Sie den folgenden Befehl aus, und ersetzen Sie „TempPW“ durch das Kennwort, das Sie Ihren Benutzern zur Verfügung stellen möchten.  

    ``` 
    $PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
    ```

    ```
    $PasswordProfile.Password = "<<enter a secure password you will remember>>" 
    ```

8. Sie sind bereit, neue Benutzer zu erstellen.  Der folgende Befehl wird mit den Benutzerinformationen ausgefüllt und ausgeführt.  Wenn Sie mehrere Benutzer hinzufügen möchten, können Sie eine Editor-TXT-Datei verwenden, um die Benutzerinformationen hinzuzufügen und sie in PowerShell zu kopieren/einzufügen. 

    ```
    New-AzureADUser -DisplayName "New User" -PasswordProfile $PasswordProfile -UserPrincipalName "NewUser@labtenantname.com" -AccountEnabled $true -MailNickName "Newuser"
    ```
**Hinweis**: Ersetzen Sie **labtenantname.com** durch den Namen **onmicrosoft.com**, der vom Labmandanten zugewiesenen wurde.

## Experimentieren mit der Verwaltung von Benutzern

Sie können Benutzer auf der Seite „Azure AD“ hinzufügen und entfernen.  Benutzer können jedoch mithilfe der Skripterstellung erstellt werden, und Rollen können zugewiesen werden.  Experimentieren Sie damit, dem Chris Green-Benutzerkonto mithilfe eines Skripts eine andere Rolle zuzuweisen. 
 

### Übung 5: Entfernen eines Benutzers aus Azure Active Directory

#### Aufgabe 1: Entfernen eines Benutzers

Es kann vorkommen, dass ein Konto gelöscht und dann wiederhergestellt werden muss. Sie müssen überprüfen, ob Sie ein Konto wiederherstellen können, das kürzlich gelöscht wurde.

1. Navigieren Sie zu [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview).

2. Wählen Sie im linken Navigationsbereich unter **Verwalten** die Option **Benutzer** aus.

3. Aktivieren Sie in der Liste **Benutzer** das Kontrollkästchen für einen Benutzer, der gelöscht werden soll. Wählen Sie beispielsweise **Chris Green** aus.

    **Tipp**: Durch Auswahl von Benutzern in der Liste können Sie mehrere Benutzer gleichzeitig verwalten. Wenn Sie den Benutzer auswählen, um die Seite des jeweiligen Benutzers zu öffnen, werden nur die Einstellungen dieses einzelnen Benutzers verwaltet.

    ![Screenshot mit der Liste „Alle Benutzer“ mit einem aktivierten Benutzerkontrollkästchen und einem weiteren hervorgehobenen Kontrollkästchen, um zu zeigen, dass mehrere Benutzer in der Liste ausgewählt werden können.](./media/lp1-mod2-remove-user.png)

4. Wählen Sie das Benutzerkonto aus, und wählen Sie im Menü **Löschen** aus.

5. Überprüfen Sie das Dialogfeld, und wählen Sie dann **Ja** aus.

#### Aufgabe 2: Wiederherstellen eines gelöschten Benutzers

1. Wählen Sie auf der Seite „Benutzer“ im linken Navigationsbereich **Gelöschte Benutzer** aus.

2. Überprüfen Sie die Liste der gelöschten Benutzer, und wählen Sie **Chris Green** aus.

    **Wichtig**: Standardmäßig werden gelöschte Benutzerkonten automatisch nach 30 Tagen dauerhaft aus Azure Active Directory entfernt.

3. Wählen Sie im Menü die Option **Benutzer wiederherstellen** aus.

4. Überprüfen Sie das Dialogfeld, und wählen Sie dann **OK** aus.

5. Wählen Sie im linken Navigationsbereich **Alle Benutzer** aus.

6. Vergewissern Sie sich, dass der Benutzer wiederhergestellt wurde.


### Übung 6: Hinzufügen einer Windows 10-Lizenz zu einem Benutzerkonto

#### Aufgabe 1: Suchen Ihres nicht lizenzierten Benutzers in Azure Active Directory

Einigen Benutzerkonten in Ihrer Organisation werden nicht alle verfügbaren Produkte in ihrer zugewiesenen Lizenz bereitgestellt, oder sie benötigen Updates oder Ergänzungen zu ihrer Lizenzzuweisung. Sie müssen sicherstellen, dass Sie die Lizenzzuweisung eines Benutzerkontos in Azure AD aktualisieren können.

1. Navigieren Sie zu [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview).

2. Wählen Sie im linken Navigationsbereich unter **Verwalten** die Option **Benutzer** aus.

3. Geben Sie auf der Seite „Benutzer“ **Raul** in das Suchfeld ein.

4. Wählen Sie **Raul Razo** aus.

5. Überprüfen Sie Rauls Profil, und stellen Sie sicher, dass für ihn ein „Nutzungsspeicherort“ festgelegt ist.

    **Warnung**: Damit einem Benutzer eine Lizenz zugewiesen werden kann, muss dem Benutzer ein Nutzungsspeicherort zugewiesen werden.

6. Wählen Sie den Menüeintrag **Lizenzen** im linken Menü aus.

7. Stellen Sie sicher, dass für Raul „Keine Lizenzzuweisungen gefunden“ angezeigt wird.

8. Navigieren Sie zu [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview]( https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview).

9. Wählen Sie im linken Navigationsbereich unter **Verwalten** die Option **Benutzer** aus.

10. Wählen Sie auf der Seite „Benutzer“ **Raul Razo** aus.

11. Wählen Sie im linken Navigationsbereich **Lizenzen** aus.

12. Wählen Sie die Schaltfläche **+ Zuweisungen** aus. 

13. Aktivieren Sie auf der Seite „Lizenzzuweisungen aktualisieren“ das Kontrollkästchen für eine **Windows 10/11 Enterprise E3**-Lizenz.

    ![Screenshot der Seite „Lizenzzuweisungen aktualisieren“ mit hervorgehobenen Lizenzoptionen](./media/lp1-mod2-assign-user-license-options.png)

14. Wählen Sie zum Abschluss **Speichern** aus.

15. Wählen Sie oben auf dem Bildschirm **Startseite**, dann **Contoso**, dann **Benutzer** und schließlich **Raul Razo** aus.

16. Beachten Sie, dass dem Benutzer wurde keine Lizenz zugewiesen wurde.
