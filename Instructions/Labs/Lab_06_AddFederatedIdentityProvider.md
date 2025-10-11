---
lab:
  title: '06: Hinzufügen eines Verbundidentitätsanbieters'
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Lab 06: Hinzufügen eines Verbundidentitätsanbieters

### Anmeldetyp = Microsoft 365 Admin

## Labszenario

Ihr Unternehmen arbeitet mit vielen Anbietern zusammen, und gelegentlich müssen Sie Ihrem Verzeichnis einige Lieferantenkonten als Gast hinzufügen und es ihnen ermöglichen, sich mit ihrem Google-Konto anzumelden.

#### Geschätzte Dauer: 25 Minuten

### Übung 1: Konfigurieren von Identitätsanbietern

#### Aufgabe 1: Konfigurieren von Google als Identitätsanbieter

**Wichtiger Hinweis**: Für diese Übung benötigen Sie ein Gmail-Konto auf Google. Erstellen Sie ein **neues Google-Konto**, und führen Sie dann die Schritte für die Übung aus.  Notieren Sie die E-Mail-Adresse und das Kennwort; sie sind erforderlich, um das Lab durchzuführen.

1. Wechseln Sie zu den Google-APIs unter https://console.developers.google.com, und melden Sie sich mit Ihrem Google-Konto an. Es wird empfohlen, ein freigegebenes Google-Teamkonto zu verwenden.

2. Stimmen Sie den Vertragsbedingungen zu, wenn Sie dazu aufgefordert werden.

**Erstellen eines neuen Projekts:**
3. Wählen Sie oben auf der Seite das Projektmenü aus, um die Seite „Projekt auswählen“ zu öffnen. Wählen Sie **Neues Projekt** aus.  Ändern Sie die Standardeinstellungen der anderen Felder nicht.

4. Geben Sie auf der Seite „Neues Projekt“ dem Projekt einen Namen: +++MyB2BApp+++, und wählen Sie dann **Erstellen**.

5. Öffnen Sie das neue Projekt über den Link Benachrichtigungen im Meldungsfeld oder das Projektmenü oben auf der Seite.

6. Wählen Sie im linken Menü **APIs & Dienste** und dann **OAuth-Zustimmungsbildschirm** aus.

7. Klicken Sie auf die Schaltfläche **Erste Schritte**.

8. Geben Sie auf dem Bildschirm „Anwendungsinformationen“ die folgenden Informationen ein:

| Abschnitt | Feldname | Wert |
| :---    | :---    | :---  |
| 1. App-Information | | |
|            | App-Name | +++Microsoft Entra ID+++ |
|            | E-Mail zur Benutzerunterstützung | Wählen Sie den E-Mail-Namen aus der Dropdown-Liste aus. |
| 2. Zielgruppe | | |
|            | Innen/außen | **Extern** |
| 3. Kontaktinformationen | | |
|            | E-Mail-Adressen | Dieselbe E-Mail-Adresse wie oben verwenden |
| 3. Fertigstellen | | |
|            | Vereinbarung | Aktivieren Sie das Kontrollkästchen. |

9. Wählen Sie die Schaltfläche **Erstellen**, um fortzufahren.

10. Wählen Sie die Schaltfläche **OAuth-Client erstellen**.

11. Wählen Sie **Anwendungstyp = Webanwendung**.

12. Übernehmen Sie den Standardnamen für die Anwendung.

13. Wählen Sie innerhalb der **Autorisierte JavaScript-Ursprünge** die Schaltfläche **+ URI hinzufügen**.

14. Geben Sie die URI +++https://microsoftonline.com+++ als Wert ein.

15. Wählen Sie innerhalb der **Autorisierten Weiterleitungs-URIs** die Schaltfläche **+ URI hinzufügen**.  Sie müssen in diesem Abschnitt drei verschiedene URIs hinzufügen:

 - **Erste URI** = +++https://login.microsoftonline.com+++
 - **Zweite URI** = +++https://login.microsoftonline.com/te/**Mandanten-ID**/oauth2/authresp+++ (wobei <tenant ID> Ihre Mandanten-ID ist)
 - **Dritte URI** = +++https://login.microsoftonline.com/te/**Mandantenname**.onmicrosoft.com/oauth2/authresp+++ (wobei <tenant name> Ihr Mandantenname ist)

