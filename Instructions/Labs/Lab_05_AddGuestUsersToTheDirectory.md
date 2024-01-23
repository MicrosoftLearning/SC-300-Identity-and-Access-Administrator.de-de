---
lab:
  title: '05: Hinzufügen von Gastbenutzern zum Verzeichnis'
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Lab 05: Hinzufügen von Gastbenutzern zum Verzeichnis

## Labszenario

Ihr Unternehmen arbeitet mit vielen Anbietern zusammen, und gelegentlich müssen Sie Ihrem Verzeichnis einige Lieferantenkonten als Gast hinzufügen.

#### Geschätzte Dauer: 20 Minuten

### Übung 1: Hinzufügen von Gastbenutzern zum Verzeichnis

#### Aufgabe: Hinzufügen des Gastbenutzers

1. Melden Sie sich bei [https://portal.azure.com](https://portal.azure.com) als Benutzer an, dem eine eingeschränkte Azure AD-Administratorrolle oder die Rolle „Gasteinladender“ zugewiesen ist.

2. Wählen Sie  **Azure Active Directory** aus.

3. Wählen Sie unter  **Verwalten** die Option  **Benutzer** aus.

4. Wählen Sie  **+ Neuer Benutzer** aus.

5. Wählen Sie im Menü „Neuer Benutzer“ die Option **Invite external user** aus, und fügen Sie dann die Informationen des Gastbenutzers hinzu.

    **HINWEIS**: Gruppen-E-Mail-Adressen werden nicht unterstützt. Geben Sie die E-Mail-Adresse einer Einzelperson ein. Einige E-Mail-Anbieter erlauben Benutzern auch, ihren E-Mail-Adressen ein Pluszeichen (+) und zusätzlichen Text hinzuzufügen. Dies kann beispielsweise beim Filtern im Posteingang nützlich sein. Allerdings unterstützt Azure AD derzeit keine Pluszeichen in E-Mail-Adressen. Um Probleme bei der Übermittlung zu vermeiden, lassen Sie das Pluszeichen und alle nachfolgenden Zeichen bis zum @-Symbol weg.

6. Geben Sie eine E-Mail-Adresse, wie **sc300externaluser1@sc300email.com** ein.

7. Wählen Sie **Einladen** aus, wenn Sie fertig sind.

8. Vergewissern Sie sich, dass auf der Seite „Benutzer“ Ihr Konto aufgeführt ist und dass in der Spalte **Benutzertyp** der Eintrag **Gast** angezeigt wird.

Nach dem Senden der Einladung wird das Benutzerkonto dem Verzeichnis automatisch als Gast hinzugefügt.


### Übung 2: Einladen von Gastbenutzern per Massenvorgang

#### Aufgabe 1: Massenbenutzereinladung

Vor kurzem wurde eine Partnerschaft mit einem anderen Unternehmen geschlossen. Vorerst werden Mitarbeiter des Partnerunternehmens als Gäste hinzugefügt. Sie müssen sicherstellen, dass Sie mehrere Gastbenutzer gleichzeitig importieren können.

1. Melden Sie sich bei [https://portal.azure.com](https://portal.azure.com) als globaler Administrator an.

2. Wählen Sie im Navigationsbereich **Azure Active Directory** aus.

3. Wählen Sie unter **Verwalten** die Option **Benutzer** aus.

4. Wählen Sie auf der Seite „Benutzer“ im Menü **Massenvorgänge > Masseneinladung** aus.

     ![Screenshot: Die Seite „Alle Benutzer“ mit den hervorgehobenen Optionen „Massenvorgänge“ und „Masseneinladung“](./media/lp1-mod3-bulk-invite-option.png)

5. Wählen Sie im Bereich „Massenbenutzereinladung“ die Option **Herunterladen**, um den Download mit Einladungseigenschaften in eine CSV-Beispieldatei durchzuführen.

6. Sehen Sie sich die CSV-Datei in einem Editor an, um die Vorlage zu überprüfen.

7. Öffnen Sie die CSV-Vorlage, und fügen Sie eine Zeile für jeden Gastbenutzer hinzu. Erforderliche Werte:

    - **E-Mail-Adresse für Einladung**: Der Benutzer, der eine Einladung erhält
    - **Umleitungs-URL**: Die URL, an die der eingeladene Benutzer nach dem Akzeptieren der Einladung weitergeleitet wird.

    ![Screenshot: Beispiel einer Vorlagen-CSV-Datei zum Masseneinladen von Gastbenutzern](./media/lp1-mod3-template-csv.png)

8. Speichern Sie die Datei.

9. Navigieren Sie auf der Seite „Massenbenutzereinladung“ unter **CSV-Datei hochladen** zur entsprechenden Datei.

     **Hinweis**: Wenn Sie die Datei auswählen, wird mit der Überprüfung der CSV-Datei begonnen.

10. Nach der Überprüfung des Dateiinhalts wird die Meldung **Datei erfolgreich hochgeladen** angezeigt. Wenn Fehler vorliegen, müssen Sie diese beheben, bevor Sie den Auftrag übermitteln können.

    ![Screenshot: „Massenbenutzereinladung“ und „Datei erfolgreich hochgeladen“](./media/lp1-mod3-bulk-invite-users-upload-csv.png)

11. Wenn Ihre Datei die Überprüfung bestanden hat, wählen Sie **Senden** aus, um den Azure-Massenvorgang zum Hinzufügen der Einladungen zu starten.

12. Wählen Sie zum Anzeigen des Auftragsstatus **Klicken Sie hier, um den Status für jeden Vorgang anzuzeigen** aus. Alternativ können Sie im Abschnitt Aktivität die Option **Ergebnisse von Massenvorgängen** auswählen. Wenn Sie ausführliche Informationen zu jedem Zeilenelement des Massenvorgangs erhalten möchten, markieren Sie die Werte unter der Spalte **# Erfolg**, **# Fehler** oder **Anforderungen insgesamt**. Wenn Fehler aufgetreten sind, werden die Fehlerursachen aufgeführt.

    ![Screenshot: Die Ergebnisse eines Massenvorgangs](./media/lp1-mod3-bulk-operations-results.png)

13. Nach Abschluss des Vorgangs wird eine Benachrichtigung angezeigt, dass der Massenvorgang erfolgreich abgeschlossen wurde.

#### Aufgabe 2: Einladen von Gastbenutzern mit PowerShell

1. Starten Sie PowerShell als Administrator.  Dazu können Sie in Windows nach PowerShell suchen und „Als Administrator ausführen“ auswählen.  

1. Sie müssen das Azure AD PowerShell-Modul hinzufügen, wenn Sie es noch nicht verwendet haben.  Führen Sie den Befehl „Install-Module AzureAD“ aus.  Wählen Sie bei entsprechender Aufforderung „J“ aus, um den Vorgang fortzusetzen.

    ``` 
    Install-Module AzureAD
    ```

1. Vergewissern Sie sich, dass das Modul ordnungsgemäß installiert ist, indem Sie den folgenden Befehl ausführen:  

    ```
    Get-Module AzureAD 
    ```

1. Als Nächstes müssen Sie sich bei Azure anmelden, indem Sie Folgendes ausführen:  

    ```
    Connect-AzureAD
    ```
    
1. Das Microsoft-Anmeldefenster wird angezeigt, in dem Sie sich bei Azure AD anmelden können.  

1. Um zu überprüfen, ob Sie verbunden sind und vorhandene Benutzer anzeigen können, führen Sie Folgendes aus:  

    ```
    Get-AzureADUser 
    ```

1. Sie sind bereit, einen Gastbenutzer einzuladen.  Der folgende Befehl wird mit den Benutzerinformationen ausgefüllt und ausgeführt.  Wenn Sie mehrere Benutzer hinzufügen möchten, können Sie eine Editor-TXT-Datei verwenden, um die Benutzerinformationen hinzuzufügen und sie in PowerShell zu kopieren/einzufügen. 

    ```
    New-AzureADMSInvitation -InvitedUserDisplayName "Display" -InvitedUserEmailAddress name@emaildomain.com -InviteRedirectURL https://myapps.microsoft.com -SendInvitationMessage $true 
    ```

Sie wissen jetzt, wie Sie Benutzer im Azure AD-Portal, Microsoft 365 Admin Center und mit Masseneinladungen mittels einer CSV-Datei und Benutzer mit PowerShell-Befehlen einladen.
