---
lab:
  title: '2.6: Hinzufügen eines Verbundidentitätsanbieters'
  learning path: '01'
  module: Module 01 - Implement an identity management solution
---

# Lab 06: Hinzufügen eines Verbundidentitätsanbieters

## Labszenario

Ihr Unternehmen arbeitet mit vielen Anbietern zusammen, und Sie müssen gelegentlich einige Lieferantenkonten zu Ihrem Verzeichnis als Gast hinzufügen und es ihnen ermöglichen, sich mit ihrem Google-Konto anzumelden.

#### Geschätzte Dauer: 25 Minuten

### Übung 1 – Konfigurieren von Identitätsanbietern

#### Aufgabe 1 – Konfigurieren von Google als Identitätsanbieter

**Wichtiger Hinweis** – Für diese Übung benötigen Sie ein Gmail-Konto bei Google. Erstellen Sie ein **neues Google-Konto**, und führen Sie dann die Schritte für die Übung aus.  Achten Sie darauf, die E-Mail-Adresse und das Kennwort zu notieren. Diese sind erforderlich, um das Lab abzuschließen.

1. Wechseln Sie zur Google-APIs unter https://console.developers.google.com, und melden Sie sich mit Ihrem Google-Konto an. Es wird empfohlen, ein freigegebenes Google-Teamkonto zu verwenden.

2. Stimmen Sie den Vertragsbedingungen zu, wenn Sie dazu aufgefordert werden.

**Neues Projekt erstellen:**
3. Wählen Sie oben auf der Seite das Projektmenü aus, um die Seite Projekt auswählen zu öffnen. Wählen Sie **Neues Projekt** aus.  Ändern Sie die Standardeinstellungen der übrigen Felder nicht.

4. Geben Sie auf der Seite Neues Projekt einen Namen (z. B. **MyB2BApp**) für das Projekt ein, und wählen Sie dann **Erstellen** aus:

5. Öffnen Sie das neue Projekt über den Link Benachrichtigungen im Meldungsfeld oder das Projektmenü oben auf der Seite.

6. Wählen Sie im linken Menü **APIs und Dienste** und dann **OAuth-Zustimmungsbildschirm** aus.

7. Wählen Sie unter Benutzertyp die Option **Extern** und dann **Erstellen** aus.

8. Geben Sie auf dem **OAuth-Zustimmungsbildschirm** unter App-Informationen einen App-Namen ein, z. B. **Microsoft Entra ID**.

9. Wählen Sie unter Benutzersupport-E-Mail eine E-Mail-Adresse aus. Dies sollte die E-Mail-Adresse enthalten, die Sie zum Anmelden bei Google verwendet haben.

10. Wählen Sie unter Autorisierte Domänen die Option **+ Domäne hinzufügen** aus, und fügen Sie dann die Domäne microsoftonline.com hinzu.

   ```
   microsoftonline.com
   ```

11. Geben Sie unter Entwickler-Kontaktinformationen die E-Mail-Adresse für das Lab-Konto ein, das Sie zum Anmelden beim Portal verwendet haben.

12. Wählen Sie **Speichern und fortfahren** aus.

13. Wählen Sie im linken Menü **Anmeldeinformationen** aus.

14. Wählen Sie **+ Anmeldeinformationen erstellen** und dann **OAuth-Client-ID** aus.

15. Wählen Sie im Menü „Anwendungstyp“ die Option Webanwendung aus. Geben Sie der Anwendung einen geeigneten Namen, z. B. Microsoft Entra B2B. Fügen Sie unter **Autorisierte Weiterleitungs-URIs** die folgenden URIs hinzu:

   ```
      https://login.microsoftonline.com
   ```
      https://login.microsoftonline.com/te/**Mandanten-ID**/oauth2/authresp (wobei <tenant ID> Ihre Mandanten-ID ist)
   ```
      https://login.microsoftonline.com/te/**tenant name**.onmicrosoft.com/oauth2/authresp
       (where <tenant name> is your tenant name)
   ```

16. Klicken Sie auf **Erstellen**. Kopieren Sie Ihre **Client-ID** und den **geheimen Clientschlüssel**. Sie verwenden diese Informationen, wenn Sie den Identitätsanbieter im Azure-Portal hinzufügen.

17. Sie können Ihr Projekt im Veröffentlichungsstatus "Testen" belassen.

#### Aufgabe  2 – Hinzufügen eines Testbenutzers
18. Wählen Sie im Menü APIs und Dienste die Option **OAuth-Zustimmungsbildschirm** aus.

19. Wählen Sie im Abschnitt **Testbenutzer* der Seite die Option **+Benutzer hinzufügen** aus.

20. Geben Sie das Gmail-Konto ein, das Sie für dieses Lab erstellt haben (oder verwenden).

21. Wählen Sie **Speichern** aus.


### Übung 2 – Konfigurieren von Azure für die Arbeit mit einem externen Identitätsanbieter