**Lab-Tipp**: Dieser Schritt ist möglicherweise einfacher, wenn Sie Notepad in der Lab-VM verwenden, um diese URIs zu erstellen, und sie dann kopieren und einfügen.

**Lab-Tipp 2**: Die Ergebnisse sollten ähnlich wie hier aussehen, mit Ihrer Mandanten-ID und Ihrem Mandantennamen.

| URI # | Link |
| :--- | :--- |
| URIs 1 | https://login.microsoftonline.com |
| URIs 2 | https://login.microsoftonline.com/te/aaaa1111bbbb2222cccc/oauth2/authresp |
| URIs 3 | https://login.microsoftonline.com/te/MyTenantName.onmicrosoft.com/oauth2/authresp |

16. Wählen Sie die Schaltfläche **Erstellen**.

17. Wenn das Element erstellt wird, kopieren Sie die **Client-ID** und den **geheimen Clientschlüssel** später in den Editor.

18. Sie können Ihr Projekt in diesem Zustand belassen, eine Veröffentlichung ist nicht erforderlich.

#### Aufgabe 2: Hinzufügen eines Testbenutzers

1. Wählen Sie im Menü auf der linken Seite den Eintrag **Zielgruppe** aus.

2. Wählen Sie im Abschnitt **Testbenutzer** der Seite **+ Benutzer hinzufügen** aus.

3. Geben Sie das Gmail-Konto ein, das Sie für dieses Lab verwenden.

4. Wählen Sie**Speichern**

#### Aufgabe 3: Hinzufügen einer autorisierten Domäne zum Branding

1. Wählen Sie im Menü auf der linken Seite den Eintrag **Branding** aus.

2. Scrollen Sie zum Ende der Seite.

3. Fügen Sie im Abschnitt **Autorisierte Domänen** die Domäne **microsoftonline.com** hinzu.

4. Fügen Sie unter **Entwicklerkontaktinformationen** die E-Mail-Adresse hinzu, die Sie für dieses Lab verwenden.

5. Wählen Sie **Speichern**.


### Übung 2 – Konfigurieren von Azure für die Arbeit mit einem externen Identitätsanbieter

#### Aufgabe 1: Konfigurieren des Google-Verbunds in Microsoft Entra ID
1. Melden Sie sich bei  [https://entra.microsoft.com](https://entra.microsoft.com)  als Admin an.

2. Wählen Sie  **Microsoft Entra ID** aus.

3. Wählen Sie unter **Identität** die Option  **Externe Identitäten** aus.

4. Wählen Sie im Menü auf der linken Seite **Alle Identitätsanbieter** aus.

5. Microsoft stellt einen direkten Partnerverbund für **Google** als Identitätsanbieter bereit.  Dies kann durch Auswahl von **+ Google** auf der Seite **External Identities | Alle Identitätsanbieter** initiiert werden.
 
6. Nachdem Sie „+ Google“ ausgewählt haben, wird eine andere Seite mit zusätzlichen Informationen geöffnet, die zum Konfigurieren von Google als Identitätsanbieter erforderlich sind.  

7. Geben Sie die **Client-ID** und den **geheimen Clientschlüssel** ein, die Sie zuvor erhalten haben.

8. Wählen Sie **Speichern** aus.

Damit ist die Konfiguration von Google als Identitätsanbieter abgeschlossen.

#### Aufgabe 2: Einladen eines Testbenutzerkontos
1. Wenn Sie ein vorhandenes Gmail-Konto verwendet haben, denken Sie daran, das Konto mit **External Identities | Alle Identitätsanbieter** zu löschen. Sie können auch zur Google-Entwicklerkonsole zurückkehren und das von Ihnen erstellte Projekt löschen.

2. Öffnen Sie Microsoft Entra ID.

3. Wechseln Sie zu "Benutzer", und wählen Sie dann **Alle Benutzer** aus.

4. Klicken Sie auf **+ Neuer Benutzer**.

5. Wählen Sie im Dropdownmenü **Invite external user** aus.

6. Geben Sie die Informationen für das Gmail-Konto ein, das Sie als Testbenutzer für die Google App in Übung 1 Aufgabe 2 eingerichtet haben.

7. Geben Sie eine persönliche Nachricht ein.

8. Wählen Sie **Überprüfen + einladen** und dann **Einladen** aus.


| **Sicherheitshinweis** |
| ----: |
| Wenn Sie ein vorhandenes Gmail-Konto verwenden, das Passkeys aktiviert hat, können Sie die Anmeldeprozesse in der Lab-Umgebung nicht abschließen.  Passkey erfordert Bluetooth, das nicht über die VM aktiviert werden kann.  Sie können das Lab dennoch abschließen, indem Sie die letzten Aufgaben in einem InPrivate-Browser außerhalb der Lab-Umgebung ausführen. |


#### Aufgabe 3: Annehmen der Einladung und Anmeldung

1. Verwenden Sie einen InPrivate-Browser, um sich bei Ihrem Gmail-Konto anzumelden.

2. Öffnen Sie **Microsoft-Einladung im Namen von** im Posteingang.

3. Wählen Sie den Link **Einladung annehmen** in der Nachricht aus.

3. Geben Sie Ihren Benutzernamen und Ihr Kennwort wie gewünscht im Anmeldedialogfeld ein (falls angefordert).

   **HINWEIS**: Wenn der Partnerverbund ordnungsgemäß funktioniert, werden hier die ersten Ergebnisse Ihres neuen Google External Identity-Anbieters angezeigt.  Sie wechseln zum Anmeldebildschirm und können sich mit Ihren Gmail-Anmeldeinformationen anmelden.  Wenn der Partnerverbund nicht funktioniert oder nicht eingerichtet wurde, erhält der Benutzer nach der Anmeldung eine KONTOÜBERPRÜFUNGS-E-Mail, um das Konto zu bestätigen.  Für den Partnerverbund ist keine zusätzliche Überprüfung erforderlich.

   **HINWEIS**: Wenn Sie den Zugriffsfehler 500 erhalten, warten Sie etwa 30 Sekunden, und aktualisieren Sie die Seite.  Wählen Sie ERNEUT ÜBERMITTELN aus.  Dieser Fehler ist ein Zeitplanungsproblem nur in der Labumgebung.

4. Lesen Sie die neue Nachricht **Permissions requested by**, die Sie erhalten.  Diese Nachricht stammt aus Ihrer Azure Lab-Domäne.

5. Wählen Sie **Annehmen** aus.

6. Sobald die Anmeldung abgeschlossen ist, wird Ihnen „MyApplications“ zugesandt.

#### Aufgabe 4: Anmelden bei Microsoft 365 mit Ihrem Google-Konto

1. Nachdem Sie den Prozess zum Einladen externer Benutzer Aufgabe 3 abgeschlossen haben, können Sie sich direkt bei Microsoft Online anmelden.

2. Öffnen Sie eine neue Registerkarte in Ihrem geöffneten Browser.

   **HINWEIS**: Wenn Sie in Aufgabe 3 keinen neuen InPrivate-Browser geöffnet haben, sollten Sie dies für diesen Schritt tun.

3. Geben Sie die folgende Webadresse ein:

   ```
   login.microsoftonline.com
   ```

4. Wählen Sie im Dialogfeld **Anmeldeoptionen** aus.
 
5. Wählen Sie **Bei einer Organisation anmelden** aus.

6. Geben Sie den Namen Ihrer **Labmandantendomäne** in das Feld ein, und wählen Sie **Weiter** aus.

7. Geben Sie die **Google-** E-Mail-Adresse und das von Ihnen erstellte Kennwort ein.

Zu diesem Zeitpunkt sollte Ihr Konto zur Bestätigung an Google übergeben werden; geben Sie dann das Microsoft Office-Portal ein.