#### Aufgabe 1: Konfigurieren des Google-Verbunds in Microsoft Entra ID
1. Melden Sie sich bei  [https://entra.microsoft.com](https://entra.microsoft.com)  als Admin an.

2. Wählen Sie  **Microsoft Entra ID** aus.

3. Wählen Sie unter **Identität** die Option  **Externe Identitäten** aus.

4. Wählen Sie im Menü auf der linken Seite **Alle Identitätsanbieter** aus.

5. Microsoft stellt einen direkten Verbund für **Google** als Identitätsanbieter bereit.Dies kann durch Auswahl von **+ Google** auf der Seite **Externe Identitäten | Alle Identitätsanbieter** initiiert werden.
 
6. Nachdem Sie + Google ausgewählt haben, wird eine andere Seite mit zusätzlichen Informationen geöffnet, die zum Konfigurieren von Google als Identitätsanbieter erforderlich sind.  

7. Geben Sie die **Client-ID** und den **geheimen Clientschlüssel** ein, die Sie zuvor erhalten haben.

8. Wählen Sie **Speichern**.

Damit wird die Konfiguration von Google als Identitätsanbieter abgeschlossen.

#### Aufgabe 2 – Einladen eines Testbenutzerkontos
9. Wenn Sie ein vorhandenes Gmail-Konto verwendet haben, denken Sie daran, das Konto mit **Externe Identitäten | Alle Identitätsanbieter** zu löschen. Sie können auch zur Google-Entwicklerkonsole zurückkehren und das von Ihnen erstellte Projekt löschen.

10. Öffnen Sie Microsoft Entra ID.

11. Wechseln Sie zu "Benutzer", und wählen Sie dann **Alle Benutzer** aus.

12. Klicken Sie auf **+ Neuer Benutzer**.

13. Wählen Sie die Menüoption **Externen Benutzer einladen** aus.

14. Geben Sie die Informationen für das Gmail-Konto ein, das Sie als Testbenutzer für die Google App in Übung 1, Aufgabe 2 eingerichtet haben.

15. Geben Sie eine persönliche Nachricht nach Wunsch ein.

16. Wählen Sie **Einladen** aus.

#### Aufgabe 3 – Annehmen der Einladung und Anmeldung
17. Verwenden Sie einen InPrivate-Browser, um sich bei Ihrem Gmail-Konto anzumelden.

18. Öffnen Sie die **Microsoft-Einladung im Auftrag von** im Posteingang.

19. Wählen Sie den Link **Einladung annehmen** in der Nachricht aus.

20. Geben Sie Ihren Benutzernamen und Ihr Kennwort wie gewünscht im Anmeldedialogfeld ein (falls angefordert).
   **HINWEIS** Wenn der Verbund ordnungsgemäß funktioniert, werden hier die ersten Ergebnisse Ihres neuen externen Google-Identitätsanbieters angezeigt.  Sie wechseln zum Anmeldebildschirm und können sich mit Ihren Gmail-Anmeldeinformationen anmelden.  Wenn der Verbund nicht funktioniert oder nicht eingerichtet wurde, wird dem Benutzer nach der Anmeldung eine E-Mail zur ÜBERPRÜFUNG DES KONTOS gesendet, um das Konto zu bestätigen.  Beim Verbund ist keine zusätzliche Überprüfung erforderlich.

   **HINWEIS** Wenn Sie einen Zugriffsfehler 500 erhalten, warten Sie etwa 30 Sekunden, und aktualisieren Sie die Seite.  Wählen Sie die Option ERNEUT ÜBERMITTELN aus.  Dieser Fehler ist ein Zeitplanungsproblem nur in der Lab-Umgebung.

21. Lesen Sie die neue Nachricht mit dem Betreff **Permissions requested by:**, die Sie erhalten.  Diese Nachricht stammt aus Ihrer Azure Lab-Domäne.

22. Klicken Sie auf **Annehmen**.

23. Sobald die Anmeldung abgeschlossen ist, wird Ihnen MyApplications gesendet.

#### Aufgabe 4 – Anmelden mit Ihrem Google-Konto bei Microsoft 365
24. Nachdem Sie den Vorgang zum Einladen externer Benutzer aus Aufgabe 3 abgeschlossen haben, können Sie sich direkt bei Microsoft Online anmelden.

25. Öffnen Sie eine neue Registerkarte im Browser, den Sie geöffnet haben.
   **HINWEIS**: Wenn Sie in Aufgabe 3 keinen neuen InPrivate-Browser geöffnet haben, sollten Sie dies für diesen Schritt tun.

26. Geben Sie die folgende Webadresse ein:

   ```
   login.microsoftonline.com
   ```

27. Klicken Sie im Dialogfeld auf **Anmeldeoptionen**.
 
28. Wählen Sie **Bei einer Organisation anmelden** aus.

29. Geben Sie den **Domänennamen des Lab-Mandanten** in das Feld ein, und klicken Sie auf **Weiter**.

30. Geben Sie die von Ihnen erstellte **Google**-E-Mail-Adresse und das von Ihnen erstellte Kennwort ein.
Zu diesem Zeitpunkt sollte Ihr Konto zur Bestätigung an Google übergeben werden; geben Sie dann das Microsoft Office-Portal ein.
